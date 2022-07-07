
## Extends vs Implements

| Features| Extends| Implements|
| --- | --- | --- |
| Implementation| The keyword extends is used when a class wants to inherit all the properties from another class or an interface that wants to inherit an interface.| We use the implements keyword when we want a class to implement an interface.|
| Method| The child class that extends a parent class may or may not override all the methods present in the parent cla| The class that implements an interface must define or provide the implementation of all the methods declared in the interface, or else the class should be declared as abstract.|
| Class| A subclass or more than one subclass can extend only one parent class at the same time.| A class can implement one or more than one interface at the same time.|
| Interface| 	An interface can extend any number of interfaces.| An interface can never implement any other interface.|