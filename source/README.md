================================================================================
Daniel Abrego
Udacity Front End Developer Nanodegree
Project 4
Website Optimization
================================================================================


================================================================================
I. PageSpeedInsights: How to optimize index.html
================================================================================
1. Open 2 terminals and both terminals, change directory to the top level directory holding the index.html file.
2. Terminal 1 - start python webserver using command >python -m SimpleHTTPServer 8000
3. Terminal 2 - start ngrok with command >ngrok http 8000
4. When ngrok starts, Terminal 2 will show a URL to past into PageSpeedInsights website, and it will analyze your index.html.


================================================================================
I.A. PageSpeedInsights: These are the optimizations to index.html recommended
from using pagespeed insights and ngrok to serve the localhost:
================================================================================
Mobile & Desktop

Optimize images
	1. Compress and resize views/images/pizzeria.jpg
	2. Compress and resize img/profilepic.jpg

Remove render-blocking script resources:
	1. Within index.html, add 'async' tag to link to analytics.js since this script does not likely manipulate the DOM.
	2. Used example from https://developers.google.com/speed/docs/insights/OptimizeCSSDelivery to inline font "http://fonts.googleapis.com/css?family=Open+Sans:400,700" so it loads load after initial painting of the page.
	3. Inlined the entire source of style.css directly into index.html to prevent additional request for css file.
	4. Added attribute "media="print" to print.css.

Followed link provided on PageSpeedInsights.com to "Download optimized image, JavaScript, and CSS resources for this page."
    1. This link provided minified and compressed css/print.css, image/pizzeria.jpg, image/profilepic.jpg, js/perfmatters.js

Used online HTML Compressor at https://htmlcompressor.com/compressor/ to compress index.html.


================================================================================
II. 60 Frames per Second:  How to optimize views/pizza.html
================================================================================
1. Open the file in the browser using the local filesystem like so:
   file:///home/path-to-portfolio/views/pizza.html
2. Press F-12 to open the Chrome Developer Tools.
3. From Chrome Developer Tools, switch to the 'Timeline' menu at the top of the tools window.
4. Press the grey dot at the top left to start recording. The dot turns red.
5. Scroll the page shown in your browser up and down.
6. Press the red dot to stop recording, and observe the timeline.
7. Use the timeline to isolate problems such as long running scripts or excessive layout.

================================================================================
III.A. 60 Frames per Second: Optimizations made in views/js/main.js
================================================================================

Line 424
Refactored function changePizzaSizes
- removed repetitive and slow call to document.querySelectorAll() and
  replaced with single call that is stores the result of the DOM call in variable 'randomPizzas'
- removed unnecessary function 'determineDX()' and replaced with straight percentages
- this allowed removal of code dependent on 'determineDX()'


Line 503
Re-factored a DOM-read that was being called over and over resulting in multiple forced synchronous layouts.
Pulled the DOM-read out of a loop since it only needed to be called once.


Line 531
Reduce the number of pizzas that are iterated since only a few can actually be shown at a time on the screen.
It was originally attempting to draw 200 pizzas at once, forcing a lot of paint envents.



