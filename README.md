# Sistema Academia - Microservicios - SpringBooot

## Principio de Responsabilidad Única

_Este principio establece que un componente o clase debe tener una responsabilidad única, sencilla y concreta. Esto simplifica el código al evitar que existan clases que cumplan con múltiples funciones, las cuales son difíciles de memorizar y muchas veces significan una pérdida de tiempo buscando qué parte del código hace qué función._

### ¿Dónde está presente en el código?

En el proyecto, este principio está presente en muchas partes, desde su estructura de carpetas (paquetes) hasta las clases contenidas en dichas carpetas. Por ejemplo, el paquete ```entity``` tiene la responsabilidad de almacenar las clases que definan los modelos que se vayan a utilizar, tal cual lo hace la clase ```Alumno```.


```java
@Entity
@Table (name = "alumnos")
@Data
@NoArgsConstructor
public class Alumno {
    @Id
    @Column(name = "id")
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long id;
    @Column(name ="matricula")
    private String matricula;
    private String nombre;
    private String apellidos;
    private LocalDate edad;
    @Column(name = "sexo", precision = 1, length = 1)
    private char sexo;
    @Column(name = "licenciatura_id")
    private Long licenciaturaId;
    @OneToMany(fetch = FetchType.LAZY, mappedBy = "alumno")
    private List<Kardex> kardexs;

}

```

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

En el proyecto podemos visualizar el cumplimiento de este principio SOLID al utilizar la anotación ```@Autowired```, dado que esta sirve para la inyección de dependencias. 
En el código siguiente, la etiqueta ```@Autowired``` se utiliza pra inyectar dependencias de dos servicios, _KardexService_ y _alumnoService_, al hacerlo nos evitamos el crear instancias de los servicios, pues Spring se encarga de crearlas por nosotros, de modo que nuestro controlador 'AlumnoController' depende de las abstracciones de dichos servicios y no necesita conocer como se implementan, sino solo necesita saber como interactuar con dichas abstracciones.
```java

@RestController
@RequestMapping(value = "/alumno")
@Log4j2
public class AlumnoController {
    @Autowired
    private AlumnoService alumnoService;

    @Autowired
    KardexService kardexService;

    @GetMapping
    public List<Alumno> getAllAlumnos() {
        return alumnoService.getAllAlumnos();
    }

    @PostMapping
    public Alumno createAlumno(@RequestBody Alumno alumno){
        log.info("Alumno  a guardar: "+alumno.toString());
        return alumnoService.createAlumno(alumno);
    }

    @PutMapping
    public Alumno updateAlumno(@RequestBody Alumno alumno) {
        log.info("Alumno a actualizar :"+alumno.toString());
        return alumnoService.updateAlumno(alumno);
    }

    @DeleteMapping("/{id}")
    public void deletealumno(@PathVariable (value = "id") Long id){
         alumnoService.deleteAlumno(id);
    }
}

```
## Referencias

Visitar la página [Kata Software](https://kata-software.com/es/publicaciones/principios-solid-en-programacion).

