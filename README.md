# Lasercutting with Inkscape for dummies

a collection of tricks and techniques that I have accumulated to efficiently create vectorfiles for lasercutting. I wrote


### Creating new files

After opening a new file in inkscape, you can go to *file > document properties*, and set the document width and height to correct size. You can also set the unit to mm or whichever you prefer.


### General tips

###### Shape fill and line
It can be very useful to make your shapes semitransparent. This can be achieved by rightclicking a shape, and choosing *fill and line*.
You can then set the alpha value in fill. This will also be used for future shapes that you create.

**Line: make sure you disable line color until the very end, otherwise your shapes will not have the correct size.**

![](http://i.imgur.com/UCA83re.png)

#### Snapping and grid

When you're working on shapes, its often convient to have one shape touch another shape. You can make your cursor snap to nearby corners/edges/middles/other features.
This behaviour can be controlled with the toolbar ([image](http://i.imgur.com/7m4eAC0.png)) on the very right side of the screen.
The main useful ones are the first 4 ones.
The snapping works based on how far your cursor is on the screen from the point, so you can zoom in or out if you experience unintended snapping.

###### Grid
I personally prefer to work without a grid, but some people like it more. Grid can be disabled and enabled in *page > grid*



### Working with shapes

You can select multiple shapes with shift+drag or by holding shift and clicking each shape individually. The last can also be used to deselect shapes.
Copy shapes with ctrl+c, paste with ctrl+v.

#### Moving shapes
Sometimes snapping isn't enough to move the shapes. In such cases, you can create a dummy square, set its size, and use this as an offset. This is especially easy when you have to repeat an action multiple times, as you can just copy the dummy square with the real square.
Alternatively, you can use the transform menu (*Object > transform*) to precisely move shapes.
Theres one more way to move shapes, and that is the arrow keys. However for this to be useful, you have set the amount a keypress moves a shape: in *edit > preferences*, *behaviour > steps* and the first option. I personally have mine set to 1 mm. If you hold down shift while using the arrow keys, all the shapes will move 10 times that distance.


#### Creating shapes

**Squares**
You can create squares with the square tool on the left. After you created a square, you can use the selection tool (**F1**) to set it to the correct size in the top toolbar (*B:* and *H:* fields), and move it to the correct position.

**Circles and rounded corners**
There are multiple ways to create circles. I personally prefer to create a square first, and after I'm done giving it the correct location and everything, I use the square tool to set the corner radius Rx in the top toolbar. Set both Rx and Ry to create ovals.

**Slanted edges**
To create slanted edges, you can first create a second square that is big enough, then rotate it with the transform > rotate menu (*Object > transform*). After you've moved the shape to the correct position, you can subtract that square from the original shape as explained below to create the slanted edge.

#### Adding and subtracting shapes.

**Adding shapes**
You can combine two or more shapes by selecting them, and pressing **ctrl+'+'**.
When combining shapes, try to make sure that the shapes actually overlap, because otherwise you have a high chance of creating zero width gaps due to rounding errors. More information below.

**Subtracting shapes**
This only works when you have exactly two shapes selected.
To subtract the newest shape from the oldest shape, use **ctrl+'-'**.
Similary, you can subtract the oldest shape from the newest shape, use **ctrl+'\*'**
Keep in mind to extend the shape you are subtracting off the original shape to beyond the original shape, otherwise you're going to run into the same rounding error issue.


### Creating teeth
Often you want to design complex 3D structures, and they need alot of teeth to interlock. You can do this efficiently by creating a large teeth shape at the beginning of a project.
To create this shape, simply copy paste one tooth over and over and then combining all of them together to a single shape like so.
![](http://i.imgur.com/KGsLOf6.png)
When you need a teeth side in your shape, you can copy this teeth shape and subtract it or add it to the original shape. Keep in mind the rounding errors when doing this! You can easely stretch your teeth to avoid this.
After you've created the teeth shape on one side, you can simply copy the shape, and subtract it from the other shape where you need the matching teeth. This will make sure you don't mess up and horribly mismatch the teeth.

### Practical tips

#### Printing holes in small shapes
Often, when you print a small shape, it moves just a little bit because of the force of the printer. To avoid this, I wrote a simple extension that will make sure the smaller holes get printed before the outline. Installation and usage instructions for this extension can be found here: (inkscape-laser-sequence-extension)[https://github.com/L0laapk3/inkscape-laser-sequence-extension]

#### Zero width shapes and invisible cuts.
Often, when you add touching shapes together, inkscape can induce rounding errors. This will result in a zero wide gap, which you can only see enabling shape lines and setting line style to a high value.

![](http://i.imgur.com/boT4zfa.png)

This is very annoying and can often cause failed prints.
I found this "hack" that can fix this problems. Before you can use it, you need to go to *edit > preferences*, *behaviour > steps*, and set *inset/outset with:* to zero.
Then, to fix the selected shapes, you first use to *path > outset*, and then *path > inset*.

Note that this is a dirty hack, it can create new nodes in your path and induce even more rounding errors, use with care.


### Before printing

#### Cutting
Select all the shapes, rightclick *fill and line*. In fill, select no fill. in line color, select solid color, you want to set the line color to red or whichever color is required for your lasercutter. In line style you want to make all your lines super thin (0.010 mm works fine for me).

#### Engraving
You can usually also engrave:
If you want to engrave lines, make the lines blue or whichever color is required for your lasercutter.
If you want to engrave images, Make them black. Greyscale works, however the results from this are varying as the greyscale colors will not be linear. 
