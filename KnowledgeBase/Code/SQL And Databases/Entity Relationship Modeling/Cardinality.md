[[Introduction to Entity Relationship Modeling]]

Cardinality defines the numerical relationship between two entities. It specifies the maximum number of instances of one entity that can be associated with a single instance of another entity. The most common cardinalities are:
- One-to-One (1:1): One instance of Entity A can be associated with at most one instance of Entity B, and vice versa.
- One-to-Many (1:N): One instance of Entity A can be associated with multiple instances of Entity B, but one instance of Entity B can be associated with only one instance of Entity A.
- Many-to-Many (M:N): Multiple instances of Entity A can be associated with multiple instances of Entity B, and vice versa.

In ER diagrams, cardinality is represented using a specific notation, such as a single line for one-to-one, a lite with an arrowhead for one-to-many, and a line with arrowhead at both ends for many-to-many relationships.

![[CardinalityVisualRepr.png]]