## Website Performance Optimization portfolio project

### Rendering optimization in index.html

* Used an online tool to compress the 'profilepic.jpg' image: http://compressnow.com/
* Followed this documentation to eliminate render-blocking JavaScript: https://developers.google.com/speed/docs/insights/BlockingJS
  * Inline perfmatters.js because it is a small file
  * Added 'async' attribute to analytics.js
* Used an online tool to minify the CSS files: http://refresh-sf.com/
* Followed this documentation to asynchronously load CSS files: https://developers.google.com/speed/docs/insights/OptimizeCSSDelivery
  * Made a small modification to be able to load multiple CSS files.

### JavaScript optimization in views/js/main.js
#### Time to resize pizzas in pizza.html
* Changed the function 'determineDx' to 'determineWidth': The determineDx function is a complicated way of assigning percentage size. We only need to return a string in the form "xx%" and use it as the new width.
* Compute newwidth only once for all '.randomPizzaContainer' items
* Save the result of 'querySelectorAll' into a variable instead of using the function call in the for loop
```  
  function changePizzaSizes(size) {
    // Compute newwidth only once
    var newwidth = determineWidth(size);
  
    // run the 'document.querySelectorAll' only once
    var items = document.querySelectorAll(".randomPizzaContainer");
    for (var i=0; i<items.length; i++){
      items[i].style.width = newwidth;
    }
  }
```

### Framerate when scrolling in pizza.html
* The value of 'document.body.scrollTop' is the same for all iterations, so we can move it outside of the for loop to get the framerate around 60 fps.
```
var x = document.body.scrollTop / 1250;

for (var i = 0; i < items.length; i++) {
  var phase = Math.sin(x + (i%5));
  items[i].style.left = items[i].basicLeft + 100 * phase + 'px';
}
```
