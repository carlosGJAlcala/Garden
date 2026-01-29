---
title: "fastapi_app.py"
date: 2026-01-26
tags:
  - ciencias-computacion
  - ia
---
Para tu caso (agente interno que genere documentos con formato corporativo), iría directo a **Python + Ollama + plantillas Jinja2**, y si más adelante necesitas orquestación de flujos, añadiría **Magic Flow** como capa opcional. n8n aquí aporta poco: está pensado para “conectar APIs” más que para razonar y maquetar documentos.

La idea es simple: el agente razona el contenido con el LLM local (Ollama), valida y normaliza con Python, y renderiza en tus plantillas oficiales para garantizar el formato siempre igual.

Así lo montaría, de forma mínima pero sólida:

1. Un servicio en **FastAPI** con dos rutas: “/draft” para que el LLM redacte secciones según un **esquema** y “/render” para convertir eso en el documento final con **Jinja2**. Los **esquemas** (Pydantic) te aseguran que siempre existan títulos, versión, fecha, propietario, áreas, secciones, etc.
    
2. **Plantillas Jinja2** en un repo privado: una por tipo de documento (política, procedimiento, informe técnico, acta). El agente nunca “inventa” formato, solo rellena bloques.
    
3. **Prompts con instrucciones duras**: estilo, tono, longitud, terminología corporativa y checklist de cumplimiento. Si el modelo se sale, devuelves error y reintentas con corrección.
    
4. **Auditoría y aprobaciones**: guarda el JSON de entrada, el borrador del LLM y el PDF final; añade campos “autor”, “revisor”, “versión”. La aprobación la puedes hacer por Slack/Email o una pequeña UI interna.
    
5. **Modelos en Ollama**: empieza con Llama 3.1 o Qwen2.5 para español. Para documentos largos, genera por secciones. Si necesitas tablas complejas, pide JSON estructurado y luego lo pintas con Jinja2/WeasyPrint o Docx.
    

Ejemplo ultra-sintético de esqueleto:

```python
# fastapi_app.py

> **Relacionado**: [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Alcance|Alcance]]. [[01-Ciberseguridad/Gestion-Seguridad/Tema4Auditoria/Controles|Controles]]. [[02-Ciencias-Computacion/IA/Notas|Notas]]. [[02-Ciencias-Computacion/Sistemas-Operativos/Docker|Docker]]. [[08-Personal/Cuidado-Personal/Pelo/resumen|resumen]].

from fastapi import FastAPI
from pydantic import BaseModel, Field
from jinja2 import Environment, FileSystemLoader
import requests, datetime, os

OLLAMA_URL = os.getenv("OLLAMA_URL", "http://localhost:11434/api/generate")
MODEL = os.getenv("MODEL", "llama3.1")

app = FastAPI()
env = Environment(loader=FileSystemLoader("./plantillas"))

class DocSpec(BaseModel):
    tipo: str = Field(..., description="ej: politica, procedimiento, informe")
    titulo: str
    propietario: str
    areas: list[str]
    objetivos: list[str]
    alcance: str
    requisitos: list[str]
    anexos: list[str] = []
    notas: str = ""

class Draft(BaseModel):
    secciones: dict  # {"Introducción": "...", "Desarrollo": "...", ...}

def llama(prompt: str) -> str:
    payload = {"model": MODEL, "prompt": prompt, "stream": False}
    r = requests.post(OLLAMA_URL, json=payload, timeout=120)
    r.raise_for_status()
    return r.json()["response"]

SYSTEM = (
    "Eres un redactor corporativo. Escribe claro, conciso, en español España, "
    "con tono profesional y numeraciones estables. No inventes formato."
)

@app.post("/draft", response_model=Draft)
def draft(spec: DocSpec):
    prompt = f"""{SYSTEM}
Vas a preparar un borrador para un documento de tipo "{spec.tipo}".
Título: {spec.titulo}
Propietario: {spec.propietario}
Áreas: {", ".join(spec.areas)}
Objetivos: {", ".join(spec.objetivos)}
Alcance: {spec.alcance}
Requisitos: {", ".join(spec.requisitos)}
Notas: {spec.notas}

Devuelve un JSON con las claves:
"Resumen Ejecutivo", "Contexto", "Contenido", "Riesgos y Controles", "Conclusiones".

Cada sección debe ser 2–4 párrafos. No uses markdown.
Responde solo con JSON válido.
"""
    raw = llama(prompt)
    # mínimo saneado: si algo falla, levantarías 422 o reintentas con corrección
    import json
    secciones = json.loads(raw)
    return Draft(secciones=secciones)

@app.post("/render")
def render(spec: DocSpec, draft: Draft):
    template = env.get_template(f"{spec.tipo}.j2")  # p.ej. plantillas/politica.j2
    now = datetime.date.today().isoformat()
    html = template.render(
        titulo=spec.titulo,
        propietario=spec.propietario,
        areas=spec.areas,
        objetivos=spec.objetivos,
        alcance=spec.alcance,
        requisitos=spec.requisitos,
        secciones=draft.secciones,
        fecha=now,
        version="1.0.0",
    )
    # aquí conviertes a PDF (WeasyPrint) o DOCX (docxtpl) según prefieras
    return {"html": html}
```

Una plantilla Jinja2 de ejemplo muy corta (`plantillas/politica.j2`):

```jinja2
<h1>{{ titulo }}</h1>
<p><strong>Versión:</strong> {{ version }} • <strong>Fecha:</strong> {{ fecha }}</p>
<p><strong>Propietario:</strong> {{ propietario }} • <strong>Áreas:</strong> {{ ", ".join(areas) }}</p>

<h2>Objetivos</h2>
<ul>{% for obj in objetivos %}<li>{{ obj }}</li>{% endfor %}</ul>

<h2>Alcance</h2>
<p>{{ alcance }}</p>

<h2>Requisitos</h2>
<ul>{% for r in requisitos %}<li>{{ r }}</li>{% endfor %}</ul>

{% for titulo, cuerpo in secciones.items() %}
  <h2>{{ titulo }}</h2>
  <p>{{ cuerpo }}</p>
{% endfor %}
```

Con esto ya tienes un “agente” controlado: el LLM solo redacta contenido bajo tus reglas, y el formato queda blindado por la plantilla. Si luego quieres orquestar pasos (pedir datos a Jira/Confluence, lanzar validaciones, publicar a SharePoint), puedes envolverlo en **Magic Flow** y añadir nodos de aprobación. Todo corre on-prem con Ollama, sin sacar datos fuera.

Si te encaja, te dejo en la siguiente vuelta un repositorio mínimo con:

- Docker Compose para FastAPI + Ollama.
    
- Dos plantillas base (política y procedimiento).
    
- Conversión a PDF con WeasyPrint y almacenamiento versionado en disco.