Inbuilt Packages
****************

The inbuilt packages are used only internally but feel free to use them although please beware of modifying them as it will have global effects.


User interface
--------------
The user interface can be accesed in two ways:

Use this to create a new UI package, use this in exceptional circumstances.

.. function:: ui_package:new()

    :returns ui_package:

OR

This is the main method of accessing UI

`Gamestate.current().ui`

Parenting
=========

The UI is based on a parent and child system, inother words if you create a button it is either the child of the UI itself or a frame or another item.

The use of this system should come intuitively.

All of the ui elements with the exception of a few follow this syntax:

::

 ui:add<Item>(parent,x,y,width,height,...)

**Example**::

 -- Creating a frame with a button on it.
 local width,height = 200,200
 local Frame = ui:addFrame(nil,400,300,width,height)

 local doneButton = ui:addButton(frame,5,20,100,100)
 doneButton:setText("Done")
 -- this will create a button at 405 and 320; the 5,20 coords are relative.
 doneButton.OnClick = function()
    -- this will remove the Frame AND the button.
    Frame:remove()
 end

The parent system is cumulative meaning that you can have a parent who's child is also a parent and so on, this is also used internally especially in lists.

Items
=====
Here are all the currently implemented items and their functions.

- Frame

    .. function:: ui:addFrame([parent or name],x,y,width,height,[parent])

        :returns Frame: the frame item.

    .. function:: frame:addCloseButton(function)

        :params function: the function executed when the X button is pressed.

    .. function:: frame:setShape(shape)

        :params HardonCollider shape: the shape of the new frame.

    .. function:: frame:setImage(image)

        :params love2DImage: the image to draw on the frame

    .. function:: frame:setTooltip(toolTip, delay)

        :params toolTip: the pre-created tooltip

        :params number delay: time before the tooltip shows up.

    .. function:: frame:addTooltip(text,delay)

        :params string text: the text the tooltip will display

        :params number delay: time before the tooltip shows up

    .. function:: frame:setSize(width,height)

    .. function:: frame:setTexture(image.wrap)

        :params Love2DImage: the image for the texture.

        :params wrap:  the wrap mode, see: `Wrap Modes <https://love2d.org/wiki/WrapMode>`_.

    .. function:: frame:setHeader(name,width,height.color)

        :params table color: color = {r,g,b,a}

    **Important Variables**:

        dontDrawSelf ; boolean, prevents the frame from being drawn.

    **Events**:

       `OnDrawTop(self)`

- Button

    .. function:: button:setTooltip(toolTip, delay)

        :params toolTip: the pre made tooltip

    .. function:: button:addTooltip(text,delay)

        :params string text: the text

        :params delay: the time required for the tooltip to appear.

    .. function:: button:setShape(shape)

        :params HardonCollider shape: the shape of the new button

    .. function:: button:setSize(width,height)

    .. function:: button:setTexture(image.wrap)

        :params Love2DImage: the image for the texture.

        :params wrap:  the wrap mode, see: `Wrap Modes <https://love2d.org/wiki/WrapMode>`_.

    **Important Variables**:

        dontDrawB ; boolean, prevents drawing of image on button.

        dontDrawC ; boolean, prevents drawing of collision.

        dontDrawText ; boolean, prevents drawing text.

        dontDrawActive ; boolean, prevents drawing active/inactive gestures.



- Text

    .. function:: ui:addText([parent],x,y,text,[font],[color])

        :params font: love2d font for the text.

    .. function:: text:setText(text,[font],[color])

    **Events**:

        DrawPrefix(x,y)

        DrawSuffix(x,y)

- Costum

    Experimental, only use if you absolutely need to.

    .. function:: ui:addCostum(x,y,colision)

    Only has `draw` , `getColision` and `update`


- Tooltip

    .. function:: ui:addTooltip([parent],text,mode,[font],[color])

    .. function:: tooltip:setCenter(cx,cy,px,py)

        :params numbers cx,cy: the center x and y

        :params numbers px,py: the parent x and y

    .. function:: tooltip:setPoints()

     Resets the points.

- Menu

    .. function:: ui:addMenu([parent],x,y,[table])

        :params table: table filled in as such:

        ::

         {  {"Run",function() salf:save() salf:run() end,10}    }
         -- Syntax:
         { {Text,function,gap} }


    .. function:: menu:addChoice(text,function)

    .. function:: menu:addItem(item, function)

        :params ui_item item: A UI item to be an item within the list.

    .. function:: menu:clear()

    .. function:: menu:refresh()

