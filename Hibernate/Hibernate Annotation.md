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
* @ElementCollection @CollectionTable(name="emp_dtls", //table
joinColumns=@JoinColumn(name="eidFk")) //key col
* @Column(name="lst_data") //element col
private Set<String> details=new HashSet<String>(0);
