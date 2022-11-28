# Entity Relationship Diagrams

### Syntax

Entities and Relationships

Entity names are often capitalised, although there is no accepted standard on this, and it is not required in Mermaid.
Relationships between entities are represented by lines with end markers representing cardinality. Mermaid uses the most popular crow's foot notation. The crow's foot intuitively conveys the possibility of many instances of the entity that it connects to.

Crow's foot notation - represent entities as boxes, and relationships as lines between the boxes. Different shapes at the ends of these lines represent the relative cardinality of the relationship. These symbols are used in pairs to represent the four types of cardinality that an entity may have in a relationship.

These four types are:

- one-to-one.
- one-to-many.
- many-to-one.
- many-to-many.

Mermaid syntax for ER diagrams is compatible with PlantUML, with an extension to label the relationship. Each statement consists of the following parts:

```
  <first-entity> [<relationship> <second-entity> : <relationship-label>]

  CUSTOMER ||--o{ ORDER : places
```

- first-entity is the name of an entity. Names must begin with an alphabetic character and may also contain digits, hyphens, and underscores.
- relationship describes the way that both entities inter-relate. See below.
- second-entity is the name of the other entity.
- relationship-label describes the relationship from the perspective of the first entity.

### Relationship Syntax

Cardinality is a property that describes how many elements of another entity can be related to the entity in question. In each cardinality marker there are two characters. The outermost character represents a maximum value, and the innermost character represents a minimum value. The table below summarises possible cardinalities.

| Value (left)  | Value (right)   | Meaning                          |
| :------------ |:---------------:| -----:                           |
| l o           |   o l           | Zero or one                      |
| l l           | l l             |   Exactly one                    |
| }o            | o{              |    Zero or more (no upper limit) |
| } l           | l{              |    One or more (no upper limit)  |

### Attributes

Attributes can be defined for entities by specifying the entity name followed by a block containing multiple type name pairs, where a block is delimited by an opening { and a closing }. For example:

```
CAR ||--o{ NAMED-DRIVER : allows
    CAR {
        string registrationNumber
        string make
        string model
    }
    PERSON ||--o{ NAMED-DRIVER : is
    PERSON {
        string firstName
        string lastName
        int age
    }
```

### Attribute Keys and Comments

Attributes may also have a key or comment defined. Keys can be "PK" or "FK", for Primary Key or Foreign Key. And a comment is defined by double quotes at the end of an attribute. Comments themselves cannot have double-quote characters in them.

```
erDiagram
    CAR ||--o{ NAMED-DRIVER : allows
    CAR {
        string allowedDriver FK "The license of the allowed driver"
        string registrationNumber
        string make
        string model
    }
    PERSON ||--o{ NAMED-DRIVER : is
    PERSON {
        string driversLicense PK "The license #"
        string firstName
        string lastName
        int age
    }
```

Reference: https://mermaid-js.github.io/mermaid/#/entityRelationshipDiagram
