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