- Slider

    .. function:: ui:addSlider([parent],x,y,width,height,[mode])

        :params string mode: horizontal or vertical, horiz or vert for short.

    .. function:: slider:getFloat()

        :returns: gets the float value in terms of percent of.

    .. function:: slider:setFloat(d)

        :params float d: the float number of d, use to set the current percentage.

    .. function:: slider:setRange(min,max,isInteger)

        :params bool isInteger: if you want integer only values.

    .. function:: slider:getStepSizePX()

        :returns number: the number of pixels per step.

    .. function:: slider:getValue()

        :returns number: the current value so if min = 100, max = 200 will return value inbetween.

    .. function:: slider:setValue(val)

        :params number val: the value that lies within min and max set earlier.

    .. function:: slider:OnMove(x,y)

    **Event**:

        `OnChange(value)`

- Textinput

    .. function:: ui:addTextinput([parent],x,y,width,height,text)

    .. function:: textinput:getLocalText()

    .. function:: textinput:getPosFromCords(x,y)

        :params numbers x,y: the local coordinates

        Sets the position of the indicator at X and Y.

    .. function:: textinput:resetPos()

    .. function:: textinput:setMultiline()

        Enables multi-line.

    .. function:: textinput:getText()

        :returns text: the concatenated text.

    .. function:: textinput:setAllowed(a)

        :params table a: the table full of strings you don't want to see in your input.

    .. function:: textinput:moveLine(bool)

        :params bool: false for down, true for up

    .. function:: textinput:setText(text)

        :params string text: the text as a long string.

    **Events**:

        `OnChange(text)`


- List

    .. function:: ui:addList([parent],x,y,width,height,[items],[mode])

        :params bool [mode]: True if you want horizontal mode.

    .. function:: list:setHeader(text)

    .. function:: list:addChoice(text,function)

    .. function:: list:addItem(item,position)

        :params ui_Item item:

    .. function:: list:refresh()

    .. function:: list:setMode(horizontal,vertical)

        :params booleans horizontal,vertical:

    .. function:: list:getStencil()

        :returns function:

    .. function:: list:goMax()

        Sets the position to maximum.


    .. function:: list:clear()

    .. function:: list:getLeftOver()

        :returns number: the leftover space at either the sides or top and bottom.

    .. function:: list:removeItem(item)

        :params ui_item item:


- Shared

    .. function:: <item>:getColision()

        :returns HardonCollider shape:

    .. function:: <item>:addItem(item)

        :params ui_item item:

    .. function:: <item>:setInactive(t)

        :params bool t:

    .. function:: <item>:moveTo(x,y)

    .. function:: <item>:remove()

    **Events**:

        `OnUpdate(dt)`

        `OnDraw(self)`

        `OnFocusLost()`

        `OnFocus()`

        `OnMove(x,y)` [*]_

 .. [*] This might be used internally so be careful when assigning.


    **Important Variables**:

        dontDraw  = boolean; do not draw self.

        inList    = boolean; is it in the list?


.. note::
    Some items have internal items:

        Slider: sliderButton [button]

        Menu, List, textInput: mainFrame [frame]



- Base[UI]

    .. function:: ui:getItemCount()

    .. function:: ui:clear()

    .. function:: ui:getZorder()

    .. function:: ui:draw(debug)

    .. function:: ui:update(dt)

    .. function:: ui:mousepressedList(x,y,button)

    .. function:: ui:textinput(t)

    .. function:: ui:getmxb()

        :returns HardonCollider_shape: the shape used for the mouse.

    .. function:: ui:init(Collider)

    .. function:: ui:getFont()

        :returns love2Dfont:

    .. function:: ui:setMousePos(x,y)

    .. function:: ui:setTitleIncrement(degree)

    .. function:: ui:setLeftClick(main,alt)

        :params booleans main,alt: the main and alt left clicks.

        Run at update.

    .. function:: ui:setRightClick(main,alt)

        :params booleans main,alt: the main and alt right clicks.

        Run at update.

    .. function:: ui:setMiddleMouse(down,up)

        :params booleans down,up: the down and up for middle mouse

        Run at update.

    .. function:: ui:setFont(font)

        :params Love2dFont font:


.. note::
    Some internal use functions are omitted.


Editor specific
---------------

Module admin
============

**Module admin primarily designed for internal usage, please use with care!**

to get module admin::

 local ma = Gamestate.current().moduleAdmin

.. function:: ma:newModule(directory,name)

    :returns module:

.. function:: ma:seekInstance(module,own)

    :params numbers module,own: the registry numbers that the module and instance owns.

    :returns instance:

.. function:: ma:getModules()

    :returns: table of modules.

