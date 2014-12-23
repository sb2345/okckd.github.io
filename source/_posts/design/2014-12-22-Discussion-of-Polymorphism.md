---
layout: post
title: "[Design] Discussion of Polymorphism (undone) "
comments: true
category: Design
tags: [  ]
---

### Polymorphism

Polymorphism is to use common interface instead of concrete implementation while coding. The most common use of polymorphism in OOP occurs when a parent class reference is used to refer to a child class object.

http://www.ntu.edu.sg/home/ehchua/programming/java/J3b_OOPInheritancePolymorphism.html

http://javarevisited.blogspot.sg/2011/08/what-is-polymorphism-in-java-example.html

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
