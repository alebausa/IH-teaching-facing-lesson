# Lesson 1: Objects and Arrays in JavaScript

### Lesson Duration: 3 hours

> Purpose: The purpose of this lesson is to go into detail of arrays and objects, understand the basic concepts of array and object manipulation and data access and introduce some of JavaScript's most common array and object methods.

---

### Setup

- All previous set up: VSC with LiveServer extension.

### Learning Objectives

After this lesson, students will be able to:

- Understand how <code>push()</code>, <code>unshift()</code>, <code>pop()</code>, <code>splice()</code> and <code>forEach()</code> work
- Understand how to access the data in nested object and arrays
- Understand the difference between what a method does and what a method returns
- Read official documentation before starting to code
- Create a data structure combining arrays and objects
- Iterate trough arrays

---

### Lesson 0: What have we learned so far?

> :clock10: 5 min

- How can we declare a new array
- Property .length of iterable elements
- Access its elements with braket notation and index

<details>
  <summary> Code examples </summary>

```javascript
// Name should be written in plural
const fruits = []

// We can access data with bracket notation
console.log(fruits[0])

// Check length property
console.log(fruits.length)
```

</details>

---

### Lesson 1: Data manipulation in arrays - key concepts

> :clock10: 20 min

⚠️ Before using any method, one should ask themselves first:

1. Does the method modify the original array?
2. What is its return value?
3. Check official documentation for each method before using them: [MDN Web docs](https://developer.mozilla.org/en-US/)

Most common methods to add and retrieve data from arrays:

- <code>arr.push()</code> method: adds at the end of the original array, but returns the length of the array
- <code>arr.unshift()</code> method: adds at the beggining of the original array, but returns the length of the array
- <code>arr.pop()</code> method: retrieves the last element of the original array, and returns the deleted element
- <code>arr.shift()</code> method: retrieves the first element of the original array, and returns the deleted element
- <code>arr.splice()</code> method: add and retrieve as many elements of the original array as you wish. It returns the deleted elements.

<details>
  <summary> Code example 1: simple methods </summary>

```javascript
const students = ['Elisa', 'Guillem']

function updateStudentDatabase() {
  let student = prompt("What's your name?")
  students.push(student)
  return students
}

updateStudentDatabase() // Call the function
students.unshift('Marina')
console.log(students) // Check what happened
students.pop()
console.log(students) // Check what happened
students.shift()
console.log(students) // Check what happened
```

</details>
<details>
  <summary> Code example 2: splice() </summary>

```javascript
const favFoods = ['pizza', 'icecream', 'pasta', 'avocado']

// Two parameters: where do I start deleting (index), how many I delete
favFoods.splice(1, 1)

// Three parameters: where do I start deleting, how many I delete, what I add instead
favFoods.splice(0, 1, 'salad')

// I can access the last element with length -1
favFoods.splice(favFoods.length - 1, 1, 'apple')

// What If I don't know the index of the element I want to retrieve?
let index = favFoods.indexOf('pasta')
console.log(index)
favFoods.splice(index, 1)
```

</details>

---

:coffee: **BREAK**

---

### Lesson 2: Array iteration key concepts

> :clock10: 20 min

Iterate through an array with <code>for</code> and <code>forEach</code>

- for loop (already performed)
- forEach: it takes a callback function and its return value is undefined

<details>
  <summary> Code example: for loop </summary>

```javascript
const arrayNames = ['Pedro', 'Jake', 'Joan']
for (let i = 0; i < arrayNames.length; i++) {
  console.log(arrayNames[i])
}
```

</details>

<details>
  <summary> Code example: forEach </summary>

```javascript
const arrayNames = ['Pedro', 'Jake', 'Joan']

// It takes a callback function
arrayNames.forEach(function (name) {
  console.log(name)
})

// I can also write the callback function as an arrow function (ES6)
arrayNames.forEach((name) => console.log(`Hello ${name}!`))

// I can manipulate arrays from within
const copyOfNames = []
arrayNames.forEach((name) => copyOfNames.push(name))
console.log(copyOfNames)

// I can perform more complex operations combining the forEach method with other elements (methods or properties)
const students = [
  'Kwabena',
  'Guillem',
  'Daniel',
  'Josep',
  'Elisa',
  'Elo',
  'Carlos',
]
const dropOuts = ['Guillem', 'Josep']
dropOuts.forEach((student) => {
  const indexOfDropOut = students.indexOf(student)
  students.splice(indexOfDropOut, 1)
})
console.log(students)
```

</details>

---

#### :pencil2: Time to practise

> :clock10: 20 min (+ 10 min Review)

<details>
  <summary> Click for instructions </summary>

- Fork the following replit into your account: [Array practise](https://replit.com/@AlejandraBausa/ArrayPractice#script.js).

</details>

<details>
  <summary> Click for solutions: we will code along the solutions together </summary>

```javascript
// SOLUTIONS

// 1.1.
animals.shift()
// 1.2.
animals.pop()
// 1.3.
animals.splice(2, 1)
// 1.4.
animals.unshift('iguana')

// 2.1.
numbers.forEach((number) => console.log(`You have ${number} euros!`))
// 2.2.
const newNumbers = []
// 2.3.
numbers.forEach((number) => newNumbers.push(number * 2))
// 2.4.
const allTheNumbers = numbers.concat(newNumbers)

// 3.1.
letters.reverse()
// 3.2.
letters.includes('c')
```

</details>

---

:coffee: **BREAK**

---

### Lesson 3: Object manipulation key concepts

> :clock10: 20 min

- Objects are commonly used when there are several properties that belong to the same concept or unit of data
- There are different ways to declare objects
- We can access their properties via bracket notation or dot notation
- There are different methods to check whether an object has a specific key declared
- There are ways to reassign keys and values in an object and create new keys
- Iterate through the object keys with the <code>for in</code> method

<details>
  <summary> Click for code examples</summary>

```javascript
const student = {}
const student = new Object()
const student = {
  // Key: value
  name: 'Olivia',
  age: 32,
  level: 'intermediate',
  scholarship: true,
}
```

```javascript
// Bracket notation
console.log(student['age'])
// Dot notation
console.log(student.age);
}
```

```javascript
console.log(Object.keys(student)); // Returns a key array
}
```

```javascript
// Add properties or reassign them

// Via dot notation
student.phone = 637129070;
// Via bracket notation
student['lastName'] = 'Dunham';
}
```

```javascript
// Add properties or reassign them

// Via dot notation
student.phone = 637129070;
// Via bracket notation
student['lastName'] = 'Dunham';
}
```

```javascript
for (let key in student) {
  console.log(key)
}
```

</details>

---

### Lesson 4: Arrays & Objects combined key concepts

> :clock10: 20 min

- Objects can contain nested objects, and we can chain different notations to access data
- There are multidimensional arrays: how to access array sublevels
- If we combine arrays and objects, we have data structures, and therefore,we can combine notations to access the data

<details>
  <summary> Click for code examples</summary>

```javascript
const school = {
  address: {
    street: 'Fake St',
    number: 34,
  },
  contact: {
    phone: 934561278,
    email: 'school@edu.com',
  },
}

// Access the email property
school.contact.email
```

```javascript
const groups = [
  ['Harry', 'Ron', 'Hermione'],
  ['Draco', 'Crab', 'Goyle'],
  ['Luna', 'Ginny', 'Neville'],
]

// Access the 'Crab' string:
groups[1][1]
```

```javascript
const classRoom = {
  teacher: {
    firstName: 'Marcelino',
    lastName: 'Padberg',
    age: 25,
    specialty: 'WEB DEV',
  },
  students: [
    { firstName: 'Aliyah', lastName: 'Schulist', age: 18 },
    { firstName: 'Cleveland', lastName: 'Towne', age: 28 },
    { firstName: 'Jan', lastName: 'Quitzon', age: 18 },
    { firstName: 'Alaina', lastName: 'Runolfsdottir', age: 18 },
    { firstName: 'Gerhard', lastName: 'Bergstrom', age: 23 },
  ],
}

// Access the last name of the student Jan
classRoom.students[2].lastName

// To modify an element we can simply reassign it:
classRoom.teacher.specialty = classRoom.teacher.specialty.toLowerCase()
console.log(classRoom)
```

</details>

---

#### :pencil2: Time to practise

> :clock10: 20 min (+ 10 min Review)

<details>
  <summary> Click for instructions </summary>

- Fork the following replit into your account: [Object and array practise](https://replit.com/@AlejandraBausa/ObjectPractice#script.js).
</details>
<details>
  <summary> Click for solutions (code along together) </summary>

```javascript
// Solutions

// 1.1.
restaurants[2].address.street

// 1.2.
restaurants[0].cuisine[0]

// 1.3.
restaurants[1].cuisine.forEach((elem) => console.log(elem))

// 1.4.
restaurants[0].isAccessible = false
restaurants[1].isAccessible = false

// 1.5.
console.log('isAccessible' in restaurants[1])

// 1.6.
Object.keys(restaurants[2])

// 1.7.
function getRandomRestaurant() {
  const randomRestaurant =
    restaurants[Math.floor(Math.random() * restaurants.length)]
  return randomRestaurant
}
```

</details>

---

### ✅ End of the day: recap

> :clock10: 10 min

- What have we learned today?
- What are the students supposed to do in the lab?