.. function:: ma:getModulesFrom(dir,make)

    :params string dir: the directory where the modules are.

    :params boolean make: if the module should be created.

    :returns table: in format {dir = string,name = string,derivatives = table}

.. function:: ma:make(table)

    :params table: in format {dir = string,name = string,derivatives = table}

.. function:: ma:save(map,[source or filter].parents)

    :params string map:

    :params string source:

    :params filter: the filter function(module), return module.

    :params table parents: Use: :func:`getParents`


.. function:: ma:saveModule(module,map,source,parents)

    :params Module module:

    :params string map:

    :params string source: source directory.

    :params table parents: Use: :func:`getParents`

    :returns table: the table with the saved module.

.. function:: ma:checkModule(src,name,instances,parents)

    :params src: source directory

    :params name: name of the module

    :params table instances: the modules instances

    :params table parents: Use: :func:`getParents`


.. function:: ma:load(map,table,parents)

    :params string map:

    :params table: the table where all of the modules were saved into.

    :params table parents: Use: :func:`getParents`

.. function:: ma:getInstances()

    :returns table: of instances

.. function:: ma:clear()

Module
++++++

.. function:: module:seek(derivative)

    :params string derivative: the name of the derivative.

.. function:: module:getInstances()

    :returns table instances:

.. function:: module:addDeriv(dir,name)

    :params string dir: the source directory of the derivative

    :patams string name: the name of the derivative.

.. function:: module:addInstance(name,x,y,zmap)

    :params string name: the name of the source derivative

    :params numbers x,y: the position in game world

    :params number zmap: the z position in game world

    :returns instance:

.. function:: module:remove()


Trigger admin
=============
To get the trigger admin handle::

 local ta = Gamestate.current().triggerAdmin()

.. function:: ta:setEnviroment(global)

   :prams table global: the pairs table with globals.
    :returns table enviroment: use in coalition with setfenv.

.. function:: ta:getEnviroment()

    :returns table enviroment:

.. function:: ta:load(t)

    :params table t: the table with saved triggers.

.. function:: ta:getModes()

    :returns table: table of strings of trigger modes.

.. function:: ta:exec(function,var)

    :params function: a function to execute

    :params var: the self variable.

.. function:: ta:addTrigger(item)

    :params Editor_item item: the item that exists within the editor.

    :returns Trigger: the trigger module used below.

Trigger
+++++++

.. function:: Trigger:setActiv(mode,fns)

    :params string mode: the mode of action

    :params function fns: the function to execute.

.. function:: Trigger:save()

    :returns table:

.. function:: Trigger:load(t)

    :params table t: the table previously made using :func:`Trigger:save`


Image admin
===========
To get the image admin use::

 local ia = Gamestate.current().imageAdmin


.. function:: ia:addImage(sheet,quad,x,y,rotation,scale_x,scale_y)

    :params Sheet sheet: the sheet from texture manager.

    :params Quad quad: from the sheet.

    :returns Image:

.. function:: ia:clear()

.. function:: ia:getItems()

.. function:: ia:save()

.. function:: ia:load(tables,tm,gamestate)

    :params TextureManager tm: link to texture manager

    :params gamestate: the current gamestate

Image
+++++

.. function:: Image:unpack()

.. function:: Image:mirror()

.. function:: Image:flip()

.. function:: Image:setScale(sx,sy)

.. function:: Image:setZmap(z)

.. function:: Image:setRotation(r)

    :params number r: In radians!

.. function:: Image:setMod(modx,mody)

    :params numbers modx,mody: the modifiers in x and y directions, used for parallax.

.. function:: Image:makeColision()

.. function:: Image:update(dt)

.. function:: Image:getPos()

    :returns numbers x,y: position

.. function:: Image:rotate(r)

    :params number r: in radians

.. function:: Image:draw(DEBUG)

    :params bool DEBUG: debug for drawing wireframe etc

.. function:: Image:remove()

.. function:: Image:OnMenu(menu,ui)

    :params ui_item menu:

    :params ui_package ui:


Shape admin
===========
To get the shape admin do::

 local sa = Gamestate.current().shapeAdmin

.. function:: sa:newRectangle(mode,x,y,width,height,color)

    :params string mode: the mode, "fill" or "line"

    :returns Rectangle:

.. function:: sa:newCircle(mode,x,y,r,color)

    :params string mode: "fill" or "line"

    :returns Circle:

.. function:: sa:newPolygon(mode,x,y,points,color)

    :params string mode: "fill" or "line"

    :params table points: the table full of points eg {x,y,x2,y2}

    :returns Polygon:

