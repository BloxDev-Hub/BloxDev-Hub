---
title: Inheritance
template: docs.html
comments: true
hide:
  - navigation
---
!!! attention "Note"
    Before reading this tutorial, you should know about [metatables](https://docs.rodevs.com/Scripting/Advanced-Courses/metatables/). An explanation of metatable exists in the Lua-Learning folder.

# What is Inheritance?

Inheritance is used mainly in oop based languages that allow one class to inherit the properties and methods from another class. 

*do note that there are a few ways of doing inheritance in lua(u) and this is one of them
## Setting up Inheritance

Let’s say we have a class called Person Class that is set up like this

```lua
local Person = {}

Person.__index = Person
-- for those that don't remember these two methods of creating __index does the same thing 
Person.__index = function(self,key)
    return Person[key]
end

function Person.new(Name,Age,Balance)
   return setmetatable({Name = Name,Age = Age, Balance = Balance},Person)
end

function Person.__tostring(self)
    return self.Name
end
function Person:GetBalance()
    return '$'..self.Balance
end

function Person:GetAge()
    return self.Age
end

function Person:GrowUp()
    self.Age += 1
end

return Person
```
Now lets make a Class call Student that will inherit from the Person Class and give it a Method called PayStudentTuition

```lua
local Student = {}
local Person = require(Path.To.Person.Class)

Student.__index = function(self,key)
    return Student[key] or Person[key]
end

function Student.__tostring(self)
    return "Student: "..self.Name
end

function Student.new(Name,Age,Balance,Id)
	return setmetatable({Name = Name,Age = Age,Balance = Balance,Id = Id},Student)
end
--another way you can make the constructor
function Student.new(Name,Age,Balance,Id)
    local person = Person.new(Name,Age,Balance)
    person.Id = Id
    return setmetatable(person,Student)
end

function Student:PayStudentTuition(fees)
    self.Balance -= fees
end

return Student
```

Basically what we've done is modify the __index metamethod so it also checks the Person class if the method you're looking for does not exist in the Student Class

For those that are wondering why we need to do it like that and we can't just do this

```lua
local Student = {}
local Person = require(Path.To.Person.Class)

Student.__index = Student

function Student.new(Name,Age,Balance,Id)
   return setmetatable(setmetatable({Name = Name,Age = Age,Balance = Balance,Id = Id},Person),Student)
end
```

it's because using setmetatable on a metatable will override the current metatable's metamethods.


Now lets make a Class call Teacher that will inherit from the Person Class and give it a Method called `GetPaycheck`

```lua
local Teacher = {}
local Person = require(Path.To.Person.Class)

Teacher.__index = function(self,key)
    return Teacher[key] or Person[key]
end

function Teacher.__tostring(self)
    return "Teacher: "..self.Name
end

function Teacher.new(Name,Age,Balance)
    return setmetatable({Name = Name,Age = Age,Balance = Balance},Teacher)
end

function Teacher:GetPaycheck(Amt)
    self.Balance += Amt
end

return Teacher
```

Here is an example script 

```lua
local StudentClass = require(Path.To.Student.Class)
local PersonClass = require(Path.To.Person.Class)
local TeacherClass = require(Path.To.Teacher.Class)
local Hao = PersonClass.new("Hao",nil,-99999)
local Bob = StudentClass.new("Bob",10,30,1235)
local Smith = TeacherClass.new("TeacherClass",37,200)

Bob:GrowUp() -- this is a method in the Person Class
Bob:PayStudentTuition(4000) -- this is a method in the Student Class
print(Bob:GetAge()) --> 11 
print(Bob:GetBalance()) --> $-3970
print(Bob) -- Invokes the __tostring metamethod --> "Student: Bob"

Smith:GetPaycheck(100) -- this is a method in the Teacher Class
print(Smith:GetBalance()) --> $300
print(Smith) --> "Teacher: Smith"

print(Hao) --> "Hao"

```

Also if you want to inherit from multiple classes you would just keep adding to the `__index` metamethod 

```lua
local MiddleSchoolStudent = {}

MiddleSchoolStudent.__index = function(self,key)
    return MiddleSchoolStudent[key] or Student[key] or Person[key] -- you can keep adding to this 
    -- this will first check MiddleSchoolStudent then Student and lastly Person
    --*the order of this will effect the outcome 
end
```

## Thanks for reading!
Thats pretty much it for this method of inheritance. if you have any more questions you can ask in #scripting-help or if you have any more suggestions you can send me a dm (@Haotian2006#3314)