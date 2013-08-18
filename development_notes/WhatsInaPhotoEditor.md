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
