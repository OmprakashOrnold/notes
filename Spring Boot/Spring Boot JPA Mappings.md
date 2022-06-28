
## Association Mapping in JPA (HAS-A) with multiplicity (1...1/1... * / * ...1/ * ... * )

* Creating Relation between two tables, by using PrimaryKey(PK)-ForeignKey(FK) Concept
* One Table PK is taken as another table FK to create link b/w table using any multiplicity
* 1...* (meaning) = 1 row in one table are connected to many rows in another table
### Real Time Example
* 1...1 : Person --- VoterId/PanCard/Aadhar
* 1...* : Person -- BankAccount
* 1...* (and) *...1 = *...*Book --- Author
**Note:**
Incase of tables link using multiplicity, create FK Column(Extra Column)
   at many side (* side)  [for 1...  *  / * ...1]
### Non-Collection	
* 1...1 
* *...1                                     
### Collection	
* *...1  
* *...1      

## Association Mapping Implementation Steps:-

*  Apply HAS-A Relation between classes
*  Check for Collection Type (or not?), 
    if it is Collection then modify HAS-A variable as Collection variable.
*  Apply multiplicity Annotation at HAS-A Variable
  1...1     @ManyToOne  (unique condition)
  *...1     @ManyToOne
  1...*     @OneToMany
  *...*     @ManyToMany

*  Apply JoinColumn (or) JoinTable at HAS-A Variable level
           
Code should be at parent model class (HAS-A variable level) only for any multiplicity

![](https://i.postimg.cc/m2G118cK/Spring-Boot7-AM-16102020.png)                                                                    