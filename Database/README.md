## Participation constraint 

  - total participation
  - partial participation

Total participation by double line

Partial participation by single line

Cardinality constraints define maximum number of relationship instances

Participation constraint define minimum number of relationship instances

Partial participation -> minimum = 0

Total participation -> minimum = 1

(min, max) notation can indicate Cardinality constraints and Participation constraint at the same time

E1, E2 is Entity, R is Relationship

E1 ----- (min1, max1) ------ R ----- (min2, max2) ----- E2

E1 R (min, max) E2

E2 R (min, max) E1

Employee ----- (1, 1) ----- Work for ----- (1, N) ----- Department

Employee Work for (1, 1) E2

Department (be) Work for (1, N) Employee

## See Other

實體關係模型(Entity-relationship model)
https://www.mysql.tw/2013/03/entity-relationship-model.html

CH02 實體關係模式--基本概念 - PostgreSQL 中文-Mammoth
http://postgresql.wisdomfish.org/zi-liao-ku-de-he-xin-li-lun-yu-shi-wu/ch02-shi-ti-guan-xi-mo-shi-ji-ben-gai-nian

Partial keys 
https://www.geeksforgeeks.org/partial-unique-secondary-composite-and-surrogate-keys-in-dbms/

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

if it is one to many relationship, we can only add Foreign key to many side (chosen primary key in one side)

(Since column be point by Foreign key must be primary key, primary key must unique value and no repeat, so start point of Foreign key must add on many side)

For example, employee work for one department, department (be) work for many employee

Now employee is many side, we add Foreign key to employee, it means one column of employee table point to department primary key

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

If Multivalue attributes is composite, include all it simple components

Mainly use for convert many-to-many, N-ary relationship and  Multivalue attributes 

## Other 
Foreign key refer to primary at same table called self reference

In diagram, be point by arrow one is primary key, the line start from column is foreign key

the double line diamond is indicate the Identify relationship that is between weak entity and strong entity

In relation model, all tuple in the relation must be distinct

## See Other
Database — Design: Logical Design (Part 6) | by Omar Elgabry | OmarElgabry's Blog | Medium
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

## Operations on Relations
Insert, Modify, Delete

Integrity constraints should not violated by those operation

Note that Insert and Modify Violation is so common sense

Delete Violation need to be more care or remember

## Insert Violation
Domain constraint: insert value not in domain, e.g put string into int

Key constraint: the insert key value already exist in relation

Entity integrity: value of primary key in inset tuple is null

Referential integrity: insert foreign key value not exist in reference relation

## Modify Violation
Domain constraint: modify value not in domain, e.g put string into int

Key constraint: the modify key value already exist in relation

Entity integrity: value of primary key in modify tuple is null

Referential integrity: modify foreign key value not exist in reference relation

## Delete Violation
Only violate Referential integrity constraint

Primary key value of tuple be deleted, and this refer from other tuple

## Prevent Violation of Integrity constraints
Several action can be taken:
- Cancel operation
- Continue operation but info user of violation 
- Correct violation operation, by Trigger addition update, e.g. Cascade deletion, delete tuple and reference tuple delete too
- Run User specified error correction routine

## Functional Dependency
Denote X -> Y, Constraint between two attribute set in relation

X depend Y, Y determine X

t1[X] = t2[X], t1[Y]  = t2[Y],  for t1, t2 is tuple of relation

value of Y of tuple depend on value of X of the tuple

e.g city -> country

## Formal definition of Functional Dependency
Let R be relation schema, α ⊆ R, β ⊆ R (α and β are sets of R's attribute), we say

α -> β

In any legal relation instance r(R), for all tuple t1 and t2 in r, we have

t1[α] = t2[α] => t1[β]  = t2[β]

## Usage of Functional Dependency
- Set constraints on relation (e.g define key constraint)
- Test relation under given set of Functional Dependency
- Test goodness of database schema design (nomalization)

## Define key constraints by Functional Dependency
Set of attribute {A1, A2, ..., An} 

Superkey definition: attributes functionally determine all other attributes of relation

Minimal: No proper subset functionally determine all other attributes of relation

Then it is candidate key

## Properties of Functional Dependency
If X -> Y, then Y not -> X

If X -> Y, then XZ -> Y

Trivial: A -> A,  AB -> A  always true

## Inference Rule for Functional Dependency
Armstrong's inferemce rules:
- Reflexive: If Y subset of X, then X -> Y
- Augmentation: If X -> Y, then XZ -> YZ
- Transitive: If X -> Y and Y -> Z, then X -> Z
- Decomposition: If X -> YZ, then X -> Y and X -> Z
- Union: If X -> Y and X -> Z, then X -> YZ
- Pseudotransitivity: If X -> Y and WY -> Z, then WX -> Z

## Prove of Union rules
(1) X -> Y (Given)

(2) X -> Z (Given)

(3) XX -> XY => X -> XY (Augmentation rule by (1))

(4) XY -> YZ (Augmentation rule by (2))

(5) X -> YZ (Transitive rule by (3) and (4))

## Closure
Closure of set F of Functional Dependency is set F+ of all Functional Dependency than can be inferred from F

Closure of set of attributes X with respect to F is the set X+ of all attributes the are functionally determined by X

If X+ consists all attribute, X is superkey

If every Functional Dependency in G also in F+, that said Functional Dependency F cover G

## Equivalence of sets of  Functional Dependency
Set F of Functional Dependency cover another set of Functional Dependency G

if every Functional Dependency in G is also in F+ (in F Closure) (F cover G)

Two sets of Functional Dependency F and G are equivalent if:

- Every Functional Dependency in F can inferred from G
- Every Functional Dependency in F can inferred from F
- F and G are equivalent if F+ = G+  (Closure is Equivalence)
E.g.  F: A -> BC,   G: A -> B, A -> C,   F+ = G+

## Normalization

### First normal form (1NF)

- All tuple unique
- No composite or multivalued attribute (Atomic)

### Second Normal Form (2NF)

- No partial functional dependency
- All column must full functional dependency to primary key

### Third Normal Form (3NF)

- No transitive functional dependency

### Boyce-Codd Normal Form (BCNF)

- Primary Key with only one column 