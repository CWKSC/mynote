## ER to Relation Model
1. Strong Entity to Relation (Table), Attribute to be Column Header, Key attribute to be primary key, non-simple attribute don't need to convert in this step
2. Weak Entity to Relation (Table) as same as step 1, add primary key attribute of owner as foreign key to column
3. Convert 1 : 1 relationship by Foreign key approach, Merged relationship approach, "Cross reference or relationship relation approach"
4. Convert 1 : N relationship by Foreign key approach or "Cross reference or relationship relation approach" 
5. Convert M : N relationship by "Cross reference or relationship relation approach"
6. Convert N-ary relationship by "Cross reference or relationship relation approach"
7. Convert Multivalue attributes by "Cross reference or relationship relation approach"

## Mapping Algorithm
- Foreign key approach
- Merged relationship approach
- Cross reference or relationship relation approach

## Foreign key approach
Choose primary key in one of them and reference it in another entity (Foreign key)
It prefer the key of entity of total participation to be the chosen key (since avoid Null value)
if it is one to many relationship, we can only add the Foreign key to many side (chosen primary key in one side)
Foreign key approach cannot convert many-to-many relationship 

## Merged relationship approach
Merge two relation to be one relation by combining attribute
It require both total participation 
(since this led every tuple in entity corresponding tuple in another entity)
This method is not commonly used

## Cross reference or relationship relation approach
Build a new relation include two foreign key refer to two primary key of entity respectively
In N-ary relationship, include N foreign key refer to N primary key respectively
If relationship contain simple attribute, it will also include to the new relation as one attribute
In Multivalue attributes, include Multivalue attributes to the new relation, and  also include one foreign key refer to the primary key of the own of Multivalue attributes
If  Multivalue attributes is composite, include all it simple components
Mainly use for convert many-to-many, N-ary relationship and  Multivalue attributes 

## Other 
Foreign key refer to primary at same table called self reference
In diagram, be point by arrow one is primary key, the line start from column is foreign key
the double line diamond is indicate the Identify relationship that is between weak entity and strong entity
In relation model, all tuple in the relation must be distinct

## See Other
https://medium.com/omarelgabrys-blog/database-modeling-logical-design-part-6-af029e93cc1f
https://cs.uwaterloo.ca/~tozsu/courses/CS338/lectures/12%20ER%20to%20Rel.pdf

## Integrity Constraints
Relational model contain a set of Integrity Constraints, called IC
It determine which values are permissible (allow) and which are not
All tuple in database should satisfy all Integrity Constraints
If satisfy all, called Valid state, otherwise called Invalid state

## Three main types of constraints
- Inherent or Implicit Constraints
- Schema-based or Explicit Constraints
- Application-based or Semantic constraints

## Inherent or Implicit Constraints
Based on data model itself
No matter how you define database model, this constraint always exist
E.g. not allow multiple value 

## Schema-based or Explicit Constraints
Depends on how you define schema
E.g. cardinality ratio constraint

## Application-based or Semantic constraints
Specified by application program

## Four main type of Schema-based or Explicit Constraints
- Domain constraints
- Key constraints
- Entity integrity constraints
- Referential integrity constraints

## Domain constraints
Every value in tuple must be atomic value from domain
It allow null value
E.g. integer, float, character, string, real number

## Key constraints
Superkey, is a subset of attribute, uniquely identify tuple
No two tuple have same value of Superkey
Every relation at least have one default Superkey, that Superkey is set of all attributes
Since in relation model, all tuple in the relation must be distinct

Candidate Key, or just called Key
Candidate Key is definitely a Supekey
It is minimal Superkey, if we remove any attribute of it, it will not be Superkey
If relation has several Candidate Key, one will chosen as primary key

## Entity integrity constraints
No primary key value can be null value
t[PK] != null, for any tuple t of R, R is Relation, PK is primary key

## Referential integrity constraints
At foreign key, R1 -> R2,  for R1, R2 both relation
R1 called referncing relation, R2 called referenced relation
Tuples in R1 have attributes FK (foreign key) that reference to primary key attribute PK of R2
FK and PK have same domain
Value in R1 must refer to some existing value in R2, it should not refer to something which does not exist
Value in R1 allow null value