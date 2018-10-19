# Canvas Cheatsheet

```js
var canvas = document.querySelector('canvas')
var ctx = canvas.getContext('2d')

var width = canvas.width
var height = canvas.height

// For simple shapes
ctx.fillRect(x,y,width,height)
ctx.strokeRect(x,y,width,height)
ctx.clearRect(x,y,width,height)

// For complex shapes
ctx.beginPath()
ctx.moveTo(x,y)
ctx.lineTo(x,y)
ctx.arc(x,y,radius,startAngle,endAngle,anticlockwise)
ctx.closePath()
ctx.fill()
ctx.stroke()

ctx.fillText(text, x, y maxWidth)

// Styling
ctx.fillStyle = 'rgba(255, 0, 0, 0.5)'
ctx.strokeStyle = 'rgba(255, 0, 0, 0.5)'
ctx.globalAlpha = 0.5
ctx.lineWidth = 2
ctx.font = "20px sans-serif"
ctx.textAlign = "center"

// Images
var img = new Image();
img.src = 'myImage.png'; 
img.onload = function() {
  // Code executed when the picture is loaded
}
ctx.drawImage(img, x, y, width, height)

// Animations
var intervalId = setInterval(function(){
  update() // => change the objects to make them move or appear or disappear
  drawEverything() // clear the canvas and draw the background and all objects 
}, 1000/60)

function stopGame() {
  clearInterval(intervalId)
}

// Listen for click events
document.onkeydown = function(e) {
  switch (e.keyCode) {
    case 38: ghost.moveUp(); break;
    case 40: ghost.moveDown(); break;
    case 37: ghost.moveLeft(); break;
    case 39: ghost.moveRight(); break;
  }
}
```