.. function:: sa:newLine(color,x,y)

    :returns Line:

Rectangle
+++++++++

    .. function:: rectangle:setPointOfCreation(x,y)

    :params numbers x,y: the position of creation.

Circle
++++++

    .. function:: circle:setRadius(r)

    :params number r: Radius in radians.


Polygon
+++++++

    .. function:: polygon:setPoints(points)

    :params table points:


Shared
++++++

    .. function:: <item>:unpack()

        :returns table: table of data from the shape that can be saved using Tserial.

    .. function:: <item>:OnCopy()

    .. function:: <item>:setMod(px,py)

        :params numbers px,py: the x and y modifiers

    .. function:: <item>:getColision()

        :returns HardonCollider shape:

    .. function:: <item>:removeTexture()

    .. function:: <item>:setTexture(sheet,quad)

        :params Sheet sheet:

        :params string quad: the name of the quad.

    .. function:: <item>:update(dt)

    .. function:: <item>:draw(debug)

    .. function:: <item>:makeColision()

    .. function:: <item>:remove()

    .. function:: <item>:OnRightClick(menu,ui,editor)

        same as `OnMenu` just slightly changed syntax

Line
++++
    .. function:: line:addPoint(x,y)

    .. function:: line:addTempPoint(x,y)

        :params numbers x,y: the x and y position of the temporary point.

    .. function:: line:update(key,key2)

        :params booleans key,key2: key is for left click and key2 is for middle click for edit mode.

    .. function:: line:makeSilent(x)

        :params bool x: sets silent mode.

    .. function:: line:remove()

    .. function:: line:makeColision()

    .. function:: line:draw()

    .. function:: line:checkPoints()

    .. function:: line:returnPoints()

        :returns table: of points, use in coalition with :func:`polygon:setPoints`

Textures
========

There are two modules for textures:

Texture manager
+++++++++++++++
::

 local tm = Gamestate.current().textureManager


.. note::
    functions that start with  `pr`  are used for once only loads.

.. function:: tm:newSheet(name,image)

    :params string name: of the new sheet.

    :params love2dImage image:

    :returns Sheet:

.. function:: tm:prNewSheet(name,image)

    :returns Sheet: Does NOT add it to the active sheets.

.. function:: tm:remove([sheet or sheet_name])

    :params Sheet sheet:

    :params string sheet_name: the name of the sheet

.. function:: tm:addSheet(sheet)

    :param Sheet sheet:

.. function:: tm:seek(sheet)

    :params string sheet: the name of the sheet

    :returns Sheet:

.. function:: tm:save(map,parents)

    :params string map:

    :params table parents: Use: :func:`getParents`

.. function:: tm:load(map,parents)

    :params string map:

    :params table parents: Use: :func:`getParents`

.. function:: tm:unpack()

    :returns table: to save using Tserial.

.. function:: tm:clear()


.. function:: tm:prLoad(map)

    :param string map:

Sheet
+++++

.. function:: sheet:addQuad(name,x,y,w,h,delay,frame1,frame2)

    :params numbers x,y,w,h: position and dimensions

    :params delay,frame1,frame2: the beginning and end frames and the delay between them.

.. function:: sheet:getImage()

    :returns love2DImage:

.. function:: sheet:seek(s,remove)

    :params string s: the name of the quad

    :params bool remove: if you want to remove the sheet; pass true

.. function:: sheet:getQuads()

    :returns table,image: full of quads, then the sheets image.

.. function:: sheet:getQuad(name)

    :returns Love2dQuad: the individual quad.

.. function:: sheet:save()

.. function:: sheet:remove()

.. function:: sheet:applyEdit()

Texture mapper
++++++++++++++
::

 local tmap = Gamestate.current().textureMapper


.. function:: tmap:new(shape,img.quad)

    :params Shape shape: shapeAdmin shape.

    :params Love2DImage img:

    :params Quad quad:

.. function:: tmap:setImage(img,quad)

    :params Love2DImage img:

    :params Quad quad:

.. function:: tmap:update(dt)

.. function:: tmap:updateCol()

    Call when the points of your Shape changes.

.. function:: tmap:draw(sx,sy)

    :params numbers sx,sy: scalex and scaley

.. function:: tmap:remove()

Text admin
==========

to get text admin::

 local ta = Gamestate.current().textAdmin

.. function:: ta:addText(x,y,z,font)

    :params numbers x,y,z: coordinates.

    :params love2DFont font:

    :returns Text:

.. function:: ta:load(data)

    :params: table of saved text.

Text
++++

