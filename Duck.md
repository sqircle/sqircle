# WebKit Canvas

A WebKit canvas can get its data from a variety of sources. 

## HTML comes from:

1. Ruby Wrapper
2. Python Wrapper
3. URL
4. File          
6. Via Pipe Interface

Its important to note that there is no way to handle all the ruby libraries & python libs etc. So what we do is just let these libs know to parse these files and spit them out to the associated file. Which is `file/Canvases/CanvasName/CanvasName.html`.

## CSS comes from:

This is a bit hard because the App by its nature needs to be CSS aware to handle the auto-spriting etc. I think what can do is append the styles and then spit the out to a user in the format they'd like. Stylus, Compass LESs etc are relatively simple langs so all we to sis strip out the fluuf to gnerate them.  

THe app will have separate generated stylesheet. When a user creates sprites it will spit out css to this stylesheet.   

## Data comes from:

A simple JSON file. No reason to pollute our markup with content. Remember the goal of this app is to work with you every step of the way.  
JSON can be pull from web or local whatever.
 
# Interfaces

Your web design app should bend to your will. Not only should it be fully scriptable using Lua but it should pssible to expose most of its stuff to other apps.

## Webit canvas server using ruby + webrick.  

Access your WebKit canvas via browser. This gives you even more flexibility for working the way you want to work.    

## Pipe in html to canvas via a port.      

vim has piping this should to. There is no reason why instant previews shouldn't be available in your editor of choice. 
# Internals     

Everything image wise is GEGL based. Will use GTK to provide the display and all the frontend stuff.

