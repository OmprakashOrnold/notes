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
RAGHU SIR [NARESH I Technologies, Ameerpet, Hyderabad]
2 | P a g e
@GeneratedValue(strategy=GenerationType.TABLE)
@GeneratedValue(strategy=GenerationType.SEQUENCE,generator="sample")
@SequenceGenerator(name="sample",sequenceName="emp_seq")
@GeneratedValue(generator="sample")
@GenericGenerator(name="sample",strategy="com.app.model.MyGen")
@GenericGenerator(name="sample",strategy="native")//identity,hilo,increment

### DATE AND TIME:(java.util.DATE
* @Temporal(TemporalType.DATE)

   private Date dateOne;

* @Temporal(TemporalType.TIME)

  private Date dateTwo;

* @Temporal(TemporalType.TIMESTAMP)

  private Date dateThree;
