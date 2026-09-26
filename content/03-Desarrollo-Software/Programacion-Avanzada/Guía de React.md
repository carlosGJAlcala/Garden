---
title: "Guía de React"
tags: [universidad, 4anyo, tfg]
date: 2026-08-12
lang: es
---
# GUÍA DE REACT

## Como crear una app en React

```bash
npx create-react-app my-app
```

## Arrancar una app en React

```bash
npm start
```

## Como insertar variables en un componente

Renderezizar contenido dinámico en un componente

```jsx
const App = () => {
  const now = new Date ()
  const a = 10
  const b = 20
  console.log ( now, a+b)
  return (
    <div>
      <p>Hello world, it is {now.toString ()}</p>
      <p>
        {a} plus {b} is {a + b}
      </p>
    </div>
  )
}
```

## Como tener componentes multiples

Los nombres de los componentes debe comenzar en mayúsculas si comienza en minúsculas, react no lo le como un componente si no como una etiqueta.

```jsx
const Hello = () => {
  return (
    <div>
      <p>Hello world</p>
    </div>
  )
}
const App = () => {
  return (
    <div>
      <h1>Greetings</h1>
      <Hello />
    </div>
  )
}
```

## Pasar datos a componentes hijos

**Para meter codigo de javascrip usamos las llaves {},** y tambie para poder ser renderizado y solo acepta datos primitivos no objetos

```jsx
const Hello = ( props) => {
  console.log ( props)
  return (
    <div>
      <p>
        Hello {props.name}, you are {props.age} years old
      </p>
    </div>
  )
}
const App = () => {
  const name = 'Peter'
  const age = 10
  return (
    <div>
      <h1>Greetings</h1>
      <Hello name='Maya' age={26 + 10} />
      <Hello name={name} age={age} />
    </div>
  )
}
```

## Como renderizar objectos

```jsx
const App = () => {
  const friends = [
    { name: 'Peter', age: 4 },
    { name: 'Maya', age: 10 },
  ]
  return (
    <div>
      <p>{friends[0].name} {friends[0].age}</p>
      <p>{friends[1].name} {friends[1].age}</p>
    </div>
  )
}
export default App
```

## Como hacer clases en JavaScript

```javascript
class Person {
  constructor ( name, age) {
    this.name = name
    this.age = age
  }
  greet () {
    console.log ('hello, my name is ' + this.name)
  }
}
const adam = new Person ('Adam Ondra', 29)
adam.greet ()
const janja = new Person ('Janja Garnbret', 23)
janja.greet ()
```

## Como hacer funciones auxiliares y desestructuración de props

```javascript
props = {
  name: 'Arto Hellas',
  age: 35,
}
```

```jsx
const Hello = ( props) => {
  const name = props.name
  const age = props.age
// tambien se puede hacer de la siguiente forma
const { name, age } = props
  const bornYear = () => new Date ().getFullYear () - age
  return (
    <div>
      <p>Hello {name}, you are {age} years old</p>
      <p>So you were probably born in {bornYear ()}</p>
    </div>
  )
}
```

Se puede comprimir la función de la siguiente manera:

```javascript
const bornYear = () => new Date ().getFullYear () - age
const bornYear = () => {
  return new Date ().getFullYear () - age
}
```

Tambien se puede desectructurar de la siguiente forma:

```jsx
const Hello = ({ name, age }) => {
  const bornYear = () => new Date ().getFullYear () - age
  return (
    <div>
      <p>
        Hello {name}, you are {age} years old
      </p>
      <p>So you were probably born in {bornYear ()}</p>
    </div>
  )
}
```

## Como renderizar una página ( use state) hook estado

Con useState se renderiza el componente y sus componentes hijos cada vez que se llama la función que se le pasa mediante desectructuracion al useState, está renderización se hace cuando se termina de ejecutar todo el componente, la cual consistiría en volver a ejecutar el codigo otravez.

El useState ( 0) es porque se inicializa con cero.

```jsx
import { useState } from 'react'
const App = () => {
  const [ counter, setCounter ] = useState ( 0)
  setTimeout (
    () => setCounter ( counter + 1),
    1000
  )
  return (
    <div>{counter}</div>
  )
}
export default App
```

## Control eventos ( por ejemplo un usuario pulsado un botón)

