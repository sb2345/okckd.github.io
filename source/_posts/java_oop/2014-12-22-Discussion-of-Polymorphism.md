---
layout: post
title: "[Java OOP] Discussion of Polymorphism "
comments: true
category: Java OOP

---

### Polymorphism

Polymorphism is to [use common interface](http://javarevisited.blogspot.sg/2011/08/what-is-polymorphism-in-java-example.html) instead of concrete implementation while coding. 

When we program for interface our code is capable of handling any new requirement or enhancement arise in near future due to new implementation of our common interface. If we don't use common interface and rely on concrete implementation, we always need to change and duplicate most of our code to support new implementation. 

The most common use of polymorphism in OOP occurs when a parent class reference is used to refer to a child class object.

### Example 

Example of Bicycle class given on [official oracle website](http://docs.oracle.com/javase/tutorial/java/IandI/polymorphism.html): 

    public class Bicycle{
        public void printDescription(){
            System.out.println("\nBike is " + "in gear " + this.gear
                + " with a cadence of " + this.cadence +
                " and travelling at a speed of " + this.speed + ". ");
        }
    }

    public class MountainBike extends Bicycle {
        private String suspension;

        public void printDescription() {
            super.printDescription();
            System.out.println("The " + "MountainBike has a" +
                getSuspension() + " suspension.");
        }
    }

    public class RoadBike extends Bicycle{
        private int tireWidth;

        public void printDescription(){
            super.printDescription();
            System.out.println("The RoadBike" + " has " + getTireWidth() +
                " MM tires.");
        }
    }

    public class TestBikes {
        public static void main(String[] args){
            Bicycle bike01, bike02, bike03;

            bike01 = new Bicycle(20, 10, 1);
            bike02 = new MountainBike(20, 10, 5, "Dual");
            bike03 = new RoadBike(40, 20, 8, 23);

            bike01.printDescription();
            bike02.printDescription();
            bike03.printDescription();
        }
    }

The output: 

    Bike is in gear 1 with a cadence of 20 and travelling at a speed of 10. 

    Bike is in gear 5 with a cadence of 20 and travelling at a speed of 10. 
    The MountainBike has a Dual suspension.

    Bike is in gear 8 with a cadence of 40 and travelling at a speed of 20. 
    The RoadBike has 23 MM tires.

Referring to the same page, __JVM calls the appropriate method for the object that is referred to in each variable__. It does not call the method that is defined by the variable's type. 

### Another example

Cylinder is a subclass of Circle. We can say that Cylinder "is-a" Circle.

We can create an instance of Cylinder, and assign it to a Circle reference: 

> Circle c1 = new Cylinder();

You can invoke all the methods defined in the Circle class, but __you cannot invoke methods defined in the Cylinder class__. c1 is a reference to the Circle class, which does not know about the methods defined in the subclass Cylinder.

__The reference c1, however, retains its internal identity__. Since Cylinder overrides getArea() method, calling c1.getArea() will invokes the overridden version defined in subclass Cylinder, instead of in Circle. This is because c1 is holding a Cylinder object internally.

The code is below: 

    public class PolymorphismSubstitutabilityDemo {

        public static void main(String[] args) {
            Circle c1 = new Cylinder(1, "white", 10);
            System.out.println(c1.getClass());
            System.out.println(c1.getRadius());
            System.out.println(c1.getColor());
            System.out.println(c1.getArea());
        }
    }

    class Circle {
        int radius;
        String color;

        public Circle(int a, String b) {
            this.radius = a;
            this.color = b;
        }

        public int getRadius() {
            return radius;
        }

        public String getColor() {
            return color;
        }

        public double getArea() {
            return 3.14159 * Math.pow(radius, 2);
        }
    }

    class Cylinder extends Circle {
        int height;

        public Cylinder(int a, String b, int c) {
            super(a, b);
            this.height = c;
        }

        public int getHeight() {
            return height;
        }

        public double getArea() {
            return super.getArea() * height;
        }
    }

The output of execution: 

    class Cylinder
    1
    white
    31.4159

### Summary: 

[ref](http://www.ntu.edu.sg/home/ehchua/programming/java/J3b_OOPInheritancePolymorphism.html)

1. A subclass instance can be assigned (substituted) to a superclass' reference.

1. Once substituted, we can invoke methods defined in the superclass; we cannot invoke methods defined in the subclass.

1. However, if the subclass overrides inherited methods from the superclass, the subclass (overridden) versions will be invoked.
