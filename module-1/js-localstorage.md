![Ironhack Logo](https://i.imgur.com/1QgrNNw.png)

# JavaScript | `localStorage`

After this lesson, you will be able to:

- Understand what is `localStorage`
- Get and set properties of `localStorage`
- Use it to save locally the best score of a game


## What is `localStorage`?

When you execute code on a browser, you have access to a variable named `localStorage`. It is a kind of very simple database that is saved only in the browser. With `localStorage`, we will be able to save some information that will remains even if the user refresh or even close his browser.


### `getItem` and `setItem`

To read and write values from `localStorage`, we use `getItem` and `setItem`.

To test them, go to your favorite website, https://www.ironhack.com. Then open the console and type the following line. You should see `null` because you try to access the local storage "test" that is not defined yet. 

```js
localStorage.getItem('test')
```

![](https://i.imgur.com/JpOX7Mm.png).


Now type the following lines and see what happens. You should see that `localStorage.getItem('test')` has a new value.

```js
localStorage.setItem('test', 'Berlin')
localStorage.getItem('test')
```

![](https://i.imgur.com/pLpWtvx.png)


Now refresh your browser and type again `localStorage.getItem('test')`. You should see that displays the value you gave before!!


With Google Chrome, you can see the detail of `localStorage` by going to the tab "Application", then choose on the left "Storage > Local Storage > https://www.ironhack.com".

![](https://i.imgur.com/iq3Tp6t.png)


## Store more complex values

With `localStorage`, we can only save strings. But if we want to store more complex information such as object, there is a trick! For that we will use two functions:
- `JSON.stringify`: Converts a JSON (object or array) into a string
- `JSON.parse`: Converts a string into a JSON 


In practise, it will look like the following example:

```js
// Save an object with localStorage
var myObject = { city: 'Berlin', country: 'Germany' };
localStorage.setItem('location', JSON.stringify(myObject));

// Retrieve an object with localStorage
var localStorageObject = JSON.parse(localStorage.getItem('location'));
```


## Exercise: saving the best score in a game

Source code: https://codepen.io/maxencebouret/pen/mjZRWj

**Iteration 1**: Save the best score and display it on the "home" screen

**Iteration 2**: Save the 5 best scores and display it on the "home" screen

**Iteration 3**: Ask for the username when a game is over and display the 5 best scores with the username