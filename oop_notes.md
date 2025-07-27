# OOP NOTES

## OOP is split into 4 pillars
1. INHERITANCE
2. POLYMORPHISM
3. ENCAPSULATION
4. ABSTRACTION

- let's see **inheritance** first.
-
```python
class Animal:
	# parent class

class Dog(Animal):
	# child class inherited from parent
```

- mesela:
```python
class Animal:
	def speak(self):
		print("animal speaks")

class Dog(Animal):
	pass

dog = Dog()
dog.speak() # "animal speaks"
```

- you can actually override parent's methods
```python

class Animal:
    def speak(self):
        print("Animal speaks")

class Dog(Animal):
    def speak(self):  # Overrides Animal.speak()
        print("Dog barks!")

dog = Dog()
dog.speak()  # Output: "Dog barks!"

```
