
# JMoordb-core

Framework Java para bases de datos NoSQL


[Libro jmoordb-core](http://leanpub.com/jmoordbcore)

Este proyecto utiliza  como base
[jmoordb-core-processor-genesis](https://github.com/avbravo/jmoordb-core-processor-genesis.git)


Ejemplo

Defina una entidad

```java
Entity(jakartaSource = JakartaSource.JAVAEE_LEGACY)
public class Pais {
    @Id(strategy = GenerationType.AUTO)
    private Long idpais;
    @Column
    private String pais;
    
    @Column
    private Date fecha;

    public Pais() {
    }

````

Cree una interface Repository

```java
@Repository(entity = Pais.class, jakartaSource = JakartaSource.JAVAEE_LEGACY)
public interface PaisRepository extends CrudRepository<Pais, Long> {

@Find
    public Stream<Pais> findByNombreAndApellidoAndEdadLessThanEquals(String nombre, String apellido, Integer edad);
    
    @Query(where = "fecha .eq. @fecha")
    public List<Pais> queryByFecha(@IncludeTime Date fecha);
    
    @Find
    public List<Pais> findByIdpaisGreaterThanPagination(Long idpais,Pagination pagination);
    

    @Find
    public List<Pais> findByFecha(@IncludeTime Date fecha);

    @Find
    public List<Pais> findByFecha(@ExcludeTime LocalDateTime fecha);

    @Find
    public List<Pais> findByFechaGreaterThan(Date fecha);

    @Find
    public List<Pais> findByFechaGreaterThanEquals(@ExcludeTime Date fecha);

    @Find
    public List<Pais> findByFechaLessThan(@ExcludeTime Date fecha);

    @Find
    public List<Pais> findByFechaLessThanEquals(@ExcludeTime Date fecha);

    @Find
    public Optional<Pais> findByFechaAndPais(@ExcludeTime Date fecha, String pais);

    @Find
    public List<Pais> findByFechaLessThanAndPais(@ExcludeTime Date fecha, String pais);

    @Find
    public List<Pais> findByPaisAndFechaLessThan(@ExcludeTime Date fecha, String pais);

////    
//    
    @Find
    public List<Pais> findByLocal(@ExcludeTime LocalDateTime local);
//    

    @CountBy
    public Long countByLocal(LocalDateTime local);

   
    @Find
    public List<Pais> findByFechaGreaterThanEqualsAndFechaLessThanEquals(@IncludeTime Date start, Date end);


    @Find
    public List<Pais> findByFechaGreaterThanEqualAndFechaLessThanEqual(@ExcludeTime Date start, @ExcludeTime Date end);

    @Find
    public List<Pais> findByFechaGreaterThanEqualAndFechaLessThanEqualAndPais(@ExcludeTime Date start, @ExcludeTime Date end, String pais);

    @DeleteBy
    public Long deleteByFechaGreaterThan(Date fecha);

    @Ping
    pubblic Boolean ping();
}


````
