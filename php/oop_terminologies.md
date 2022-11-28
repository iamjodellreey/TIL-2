# PHP OOP - Interfaces

## Interfaces:

- An interface is a description of the actions that an object can do.
- Interfaces allow you to specify what methods a class should implement.
- Interfaces are declared with the interface keyword.

Syntax

```php
    <?php
    interface InterfaceName {
    public function someMethod1();
    public function someMethod2($name, $color);
    public function someMethod3() : string;
    }
    ?>
```

## PHP - Interfaces vs. Abstract Classes

Interface are similar to abstract classes. The difference between interfaces and abstract classes are:

- Interfaces cannot have properties, while abstract classes can
- All interface methods must be public, while abstract class methods is public or protected
- All methods in an interface are abstract, so they cannot be implemented in code and the abstract keyword is not necessary
- Classes can implement an interface while inheriting from another class at the same time

## Using interfaces

```php
<?php
interface Work {
  public function describeWork();
}

class Teacher implements Work {
  public function describeWork() {
    echo "Educating students at all levels";
  }
}

$work = new Teacher();
$work->displayWork();
?>
```

## Polymorphism

- When one or more classes use the same interface, it is referred to as "polymorphism".

```php
<?php
// Interface definition
interface Work {
  public function describeWork();
}

// Class definitions
class Teacher implements Work {
  public function describeWork() {
    echo "Educating students at all levels";
  }
}

class Programmer implements Work {
  public function describeWork() {
    echo "Write, modify, and test code and scripts that allow computer software and applications to function properly";
  }
}

class Doctor implements Work {
  public function describeWork() {
    echo "Maintain, promote, and restore health by studying, diagnosing, and treating injuries and diseases";
  }
}

// Create a list of works
$teacher = new Teacher();
$programmer = new Programmer();
$doctor = new Doctor();
$works = [$teacher, $programmer, $doctor ];

// Describe Works
foreach($works as $work) {
  $work->describeWork();
}
?>
```