GEGL means the GPU stuff (which I've heard is hard to do especially cross-platform) is handled for us. Open source ftw. On the shoulders of giants.

## Canvas drawing. 

The WebKit canvas drawing tools are just going to activate the tools written in JS. They're dummy tools that simply
activate stuff in the Webkit layer. When you draw using these tools on a WebKit canavs you'll actually be drawing using
JS tools. Note: research the performance of binding things this way. May have to change it based on that.

There are some good canvas drawing libs so probably all that will be needed is to create a brushes system & some shape
tools on top of it. Then good to go.

Lua + C++

Will use OpenGL entirey. Lua app loads up creates canvases. Webkit textute using opengl.
GTK texture using clutter. 
Shoudl eb able to displaye images using Clutter GEGL. Voila everything done.
Just need paper.js and canavs layer ontop of OpenGEGL.

# Elements

## Paper.js

Should be able to recreate paper.js by inheriting from ofPath. Then we need to draw point handlers and take the events.
We need import and export svg for persistence.

## Webkit canvas

Use awesominum

## GEGL display

Use the GEGL OpenGL stuff

## GEGL interface

Abstract using something similar to ofxGUI should be able to pipe settings directly into the nodes.
Drawing a node interface should be easy should be able to find existing OFX examples.

## Brush engine

Port over mypaint.js

## Viewports

It looks like all we have to do for eevryth we render is render a texture and use this http://forum.openframeworks.cc/index.php?topic=2012.0 to crop it.
We can keep track of everything in a tiled like fashion. 
Then we need panning functions. I think the best solution is to rip a game surface from polycode or love2d.
Figure out how abstrac tthe panning then for each of the view port types. This is honestly rpobably the hardest bit.

Use ofxUISuperCanvas and ofxUIScrollingCanvas. Also ofxTimeline implements some scrolling elements.
Pretty sure I can handle the port of ofxPanZoom. Will do that. We can then inherit from it and
use it pan around in view ports. Now we need to decide can we achieve one canavs? I think yes.
We just need to persist the viewport when editing.

We can also easily utilize Box2d for panning. The helloworld examples are demonstrative enough of panning.
We made need a few different things for different canvases but I thin k this will all work in the end.

viewCenter in Box2d is totally linked to the GLviewport. Everytime we pan all we need to do is do make
a call to gluOrtho2D which handles clipping planes. Holy shit that is easy.

## Tiled Image Surface

For drawing infinitely. Is GEGL infinite maybe we just draw onto that? Mayeb just rip from mypaint.

## Caching the viewport

# What is in a Photo Editor

- Canvases
- Layers   
- Objects
- Display
- Settings/Preferences Handling.
- UI kit.
- Nodes.    
- 2 Tool Palettes  
- Div Selector           
- OverLays
- God Options        
- Filters
- Brush Browser   

# Canvases      

We can only have a single active canvas at a time.    

Canvases are a central element. Sort of like documents, so there should be main tabs for navigating between them.
Special bar above everything with the Canvases nav and maybe something else.       

# Layers
              
* Eye Icon
* Layer name
* Icon to indicate styles            

Select a layer and get an options palette with:

- Opacity
- Blending Mode Drop Down     

# Objects/Symbols

Will have option in preferences to set the style but by default should be a popup of images.

We will ovalize them and apply some drop shadows. Click on one and bring up relevant mode. Painting mode etc.     

# Display

Display is full screen by default and everything takes place on top of it. If not full screen document windows float like in PS.  When its not full screen the bar goes up to document window reflects active canvas.

# Settings/Preference  

Do this with a UI Kit. Left menu and forms in main area. Simple yet effective.

# UI Kit

Need to create a consistent set of button popup styles etc. 

# Nodes

List nodes and their previews. Either an Icon or the actual image.

- Colors
- Levels
- Curves
- B&W
- Blur
- Overlay        

# 2 Tool Palettes  

Tools palette is editable but here is the default for painting/image mode.

- Move Tool          
- Crop Tool
- Square Selection Tool       
- Polygon Selection Tool 
- Brush
- Eraser
- Color Picker
- Shape tool
- Pen Tool
- Modify Point Tool
- Add Point tool       

Add for WebKit canvas.

- Brush
- Color Picker
- Pen Tool
- Modify Point Tool
- Add Point tool   

# Div Selector

Its important to have a canvas element to draw on. Div selector allows one to select an html element.

# Overlays   

Add Images above the WebKit layer.

Adjust opacity only.

# One options palette to rule them all.
     
Why do we have to search for brush options. The options palette should be able to be always showing and automatically pull the options for what we're doing. We can have multiple options palettes out and then set them to something.

Tools palette is modal based select canvas layer updates tool palette to available tool.
Selecting a tool in the palette communicates via js to the webkit layer to select that tool. The UI for the canvas drawing system is hidden.  
Objects have extendable meta data that will give another class info they need.

# Filters

Filters can only effect images in a node, They never take effect in a canvas. 

Image layers can blend with any image layer below. Scratch that any image layer has an image rep which we grab and blend in the final composite.

To eliminate confusion UI wise. Canvases should act as containers. i.e you can have a complex image layer in a webkit canvas.   

# Brush browser

- Brush Tip Preview
- Brush Type/Name    


## Refactor using node-webkit

Will use Node for most of the UI. Can borrow from NoFlo for the Node interface for GEGl.

Then to display image we just need a surface. We can still from MyPaint or a node.js painting app.

We should treat anything drawn in vector as a format that can be thrown into a GEGL/Raster symbol easily.
If all vectors are SVG. Then just an SVG node?

Every item is a symbol. So dblclick on it and the editor is smart enough just from the class it has to pull up it's souce.
Where is the source defined? Probably in a YAML file that maps a symbol to it's source file.

We just need to make node-canvas be backed by a GEGL buffer. Then make it infinite.

It might be possible to use gegl as the tile store and simple reqeust from it.
Or we can just keep track of the tiles by an position width/height etc then request that rectangle. 
Whenever you pan out of the tiles boundaries one grabs the other segment?

But what about partial tiles? Panning snapping to big squares seems ridicioulousy annoying. Maybe keep tiles really smalL?

Actually what about when we pan we just get the dimensions of where we are and get that rectangle from GEGL?
Would that perform adequately?

Paper.js has view.scrollBy https://groups.google.com/forum/#!topic/paperjs/rDfaxwEAOlI

This for drawing GEGL to a cairo surface. http://www.spinics.net/lists/gegl/msg01160.html

Symbols can just be elements with a symbol attribute. 

All UI even stuff like layers are Light Table UI elements.

The only thing we need to do then overlay the window for editing a raster element.
Should be an above the element to leave the mode. Or maybe a little dialog to exit.

Saving should edit the css of the element. All css saves should go to the raw source file and make changes there.
Then re-eval it.

## Node-webkit

We can utilize Node.js + ClojureScript + Pix.js to build drawing apps. Then we can leverage entire JS ecosystem easily.

Just build everything on top of the browser.
Since we are native we can resolve the performance issues.

Compiling clojurescript with external libs is easy just do 

(def cats (js/require "cats"))

Which translates to

namespace = {};
namespace.cats = require("cats");

Or (let [restify (node/require "restify")

Boom!

Then we just run the compiled js through grunt-browserify


Use https://github.com/zcaudate/purnam for better interop.

## How to get this done

We need to build up Sqircle as a series of miniapps

1. A node based image editor with filters and an XML format backed by WebGL
2. Symbol and Asset handling plugin for Light Table
3. A triangles app
4. A painting app (should support multiple brush engines)
5. A vector editor and drawing app
6. A visual editor for CSS styles/gradients that works with Symbol and Asset plugin
7. An animation tool
8. An HSL color picker
9. Flexible Tabset shapes. 
10. An image editor with clone tool, smudge tool, layers with blend modes (should be backed by paint app and node image editor)

We should focus on the most experimental and useful stuff first so we can release them as apps.
