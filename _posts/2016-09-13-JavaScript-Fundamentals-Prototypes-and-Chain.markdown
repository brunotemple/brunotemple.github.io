---
layout: post
title: JavaScript Fundamentals - Prototypes and Chain.
categories: [JavaScript Fundamentals]
tags: [JavaScript, Prototypes]
date: 2016-09-13
---

### Prototype concept.

JavaScript’s prototypes can be a little bit confused, when I started to study JavaScript, I struggled with this concept. After a while studying and training, I could understand. I believe it’s crucial to understand this concept. Actually, now I think isn’t so complex. What we need to know is:
A prototype is an object, and all objects inherit methods and properties from a prototype.

#### Objects.
It’s easy, but, what is an object in JavaScript?
An object is an unordered list of primitives (String, Number, Boolean, Undefined, and Null). 
A simple example can be a car. 
As an object, a car has a list of primitives that we called properties.

		Object Car =>
			brand: Nissan
			model: Skyline
			color: Blue
			
Also, the Object Car can has methods, when there is a function defined for a property. Such as: Car.turnLeft(), Car.turnRight() , Car.stop()

#### Back to prototypes.
When we create a prototype, we define the properties and method when we use this prototype to create a new object. Let’s see a sample:  

The function below is our prototype:

		function Car(brand, model, color) {
			this.brand = brand;
			this.model = model;
			this.color = color;
		}


When I create a new object using that prototype, the new object will inherit all the properties from the Car prototype.

		var dreamCar = new Car(“Nissan”,”Skyline”,”Blue”); 

		console.log(dreamCar.brand); // Nissan

Going further.

		function Car(brand, model, color) {
			this.brand = brand;
			this.model = model;
			this.color = color;
		}

		var dreamCar = new Car("Nissan","Skyline","Blue"); 

		Car.prototype.fuel = "Petrol";
		console.log(dreamCar.fuel); // Petrol

		Car.prototype.fuel = "Diesel";
		console.log(dreamCar.fuel); // Diesel
		console.log(Car.prototype.fuel); // Diesel
		
		dreamCar.fuel = "Electricity";
		console.log(dreamCar.fuel); // Electricity
		console.log(Car.prototype.fuel); // Diesel
		
		Car.prototype.fuel = "Gas";
		console.log(dreamCar.fuel); // Electricity
		console.log(Car.prototype.fuel); // Gas

So, what happened here?
All properties created or changed in a function prototype affects all objects constructed using that prototype. As we could see, when I changed the property “fuel” in the prototype, the property has changed in the object. However, how can a change the property in the object and doesn’t change the prototype? Actually, I didn’t change the property; I add a new one for the object instead.
Let’s see.

		console.log(dreamCar.fuel); // Eletricity
		console.log(dreamCar.__proto__.fuel); // Gas

The concept behind here is that, despite the setting fuel inherited, the dreamCar object never had the property, it was a prototype’s property.

We can see creating a new object, and checking the properties of both objects:

		var dreamCar01 = new Car("Ford","GT40","Yellow"); 
		console.log(Object.keys(dreamCar01)); // ["brand", "model", "color"]
		console.log(Object.keys(dreamCar)); //["brand", "model", "color", "fuel"]


Another important concept is the chains. It means that is possible create multiple levels of inheritance. Let’s see an example:

		function Vehicle (type) {
			this.type = type || "public"
		}
		Vehicle.prototype.description = function() {
			console.log(this.type);
		}
		
		function Car(brand, model, color) {
			Vehicle.call(this, "private");
			this.brand = brand;
			this.model = model;
			this.color = color;
		}
		
		Car.prototype = Object.create(Vehicle.prototype)
		
		var dreamCar = new Car("Nissan","Skyline","Blue") 

		console.log(dreamCar); // Car {type: "private", brand: "Nissan", model: "Skyline", color: "Blue"}
		
		console.log(dreamCar.__proto__); // Vehicle
		
Note that the object dreamCar which uses the Car constructor inherited all properties and methods from Car.prototype(). Also, the Car.prototype() was created using the Vehicle.prototype() and will inherit all properties and methods from it.
Although the chain’s concept is useful, a chain with too many levels (inheritances), can make the code hard to understanding as well as to maintaining. So, use it carefully.

I hope to help you to understand a little bit more about the concepts of JavaScript. 




