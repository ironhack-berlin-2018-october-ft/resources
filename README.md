![Ironhack Logo](https://i.imgur.com/uYvaMH6.png)

# Bootcamp Resources

## Goal

The goal of this page is to share good resources with the class.

## Ironhack links

### Course links
- [Learn Platform](http://learn.ironhack.com)
- [Ironhack Berlin 2018 October Full-Time GitHub page](https://github.com/orgs/ironhack-berlin-2018-october-ft/): To find all the repositories
- [Morning challenges](https://repl.it/@MaxenceBouret/morning-challenge-october)


### Projects
- **[Project 1 guidelines](https://docs.google.com/presentation/d/17PPiYmF8CzFx-x980UMPx-jsUJPmTj67HVJWo96OHKg/edit?usp=sharing)**
- **[Project 1 list](https://docs.google.com/spreadsheets/d/1ik82xwJmrkLMWMQip2Q3yXl3pTu69z5zxHMtPdoXd80/edit?usp=sharing)**
- Project 2 guidelines (coming soon)
- Project 2 list (coming soon)
- Project 3 guidelines (coming soon)
- Project 3 list (coming soon)


### Survey
- [**Weekly Survey**](https://goo.gl/forms/nMvgsTMOGUahZWk42) (To fill every week)
<!-- - [Anonymous Survey](https://sayat.me/mc100s)  -->


## External resources

### To learn
- [regex101.com](https://regex101.com/): Website to test and understand Regular expressions
- [A guide to flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/): The Flexbox Bible
- [getbootstrap.com](http://getbootstrap.com): The Bootstrap documentation
- [W3schools CSS Selectors ](https://www.w3schools.com/cssref/css_selectors.asp): Cheatsheet for CSS selectors
- [Making Sprite-based Games with Canvas](https://github.com/jlongster/canvas-game-bootstrap/blob/master/tutorial.md)

### Software
- [Photopea](https://photopea.com): Online Free Photoshop

### Content
- [Unsplash](http://unsplash.com): Website with free good pictures (with an API)
- [Flaticon](http://flaticon.com): Website to find nice icons
- [OpenGameArt.org](https://opengameart.org): Website to get game picture resources
- [Coolors](https://coolors.co): A super fast color schemes generator

## Berlin Extra Curriculum

### General
- [Visual Studio Tips](./visualstudio.md)


### Week 1

#### Day 2
- Exercise: [CSS Positioning](./exercises/css-positioning/README.md)
- Exercise: [Flexbox Froggy](https://flexboxfroggy.com)

#### Day 3
- Exercise: [CSS Transitions](https://codepen.io/maxencebouret/pen/NOjKga?editors=1100)

#### Day 4
- Exercise: [Flexbox exercise](https://codepen.io/maxencebouret/pen/QZgvdp?editors=1100)

#### Day 5
- Course: [Class syntax (ES5 and ES6)](./module-1/classes.md)
- Pair Programming: [Lab JavaScript Vikings](https://github.com/ironhack-berlin-2018-october-ft/lab-javascript-vikings)
- Example in class: [JavaScript DOM Manipulation](https://github.com/ironhack-berlin-2018-october-ft/w1-friday-dom-manipulation)


### Week 2

#### Day 4
- [Canvas Cheatsheet](./module-1/canvas.md)

### Week 4

#### Day 3
- No need to understand the concept of partial
- [Daily Exercise without partial](https://github.com/ironhack-berlin-2018-october-ft/lab-ironbeers)

## FAQ

### General

#### How to kill a server (for example on PORT 5500)?

First you need to run the following command, that will give you the list of process using the port.
```sh
$ lsof -wni tcp:5500
# Answer 
# COMMAND     PID          USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
# Code\x20H 28289 maxencebouret   45u  IPv4 0xa9b05c1a28ae649b      0t0  TCP *:fcp-addr-srvr1 (LISTEN)
```

Then you you need to find the **PID** (here it's `28289`) and launch the following command:
```sh
$ kill -9 28289
```

### Backend

#### `Error: Cannot find module 'express'`

Your packahe is not installed. You need to do the following command at the root of your project (where you have the `package.json`): 
```sh
$ npm install express
```
