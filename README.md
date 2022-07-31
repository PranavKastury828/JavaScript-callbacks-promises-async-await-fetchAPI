# JavaScript-callbacks-promises-async-await-fetchAPI
A beginner friendly repository explaining JavaScript Callbacks, Promises, Async/Await and the Fetch API through code examples

# Callbacks, Promises, Async/Await and the Fetch API

  

 Fetch API requires a discussion of...

## Callbacks, Promises, Thenables & Async/Await

  

**Callbacks** - functions that are passed as parameters to other functions

They will call that function after finishing the other stuff

  

	function firstFunction(parameters, callback) {

	//do stuff with parameters

	callback();

	}

Problem with callbacks - **callback hell**

	firstFunction(paramOne, function() {

		//do stuff

		secondFunction(paramTwo, function() {

			//do some stuff

			thirdFunction(paramThree, function() {

	//do more stuff

			})

		})

	})

**Promises** deliver async code even if JS is synchronous (doing one thing at a time)

- Promises: "You go ahead, I'll catch up once I'm done"

- You're executing two different blocks of code at once
- 3 states - Pending, Fulfilled, Rejected

		const myPromise = new Promise((resolve, reject) => {

		const error = false

		if (!error) {

		resolve("Yes, resolved promise")

		} else {

		reject("No! Rejected the promise")

		}

		})

		console.log(myPromise)

This gives the state of the promise and the value in the form of an object. So to get the value out of the Promise, we need to chain "Thenables" to the Promise. Refer below

#### Thenables
	myPromise.then(value => {

	console.log(value) //we only get the return value of the resolve and not the state

	return value + 1;

	}).then(newValue => {

	console.log(newValue) //returns value + 1

	return newValue + " Some BS"

	}).then(newValueTwo => {

	console.log(newValueTwo)

	})

Let us now look at the reject for a Promise using **"catch"**

	const myPromise = new Promise((resolve, reject) => {

	const error = false

	if (!error) {

	resolve("Yes, resolved promise")

	} else {

	reject("No! Rejected the promise")

	}

	})
	myPromise.then(value => {

	console.log(value) //we only get the return value of the resolve and not the state

	return value + 1;

	}).then(newValue => {

	console.log(newValue) //returns value + 1

	return newValue + " Some other line"

	}).then(newValueTwo => {

	console.log(newValueTwo)

	}).catch(err => {

	console.log(err);

	})

Understanding delay that Promises could have while retrieving data from an external server using fetch API. This is demonstrated using an alternative method - **setTimeout**

	const myNextPromise = new Promise((resolve, reject) => {

	setTimeout(function() {

	resolve("myNextPromise resolved!")

	}, 3000)

	}) 

	myNextPromise.then(value => {

	console.log(value)

	})

  
	myPromise.then(value => {

	console.log(value)

	})

#### Pending state of Promise (using fetch API)

	const users = fetch("https://jsonplaceholder.typicode.com/users")

	//pending state
	console.log(users)

	fetch("https://jsonplaceholder.typicode.com/users").then(response => {

	console.log(response);

	return response.json();

	})

	.then(data => {

	data.forEach(user => {

	console.log(user.id)

	console.log(user.name)

	})

	})


In the above example, to work with data, we end up using a chain of thenables that is surprisingly similar to Callback hell.

#### Async / Await

	const  myUsers = {

	userList: []

	}

	const  myCoolFunction = async() => {

	const  response = await  fetch("https://jsonplaceholder.typicode.com/users") 
	/* adding await tells the code to WAIT for the data to be fetched from jsonplaceholder
	 BEFORE doing the next thing */

	const  jsonUserData = await  response.json() //Using await here as well since response.json() also returns a Promise

	console.log(jsonUserData) //The code on line 126 is just replicating this

	return  jsonUserData;

	}

To use `await`, it must be within an `async` function

	const  anotherFunc = async() => {

	const  data = await  myCoolFunction();

	myUsers.userList = data;

	console.log(myUsers.userList)

	}

	anotherFunc();
