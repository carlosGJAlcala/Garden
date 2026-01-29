---
title: "Selenium"
date: 2026-01-27
tags:
  - desarrollo-software
  - java
---



> **Relacionado**: [[03-Desarrollo-Software/Python/Selenium|Selenium]].

---

**1. Instala las dependencias de Selenium en Java**  
Si usas Maven, añade esto a tu `pom.xml`:

```xml
<dependencies>
    <dependency>
        <groupId>org.seleniumhq.selenium</groupId>
        <artifactId>selenium-java</artifactId>
        <version>4.21.0</version>
    </dependency>
</dependencies>
```

---

**2. Descarga el WebDriver del navegador**

- Para Chrome: [https://googlechromelabs.github.io/chrome-for-testing/](https://googlechromelabs.github.io/chrome-for-testing/)
    
- Para Firefox: [https://github.com/mozilla/geckodriver/releases](https://github.com/mozilla/geckodriver/releases)
    

Guarda el archivo y ponlo en una carpeta accesible (por ejemplo, `C:\drivers`).

---

**3. Código Java para buscar en Google**  
Ejemplo sencillo usando Chrome:

```java
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;

import java.util.List;

public class BuscadorGoogle {
    public static void main(String[] args) {
        // Ruta al chromedriver
        System.setProperty("webdriver.chrome.driver", "C:\\drivers\\chromedriver.exe");

        // Inicia el navegador
        WebDriver driver = new ChromeDriver();

        try {
            // Abre Google
            driver.get("https://www.google.com");

            // Acepta cookies si aparece el botón
            try {
                WebElement aceptar = driver.findElement(By.xpath("//div[contains(text(),'Aceptar todo')]"));
                aceptar.click();
            } catch (Exception e) {
                System.out.println("No se encontraron cookies para aceptar");
            }

            // Busca un término
            WebElement cajaBusqueda = driver.findElement(By.name("q"));
            cajaBusqueda.sendKeys("noticias de ciberseguridad 2025");
            cajaBusqueda.submit();

            // Espera un poco a que carguen los resultados
            Thread.sleep(2000);

            // Obtiene los resultados
            List<WebElement> resultados = driver.findElements(By.cssSelector("h3"));

            // Imprime los títulos de los primeros resultados
            for (WebElement r : resultados) {
                System.out.println(r.getText());
            }

        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            // Cierra el navegador
            driver.quit();
        }
    }
}
```

---

**4. Cosas a tener en cuenta**

- Google puede detectar automatizaciones y pedirte un CAPTCHA.
    
- Si quieres hacer scraping a gran escala, es mejor usar APIs o servicios de búsqueda para evitar bloqueos.
    
- Puedes usar **`WebDriverWait`** en vez de `Thread.sleep()` para esperar de forma más precisa.
    
- Si quieres que el navegador no aparezca en pantalla, puedes usar **modo headless**.
    

---

Si quieres, puedo prepararte **una versión mejorada con `WebDriverWait` y modo headless** para que sea más rápida y estable.