.. function:: Text:setText(t,font)

    :params string t: the text

    :params love2DFont: the font

The Text inherits the following functions:

``getColision``, ``draw``, ``update``, ``OnMenu``, ``OnMenu``, ``OnCopy``, ``setMod``, ``save``, ``remove``

**However it does not include ``load`` !**


layers
======

To manage z coordinates I decided to produce a layer system, it is supposed to replicate the layer method just like in that of graphics production software including photoshop etc.

Obviously it is still missing a bulk of features such as the ability to add effects and drawing methods, but this is coming soon when I sort out some performance issues.

To get layers::

 local layers = Gamestate.current().layers


.. function:: layers:update(dt)

    :params number dt: delta time.

.. function:: layers:clear()

.. function:: layers:unpack(zmap)

    :params number zmap: the zmap of the target layer.

.. function:: layers:save()

    :returns table: the table with all the saved data.

.. function:: layers:load(a)

    :params table a: the table retrieved from :func:`layers:save`

.. function:: layers:getRange()

    :returns numbers min,max: the range of z cords in use.

.. function:: layers:seek(zmap)

    :params number zmap: the z coord of the target layer.

.. function:: layers:removeLayer([layer or zmap])

    :params Layer layer:

    :params number zmap: the z coord of the layer.

.. function:: layers:move(l,z)

    :params Layer l:

    :params number z: the new z cordinate.

.. function:: layers:moveLayers(old,new)

.. function:: layers:addLayer(name,zmap,modx,mody,col,sound,transp)

    :params stirng name: the identifying name of the layer.

    :params numbers zmap,modx,mody: the z coord and modifier position.

    :params booleans col,sound:

    :params number transp: transparency, out of 255

    :returns Layer:

Layer
+++++

.. function:: Layer:getMod()

    :returns numbers modx,mody:

.. function:: Layer:setParalax(x,y)

    :params numbers x,y: the modifiers

.. function:: Layer:setColision(col)

    :params boolean col: if the layer enables collision.

.. function:: Layer:setName(name)

    :params string name: the new name of the layer.

.. function:: Layer:setData(name,zmap,modx,mody,col,sound,transp)

    Same params as :func:`layers:addLayer`

.. function:: Layer:unpack()

    :returns: name,zmap,modx,mody,col,sound,transp


Map admin
---------

The map admin is a table of functions used for drawing and parsing the map.

Be very careful when modifying these functions.

.. note::
    The self parameter in the functions bellow relates to a State such as Play,Editor or Battle.

.. function:: mapAdmin.parse(active,passive,self)

    :params table active: HardonCollider active shapes.

    :params table passive:  HardonCollider passive shapes.

    :returns table: active shapes.

.. function:: mapAdmin.scanModules(self,collider,ret)

    :params HardonCollider collider:

    :params table ret: return table.

    :returns table: of modules.

.. function:: mapAdmin.updateSingle(shape,dt)

    :params Instance shape: the instance as found from parse/parseSingle

.. function:: mapAdmin.parseHead(self)

    parses the head portion, use for Editor only.

.. function:: mapAdmin.parseSingle(self,shape,dt,rt,[cond or filter])

    :params HardonCollider_shape shape:

    :params table rt: return table for priority instances.

    :params boolean cond: if the instance should be updated or not.

    :params function filter: filter that either allows an instance through or not

.. function:: mapAdmin.parseTail(self,dt)

    :params number dt: delta time.

    Used for Editor only.

.. function:: mapAdmin.draw_visible(self,zmap,current_zmap)

    :params none zmap: used for legacy.

    :params number current_zmap: the current zmap.

.. function:: mapAdmin.mousepressed(self,mxb,x,y,b)

    :params mxb: use :func:`ui:getmxb`

    :params x,y: position of the click

    :params string b: the keyConstant.

.. function:: mapAdmin.updateCol(self,mxb)

    :params mxb: use :func:`ui:getmxb`

.. function:: mapAdmin.shapeCol(self,mxb,dt,a,b)

     :params mxb: use :func:`ui:getmxb`

     :params HardonCollider_shapes a,b: the shapes colliding

.. function:: mapAdmin.shapeStop(self,mxb,dt,a,b)

     :params mxb: use :func:`ui:getmxb`

     :params HardonCollider_shapes a,b: the shapes colliding

.. function:: mapAdmin.clear(collider,self)

    :params HardonCollider collider:

.. function:: mapAdmin.save(self,name,items)

    :params string name: the map name.

    :params table items: a table of instances.


.. function:: mapAdmin.load(self,file)

    :params string file: the filename of the map.