Los controles de eventos son funciones, que pueden ser llamadas ( o bien pasandole una referencia o bien una función al atributo del controlador de evento, por ejemplo onClick.

```jsx
const App = () => {
  const [ counter, setCounter ] = useState ( 0)
  const increaseByOne = () => setCounter ( counter + 1)
  const setToZero = () => setCounter ( 0)
  return (
    <div>
      <div>{counter}</div>
      <button onClick={increaseByOne}>
        plus
      </button>
      <button onClick={setToZero}>
        zero
      </button>
    </div>
  )
}
```

## Como renderizar objectos usando hook

```jsx
const App = () => {
  const [clicks, setClicks] = useState ({
    left: 0, right: 0
  })
  const handleLeftClick = () => {
    const newClicks = {
      left: clicks.left + 1,
      right: clicks.right
    }
    setClicks ( newClicks)
  }
  const handleRightClick = () => {
    const newClicks = {
      left: clicks.left,
      right: clicks.right + 1
    }
    setClicks ( newClicks)
  }
  return (
    <div>
      {clicks.left}
      <button onClick={handleLeftClick}>left</button>
      <button onClick={handleRightClick}>right</button>
      {clicks.right}
    </div>
  )
}
```

## Como renderizar arreglos usando hook

```jsx
const App = () => {
  const [left, setLeft] = useState ( 0)
  const [right, setRight] = useState ( 0)
  const [allClicks, setAll] = useState ([])
  const handleLeftClick = () => {
    setAll ( allClicks.concat ('L'))
    setLeft ( left + 1)
  }
  const handleRightClick = () => {
    setAll ( allClicks.concat ('R'))
    setRight ( right + 1)
  }
  return (
    <div>
      {left}
      <button onClick={handleLeftClick}>left</button>
      <button onClick={handleRightClick}>right</button>
      {right}
      <p>{allClicks.join (' ')}</p>
    </div>
  )
}
```

## Renderizar colecciones ( lista plantas – lista usuarios)

Para introducir listas o colleciones tenemos que usar la función map or reduce o find

```jsx
const Note = ({ note }) => {
  return (
    <li>{note.content}</li>
  )
}
const App = ({ notes }) => {
  return (
    <div>
      <h1>Notes</h1>
      <ul>
        {notes.map ( note =>
          <Note key={note.id} note={note} />
        )}
      </ul>
    </div>
  )
}
```

## Formulario como hacerlo

```jsx
const App = ( props) => {
  const [notes, setNotes] = useState ( props.notes)
  const [newNote, setNewNote] = useState (
    'a new note...'
  )
  const addNote = ( event) => {
    event.preventDefault ()
    console.log ('button clicked', event.target)
  }
  return (
    <div>
      <h1>Notes</h1>
      <ul>
        {notes.map ( note =>
          <Note key={note.id} note={note} />
        )}
      </ul>
      <form onSubmit={addNote}>
        <input value={newNote} />
        <button type="submit">save</button>
      </form>  
    </div>
  )
}
```

## Como obtener datos de una API

Para ello usamos axios

```bash
npm install axios
```

### GET

Para hacer un get lo hacemos de la siguiente forma:

```javascript
import axios from 'axios'
const promise = axios.get ('http://localhost:3001/notes')
console.log ( promise)
const promise2 = axios.get ('http://localhost:3001/foobar')
console.log ( promise2)
```

Una promesa es un objeto que representa la evutual finalización o falla de una operación asíncrona.

Para acceder datos a los datos se pueden acceder de la siguiente forma:

```javascript
axios
  .get ('http://localhost:3001/notes')
  .then ( response => {
    const notes = response.data
    console.log ( notes)
  })
```

## Use effect hook

Para ello utilizamos effect hooks , el cual sirve para renderizar un componecte cada vez que cambie la dependencia de un componente.

Esta función recibe dos parámetros , la función de codigo a ejecutar y un arreglo de dependencias, si la dependencia cambia solo se ejecutara cuando se renderiza el codigo en el dom por primera vez

```jsx
import { useState, useEffect } from 'react'
import axios from 'axios'
import Note from './components/Note'
const App = () => {
  const [notes, setNotes] = useState ([])
  const [newNote, setNewNote] = useState ('')
  const [showAll, setShowAll] = useState ( true)
  useEffect (() => {
    console.log ('effect')
    axios
      .get ('http://localhost:3001/notes')
      .then ( response => {
        console.log ('promise fulfilled')
        setNotes ( response.data)
      })
  }, [])
  console.log ('render', notes.length, 'notes')
  // ...
}
```

### POST

```javascript
addNote = event => {
  event.preventDefault ()
  const noteObject = {
    content: newNote,
    important: Math.random () < 0.5,
  }
  axios
    .post ('http://localhost:3001/notes', noteObject)
    .then ( response => {
      console.log ( response)
    })
}
```
