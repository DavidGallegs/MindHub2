# UNIDAD 1

## ESTRUCTURA COMPONENTES

Los componentes se crearán en la carpeta `src/components`
Y luego se importan en el archivo `App.tsx`

**Archivo App.tsx:**

~~~tsx
import Card from './components/Card'

function App() {

  return <Card/>
}

export default App;
~~~

**Componete:**

~~~tsx
function Card(){
    return (
        <div className="card">
            ...
        </div>  
    );
}

export default Card;
~~~

## ESTILOS COMPONENTES (MALA PRÁCTICA)

Los componentes en react pueden recibir valores en forma de variables
esto sirve para pasar información, datos o estilos usando `style={variable}`

~~~tsx
function Card(){

    const width = {
        width: '350px'
    }
    
    return (
        <div className="card" style={width}>
            ...
        </div>  
    );
}

export default Card;
~~~

En caso de que solo sea un estilo podemos hacerlo dentro de la misma etiqueta `style`

~~~tsx
function Card(){

    return (
        <div className="card" style={{width: "350px"}}>
            ...
        </div>  
    );
}

export default Card;
~~~

## FRAGMENTS

Para tener un componente escalable en el tiempo, podemos dividir su interior en `fragments`

~~~tsx
function Card(){
    
    return (
        <div className="card" style={{width: "350px"}}>
            <CardBody/>
        </div>  
    );
}

export function CardBody(){

    return (
        <>
            <h5 className="card-title">Card title</h5>
                <p className="card-text">
                    Some quick exameple text to build on the card title and make
                    up the bulk of the card's content.
                </p>
                <a href="#" className="btn btn-primary">Go somewhere</a>
        </>
    )
}
export default Card;
~~~

## PROPS

Para poder reutilizar los componentes utlizamos propiedades o `props`
