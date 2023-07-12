# Sistema Academia - Microservicios - SpringBooot

## Principio de Responsabilidad Única

_Este principio establece que un componente o clase debe tener una responsabilidad única, sencilla y concreta. Esto simplifica el código al evitar que existan clases que cumplan con múltiples funciones, las cuales son difíciles de memorizar y muchas veces significan una pérdida de tiempo buscando qué parte del código hace qué función._

### ¿Dónde está presente en el código?


## Principio Abierto/Cerrado

_Este principio establece que los componentes del software deben estar abiertos para extender a partir de ellos, pero cerrados para evitar que se modifiquen._

### ¿Dónde está presente en el código?

En el proyecto se estuvo trabajando con los paquetes *_Repository_*, los cuales contienen clases con interfaces que nos otorgan funcionalidades como la capacidad de realizar operaciones con la base de datos, dado que extendemos de clases de _Jpa_, pero si prestamos atención podemos ver que se pueden agregar métodos distintos a la clase original sin afectarla, lo cual indica que se cumple este principio.

```java
public interface KardexRepository extends JpaRepository<Kardex, Long> {
    List<Kardex> findAllByAlumno_Matricula(String matricula);
}
```
## Principio de Substitución de Liskov

_Este principio establece que una subclase puede ser sustituida por su superclase. Es decir, podemos crear una subclase llamada Auto, la cual deriva de la superclase Vehículo.  Si al usar la superclase el programa falla, este principio no se cumple._

### ¿Dónde está presente en el código?



## Principio de Segregación de Interfaz

_Este principio establece que los clientes no deben ser forzados a depender de interfaces que no utilizan. Es importante que cada clase implemente las interfaces que va a utilizar. De este modo, agregar nuevas funcionalidades o modificar las existentes será más fácil._

### ¿Dónde está presente en el código?

## Principio de Inversión de Dependencias

_Este principio establece que los módulos de alto nivel no deben de depender de los de bajo nivel. En ambos casos deben depender de las abstracciones. Alto nivel se refiere a operaciones cuya naturaleza es más amplia o abarca un contexto más general y bajo nivel son componentes individuales más específicos._

### ¿Dónde está presente en el código?

## Referencias

Visitar la página [Kata Software](https://kata-software.com/es/publicaciones/principios-solid-en-programacion).

