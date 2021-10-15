# React

## Estados y Ciclo de vida 

***State***

El estado puede ser un objeto (Por lo regular es un JSON) o variable.
Podemos utilizarlo para realizar cambios desde dentro de los componentes.

El state son los valores internos que manejan la lógica y los datos de un componente, permite que éste reaccione a cualquier cambio lo que hará que se vuelva a renderizar en la interfaz.

***Uso del state en componentes de clases (class component)***

Para acceder y manipular el estado dentro de un componente de clase debemos hacer uso de this.
 

***Inicializando el state de un componente de clase**
Podemos declarar el estado de la siguiente forma dentro del constructor de la clase

```js
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
```

***Modificar el state de un componente de clase***

La manera correcta de actualizar y manipular el estado en este tipo de componentes es a través de setState, por ejemplo:

```js
class Hijo1 extends React.Component{
    ...
  aumentar=()=>{
    this.setState({
      cuenta:this.state.cuenta + 1
    });
  }
    ...
}
```

***¿Qué son los métodos de ciclos de vida?***

Son métodos que se ejecutan automáticamente en un Componente de Clase, ocurren en 3 fases:

1. Creación del componente .
2. Actualización.
3. Destrucción del componente

1.Estos métodos se ejecutan cuando se crea un componente y se inserta en el árbol del DOM.

constructor(): Se ejecuta al crear la instancia del componente, en el constructor puedes inicializar el estado y enlazar manejadores de eventos.
render(): Es el único método requerido, cuando se ejecuta, examina el estado y las propiedades y dibuja el componente en el árbol del DOM.
componentDidMount(): Se invoca inmediatamente después de que un componente se ha insertado al árbol del DOM. Es útil para ejecutar suscripciones o peticiones asíncronas a API's, bases de datos, servicios, etc.

2.Estos métodos son ejecutados por cambios en el estado o las propiedades de los componentes.

render(): redibuja el componente cuando detecta cambios en el estado o las propiedades del componente.
componentDidUpdate(): Se ejecuta inmediatamente después de que la actualización del estado o las propiedades sucede, al igual que componenDidUpdate es un método ideal para hacer peticiones externas.

3.Estos métodos son ejecutados una vez que el componente ha sido eliminado del árbol del DOM.
componentWillUnmount(): Se ejecuta antes de destruir el componente del árbol del DOM, es un método útil para hacer tareas de limpieza.


***componentDidMount()***

En el momento que tu componente ya se creo, es cuando este metodo empieza a ejecutarse.
En este método se suele poner las llamadas a la api en el caso de que lo necesitaras.

Ejemplo:
```js
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
```
***componentDidUpdate()***

Este ciclo se invoca tan pronto como la actualizacion ocurre.
Se suele usar para actualizar el DOM con los datos de tu state.

Ejemplo de uso:
```js
componentDidUpdate(previasProps, previoState) {
        if (this.props.input == previasProps.input) {
          // Llamar a una funcion o hacer peticiones ajax
        }
}
```
***componentWillUnmount()***

Como el nombre suguiere, este metodo se llamara justo antes de que sea destruido.
Se suele utilizar para limpieza (cerrar peticiones ajax, timeouts, eliminar Eventos… )

Ejemplo de uso:
```js
componentWillUnmount() {
      document.removeEventListener("click", funcionAsignada);      
}
```

![image](https://user-images.githubusercontent.com/6796155/137124077-0bc9e1b8-f9f9-4fd4-b6b5-44ccf92221e5.png)


## ***Puerto por Defecto***

Cuando creamos un proyecto de React. JS con la plantilla, por defecto se ejecutará en el puerto 3000

## ***Router***

React Router es una colección de componentes de navegación la cual podemos usar tanto en web o en móvil con React Native. Con esta librearía vamos a obtener un enrutamiento
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

***Propagación de propiedad***


Esta es una característica de ES6, que también se usa en React. Mira el siguiente ejemplo:

Los llamados atributos de propagación permiten expandir una expresión.

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

***Constructor Más definiciones***

El estado de nuestro componente en el constructor se define así:
```js
constructor (props) {
    super(props);
    this.state = {
        propiedad: 'Algún valor'
    }
}
```
Si no se define ningún estado en el constructor, entonces no lo necesita.


Se tendra que enlazar la referencia de la instancia de nuestro componente a los métodos que son utilizados en el método render() y que normalmente son los manejadores de eventos:
```js
class Padre extends React.Component {
    constructor (props) {
        super(props);
        this.state = { src: '' }
        this.cambiarAnimal = this.cambiarAnimal.bind(this);
    }
    
    cambiarAnimal () {
        this.setState({
            src: 'Algúna url que apunte a una imagen de un animal' 
        });
    }
    
    render() {
        return (
          <div>
            <Animal src={this.state.src}/>
            <button onClick={this.cambiarAnimal}>Cambiar animal</button>
          </div>
        );
    }
}
```
Ahora el método this.cambiarAnimal podrá acceder a la instancia de nuestro componente a través de this y así utilizar this.setState() para cambiar el estado.

Existe otra opción para utilizar métodos de nuestra clase como manejadores de eventos, con el uso de funciones flecha (arrow functions).
```js
class Padre extends React.Component {
    constructor (props) {
        super(props);
        this.state = { src: '' }
    }
    
    cambiarAnimal = () => {
        this.setState({
            src: 'Algúna url que apunte a una imagen de un animal' 
        });
    }
    
    render() {
        return (
          <div>
            <Animal src={this.state.src}/>
            <button onClick={this.cambiarAnimal}>Cambiar animal</button>
          </div>
        );
    }
}

```
