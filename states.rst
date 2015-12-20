States
******

The states used are from `Hump Gamestate <http://hump.readthedocs.org/en/latest/gamestate.html>`_, so make sure to read its documentation before you start.
To get the current gamestate use:
``Gamestate.current()``

**Gamestates Editor,Play and Battle have the following in common**

Variables
---------

    *x,y*

    The current positions of the camera.

    *current_zmap*

    the active zmap.

    *scale*

    *layers*

        Layers module link.

    *textureManager*

        Texture manager module link.

    *textureMapper*

        Texture mapper module link.

    *imageAdmin*

        The image module link.

    *shapeAdmin*

        Shape module link.

    *moduleAdmin*

        Module Admin link.

    *textAdmin*

        Text module link.

    *tool*

        The current active tool.

    *mainCanvas*

        The main canvas where everything except UI is drawn upon.

    *ui_keyControler*

        The ui key controller

    *CamerBox*

        The camera box HC shape.

    *ui*

        The ``ui_package`` used.

Functions
---------

.. function:: worldPos(x,y)

    :param numbers x,y:  Position on screen
    :returns numbers x,y: Position in the world.

.. function:: camPos(x,y)

    :param: floats x.y: Position in the world
    :returns floats x,y: Position on the camera.

.. function:: render()

    Draws all of the items on the mainCanvas.

.. function:: getTween()

    :returns: Flux group; The flux group used for tweens within the gamestate.

.. function:: parse()

    :returns table: Editor items including shapes and modules etc.

Editor
------

.. function:: Editor:renderRuler()

   :returns: draws the ruler on the ruler canvas.

.. function:: Editor:getMousePos()

    :returns floats x,y: the mouse position.


.. function:: Editor:getMod()

    :returns floats x,y: modifiers for parallax from the current layer.

.. function:: Editor:remakeCamera()

    Recreates the camera shape, use it if you are setting scale etc, no need to use it when changing position.

.. function:: Editor:navigation(KeyControler keycontrol1,keyControler keycontrol2,float dt)

    Controls all of the navigation.

.. function:: Editor:save(name)

    :param string name: saves the map with the name.

.. function:: Editor:run()

    Runs the game into Play mode.

.. function:: Editor:load(name)

    :param string name: loads the map at name

.. function:: Editor:refreshImageList()

    Refreshes the image list if it is open.

.. function::  Editor:getMapDir(tail)

    :param string tail: the tail string such as "/children/"
    :returns string: directory.

.. function:: Editor:pickImage(function)

    :param: ``function(sheet,quad)``, executed when the appropriate sprite is selected.

.. function:: Editor:pickLayer(function)

    :param: ``function(zmap,layer)``, executed when the appropriate layer is selected.

.. function:: Editor:pickSound(function) -- WORK IN PROGRESS!

    :param: ``function(name,dir)``, executed when the appropriate sound is selected.

.. function:: Editor:getUi()

    :returns: the ui package used in the state.

.. function:: Editor:newMap(name)

    :param string name: the name of the new map.


Variables:
==========

    *dock*

        the Dock ui portion.

    *dropDown*

        The drop down menu.

    *quickSave*

        The quick save timer if it reaches zero the game is saved.

    *mx,my*

        The mouse position.

    *all_active*

        All of the active items, within and outside of CameraBox


Play
----

Play state is the main state, it is the platformer part of the game.

Functions
=========

.. function:: Play:getPlayer()

    :returns: the active camera holder, aka the player.

.. function:: Play:getScenes(map,initial)

    :param string map: the map to query (optional).

    :param table initial: the initial table filled with maps or empty (optional)

    :returns table scenes: the table full of scene locations in string format.

.. function:: Play:OnBattleMode(team,player,ownTeam,cards)

    :param table team: table with Ghosts, max: 5.

    :param table player: the player instance

    :param table ownTeam: Optional, the players team.

    :param table cards: Optional, the players cards.


The table full of Ghosts should look like this::

 {
    {name = string name
    dir = string directory
    _host = ghost -- Instance of loadGhost data}
 }


.. function:: Play:save(string name, Team)

    :params string name: The name of the save.
    :params Team: The team, same syntax as :func:`OnBattleMode`

.. function:: Play:tweenCapture()

    It is the capture tween, the effect that happens when you are about to enter the Battle mode.

.. function:: Play:clampCamera()

    :returns Camera: The camera unique to the current game.

.. function:: Play:getCamera()

    :returns Camera: The camera unique to the game, Doesn't block the existing one though.

.. function:: Play:releaseCamera()

    releases the camera.

.. function:: Play:switchMap(dir)

    :param string dir: the directory of the map.

Camera
======

The camera is a new class created when you either :func:`Play:getCamera` or :func:`Play:releaseCamera`

* Variables

 *x,y* the map position of the Camera.

* Functions

.. function:: Cam:updateCamera()

    :returns numbers x,y: new x and y positions in the world.

You must redefine this function to set the appropriate positions.


**Example usage**::

    local game = Gamestate.current()

    local Cam = game:clampCamera(true)
    local finished = false
    Cam.modx = 0
    Cam.mody = 0
    game.tweenGroup:to(Cam,2,{modx = 100})
    function Cam:updateCamera(dt)
        local x,y = self.x + self.modx,self.y + self.mody
        return x,y
    end

    -- some where else when finish = true,

    if finish then
        game.tweenGroup:to(Cam,2,{modx = 0}):oncomplete(function()
            game:releaseCamera()
        end)
    end


Battle
------
Battle is the RPG part of the game,

Battle has little to no functions at the moment, but please note that is soon subject to change.

As of right now it has little modding compatibility and will soon be rewritten.



MainMenu
--------

The main menu doesn't share the afro mentioned functions but instead has the following:

.. function:: pralaxPos(factor)

    :param factor: the parallax factor.
    :returns numbers x,y: the new position.


As you may have guessed MainMenu is currently off-limits too, however that is subject to change.

Options and Menu
================

Options is a sub-state of Menu while Menu itself is a state that is found across the states.

Menu will be used in most states to allow for navigation, just press ESC.


