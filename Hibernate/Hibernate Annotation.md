## Hibernate Annotation
### BASIC ANNOTATIONS:
* @Entity
* @Table(name="empt_tab")
* @Id
* @Column(name="eid")

### PRIMARY KEY GENERATOR
* @GeneratedValue 
* @GeneratedValue(strategy=GenerationType.AUTO)
* @GeneratedValue(strategy=GenerationType.IDENTITY)
* @GeneratedValue(strategy=GenerationType.SEQUENCE) 
* @GeneratedValue(strategy=GenerationType.TABLE)

* @GeneratedValue(strategy=GenerationType.SEQUENCE,generator="sample")
* @SequenceGenerator(name="sample",sequenceName="emp_seq")
* @GeneratedValue(generator="sample")
* @GenericGenerator(name="sample",strategy="com.app.model.MyGen")
* @GenericGenerator(name="sample",strategy="native")//identity,hilo,increment
* @GeneratedValue(strategy=GenerationType.TABLE)
* @GeneratedValue(strategy=GenerationType.SEQUENCE,generator="sample")
* @SequenceGenerator(name="sample",sequenceName="emp_seq")
* @GeneratedValue(generator="sample")
* @GenericGenerator(name="sample",strategy="com.app.model.MyGen")
* @GenericGenerator(name="sample",strategy="native")//identity,hilo,increment

### DATE AND TIME:(java.util.DATE
* @Temporal(TemporalType.DATE)

   private Date dateOne;

* @Temporal(TemporalType.TIME)

  private Date dateTwo;

* @Temporal(TemporalType.TIMESTAMP)

  private Date dateThree;


### BLOB and CLOB
* @Lob

  private byte[] image;

* @Lob

  private char[] doc

### VERSION OF OBJECT:
* @Version

  private int ver1;
* @Version

  private Date ver2  ;


### LIST, SET AND MAP WITH PRIMITIVES:
* @ElementCollection  
* @CollectionTable(name="emp_dtls", //table

  joinColumns=@JoinColumn(name="eidFk")) //key col

* @Column(name="lst_data") //element col

 **private Set<String> details=new HashSet<String>(0);**


* @ElementCollection 
* @CollectionTable(name="emp_data", //table

  joinColumns=@JoinColumn(name="eidFk"))        //key col
* @OrderColumn(name="pos") //index col
* @Column(name="prjs") //element col

**private List<String> data=new ArrayList<String>(0);**

* @ElementCollection *
* @CollectionTable(name="emp_models", //table

  joinColumns=@JoinColumn(name="eidFk")) //key col

* @MapKeyColumn(name="pos") //index col
* @Column(name="model_data") //element col

**private Map<Integer,String> models=new HashMap<Integer, String>();**


### COMPONENT MAPPING:
```java 
@Embeddable 
public class Address{
      @Column(name="hno")
      private int hno;
      @Column(name="loc")
      private String loc;
}
```
```java 
@Entity
class Employee {
     @Embedded
     @AttributeOverrides({
     @AttributeOverride(name="hno",column=@Column(name="hno")),
     @AttributeOverride(name="loc",column=@Column(name="location"))
      })
      private Address addr=new Address();
}
```


### Hibernate BootStrap class:-
```java
import java.util.Properties;
import org.hibernate.SessionFactory;
import org.hibernate.boot.registry.StandardServiceRegistry;
import org.hibernate.boot.registry.StandardServiceRegistryBuilder;
import org.hibernate.cfg.Configuration;
import org.hibernate.cfg.Environment;
import in.nit.model.Employee;
public class HibernateUtil {
    private static SessionFactory sf=null;
    static {
        try {
          //1. Properties object using Environment
          Properties p=new Properties();
          p.put(Environment.DRIVER, "com.mysql.jdbc.Driver");
          p.put(Environment.URL,"jdbc:mysql://localhost:3306/hibernate");
          p.put(Environment.USER, "root");
          p.put(Environment.PASS, "root");
          p.put(Environment.DIALECT, "org.hibernate.dialect.MySQL55Dialect");
          p.put(Environment.SHOW_SQL, true);
          p.put(Environment.FORMAT_SQL,true);
          p.put(Environment.HBM2DDL_AUTO,"update");
          //2. Convert into Hibernate Object format
          Configuration cfg=new Configuration();
          //3. Load Properties into Configuration
          cfg.setProperties(p);
          //4. Provide entity details to cfg
          cfg.addAnnotatedClass(Employee.class);
          //cfg.addAnnotatedClass(Employee.class);
          //5. ServiceRegistery
          StandardServiceRegistry register=new StandardServiceRegistryBuilder()
                                             .applySettings(cfg.getProperties())
                                             .build();
          //6. SessionFactory
          sf=cfg.buildSessionFactory(register);
          } catch (Exception e) {
          e.printStackTrace();
       }
}
public static SessionFactory getSf() {
         return sf;
     }
}

```
