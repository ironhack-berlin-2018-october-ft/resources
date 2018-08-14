![Ironhack Logo](https://i.imgur.com/1QgrNNw.png)

# JavaScript | `localStorage`

After this lesson, you will be able to:

- Understand what is `localStorage`
- Get and set properties of `localStorage`
- Use it to save locally the best score of a game


## What is `localStorage`?

When you execute code on a browser, you will have access to a variable named `localStorage`. It is a kind of very simple database that is saved on just the client browser. With `localStorage`, we will be able to save some information that will remains even if you refresh or even close the browser.


### `getItem` and `setItem`

We will play with 2 methods of `localStorage`: `getItem` and `setItem`.

First, go to your favorite website, https://www.ironhack.com. 

Then open the console and type the following line. Here you should see `null` because you try to access the local storage "test" that is not defined yet. 

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

```js
// Save an object with localStorage
var myObject = { city: 'Berlin', country: 'Germany' };
localStorage.setItem('location', JSON.stringify(myObject));

// Retrieve an object with localStorage
var localStorageObject = JSON.parse(localStorage.getItem('location'));
```