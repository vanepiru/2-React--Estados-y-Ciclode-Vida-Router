# React

## ***Estados y Ciclo de vida ***

***Estado***

El estado puede ser un objeto (Por lo regular es un JSON) o variable.
Podemos utilizarlo para realizar cambios desde dentro de los componentes.
Si el estado cambia, los componentes reaccionan a este cambio modificando algo en si mismos, que prácticamente siempre será un cambio en la DOM.
El estado también puede ser modificado desde fuera del componente y dicho componente reaccionará de la misma manera al cambio.

USO DEL STATE EN COMPONENTES DE CLASES (CLASS COMPONENT)
Para acceder y manipular el estado dentro de un componente de clase debemos hacer uso de this,
ejemplo de como podemos inicializar nuestro state.
 

INICIALIZANDO EL STATE EN UN COMPONENTE DE CLASE
Tomando el ejemplo que realizamos en el vídeo, podemos declarar el estado de la siguiente forma dentro del constructor de la clase

class Hijo1 extends React.Component{
  constructor(props){
    super(props);
      this.state={
      titulo:"Hijo 1",
      subtitulo:"Contador",
      cuenta:1
    }
    ...
  }
}

 

***MODIFICAR EL STATE EN UN COMPONENTE DE CLASE***
La manera correcta de actualizar y manipular el estado en este tipo de componentes es a través de setState, por ejemplo:

class Hijo1 extends React.Component{
    ...
  aumentar=()=>{
    this.setState({
      ...this.state,
      cuenta:this.state.cuenta + 1
    });
  }
    ...
}

***¿Qué son los métodos de ciclos de vida?***

Son la serie de eventos que sucede desde que se crea el componente hasta su destrucción
Para que te sea mas fácil de comprender el ciclo de vida de un componente.

Los palabras claves de los métodos son las siguientes

***1º Mounting***: creación del componente

***2º Update***: Cambios en el componente

***3º Unmount***: Destrucción del componente

Ciclos más usados

Render()

El método render() es el método más usado es el unico metodo obligatorio en la clase de un componente de React

***1º componentDidMount()***

En el momento que tu componente ya se creo, es cuando este metodo empieza a ejecutarse.

En este método se suele poner las llamadas a la api en el caso de que lo necesitaras.

Ejemplo:

cargarDatos = () => {
    var url = "http://yoururlapirequest.com"
    axios.get(url).then(res => {
        this.setState({
            departamentos: res.data
        });
    });
}
componentDidMount = () => {
    this.cargarDatos();
}
***2º componentDidUpdate()***

Este ciclo se invoca tan pronto como la actualizacion ocurre.

Se suele usar para actualizar el DOM con los datos de tu state.

Ejemplo de uso:

componentDidUpdate(previasProps, previoState) {
        if (this.props.input == previasProps.input) {
          // Llamar a una funcion o hacer peticiones ajax
        }
}
***3º componentWillUnmount()***

Como el nombre suguiere, este metodo se llamara justo antes de que sea destruido.
Se suele utilizar para limpieza (cerrar peticiones ajax, timeouts, eliminar Eventos… )

Ejemplo de uso:

componentWillUnmount() {
      document.removeEventListener("click", funcionAsignada);      
}


https://techclub.tajamar.es/ciclo-de-vida-de-los-componentes-en-react/

## . ***Puerto por Defecto***

3000

## . ***Router***

React Router es una colección de componentes de navegación la cual podemos usar
tanto en web o en móvil con React Native. Con esta librearía vamos a obtener un enrutamiento
dinámico gracias a los componentes, en otras palabras tenemos unas rutas que renderizan un componente.

***Switch***

Este componente es el encargado de que solo se renderice el primer hijo Route o Redirect que coincide con la ubicación.
Si no usar este componente todos los componentes Route o Redirect se van a renderizar mientras cumplan con la condición establecida.

***Route***

Con Route podemos definir las rutas de nuestra aplicación, quizás sea el componente más importante de React Router
para llegar a comprender todo el manejo de esta librería. Cuando definimos una ruta con Route le indicamos
que componente debe renderizar.

Este componente cuanta con algunas propiedades.

***Path***: la ruta donde debemos renderizar nuestro componente podemos pasar un string o un array de string.

***Exact***: Solo vamos a mostrar nuestro componente cuando la ruta sea exacta. Ej: /home === /home.

***Strict***: Solo vamos a mostrar nuestro componente si al final de la ruta tiene un slash. Ej: /home/ === /home/

***Sensitive***: Si le pasamos true vamos a tener en cuenta las mayúsculas y las minúsculas de nuestras rutas. Ej: /Home === /Home

***Component***: Le pasamos un componente para renderizar solo cuando la ubicación coincide.
 En este caso el componente se monta y se desmonta no se actualiza.

***Render***: Le pasamos una función para montar el componente en línea.


https://johnserrano.co/blog/aprende-a-crear-rutas-con-react-router


**Ejemplo:**

```js
import React, { Suspense, lazy } from 'react';
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';

const Home = lazy(() => import('./routes/Home'));
const About = lazy(() => import('./routes/About'));

const App = () => (
  <Router>
    <Suspense fallback={<div>Loading...</div>}>
      <Switch>
        <Route exact path="/" component={Home}/>
        <Route path="/about" component={About}/>
      </Switch>
    </Suspense>
  </Router>
);
```

## . ***Propagación de propiedad ***


Esta es una característica de ES6, que también se usa en React. Mira el siguiente ejemplo:

Los llamados atributos de propagación que el nombre representa permiten expandir una expresión.

```js
var parts = ['two', 'three'];
var numbers = ['one', ...parts, 'four', 'five']; // ["one", "two", "three", "four", "five"]
```

//just assume we have an object like this:
```js
var person= {
    name: 'Alex',
    age: 35
}
```
Con propagación
```js
<Modal {...person} title='Modal heading' animation={false} />
```
es igual a
```js
<Modal name={person.name} age={person.age} title='Modal heading' animation={false} />
```


## . ***Estado con Hook***

Los Hooks son una nueva incorporación en React 16.8. Permiten usar estado y otras características de React sin escribir una clase.
Por ejempo Con Hook

```js
import React, { useState } from 'react';

function Example() {
  // Declaración de una variable de estado que llamaremos "count"
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

Por ejempo Sin Hook
Equivalente
```js
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }

  render() {
    return (
      <div>
        <p>You clicked {this.state.count} times</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Click me
        </button>
      </div>
    );
  }
}

```
