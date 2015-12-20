Global variables
################

Functions
*********
.. function:: getPackageAlt()

    :returns string _PACKAGE: the current location of the file.

.. function::  getEnv()

Gets the current environment used for setfenv()

.. function:: copyFiles(string dir,string dest)

copies files from one directory to the other, recursively.

.. function::  saveLog()

saves the log file to %appdata%/LOG

.. function::  RCtoWH(userData image,int rows,int colums)

converts rows and columns to frame dimensions.

.. function::  printStats(float x,float y)

print statistics at x,y

.. function:: loopRange(var root,float range,string name,float speed, string mode)

short hand for a recursive tween.

.. function::  parseColor(string t)

used for parsing color from text as such; "255,255,255,255"

.. function::  checkPlayerCol(HC shape a,HC shape b)

checks the shapes type and returns player and part and other

.. function::  tableLenght(table t)

returns table lenght of a non-indexed table.

.. function::  findDistance(float x,float y)

finds the distance between two points

.. function::  findDimensions((HC shape or float x),float y,float x1,float y1)

.. function::  drawRelease()

draws overlay of version

.. function::  incrementPos(float x,float y,float ofx,float ofy,float degree)

allows for locking to grid of cordinates.

.. function::  showFPS()

shows fps on the screen

.. function::  inRange(float x,float item,float y)

returns boolean if item is in range of x and y

.. function::  inRangeHigher(...)

same as inRange, but returns true if it equals to higher.

.. function::  inRangeLower(...)

same as inRange, but returns true if it equals to lower.

.. function::  hsvToRgb(float h, float s float v)

converts HSV to RGB color space, returns table: {r,g,b}

.. function::  MinMaxFromTable(table)

returns the maximum numeric value from a table.

.. function::  crop(image,imagex,imagey,fw,fh,scalex,scaley,directon)**

crops an image and returns an image as result

.. function::  removeFromTable(table,item)

.. function::  mergeTable(table1,table2,mode)

Modes: [add, force] add will add the values while force will set it.

.. function::  getFactors(float number)

.. function::  nokey()

empty key

.. function::  keyboardpress(key,block)

key is the name of the key, block overrides LOCKCONTROLS

.. function::  mousepress(key,block)

.. function::  gamepadpress(joystick,key,block)

experimental.

.. function::  findMap(name)

finds a map on the top layer, aka maps/ and inbuilt_maps/

.. function::  saveGame(string name,optional map)

saves the game.

.. function::  getSaves()

returns saves in format:
::

 {
    name = string,
    mapName = string, Note: only the first line without path.
    map = string,
    playTime = {h=h,m=n.s=s} Note: broken.
    cards = {} Note: players cards, table of names.
    mobs = {}, Note: players mobs, table of names.
    date = {date,time},

  }

.. function::  saveGameShort(name)

saves a map to playerData.children_maps.

.. function::  loadGameShort(name)

returns the playerData.children_maps table for the map of the name var.

.. function::  loadGame(string name,bool dontswitch )

dont switch prevents the switching of state, name is the savefile name.

.. function::  queryKey(string name,KeyControler c,function fn)

returns bool if found, bool isDown, int position in table

.. function::  deepCopy(table)

copies a table, please use deepCopy2 instead

.. function::  deepCopy2(table)

properly copies a table including metatable, recursive.

.. function::  reverseTable(table)

Reverses the table index.

.. function::  precentOf(int full, int current)

same as findPercent, kept for legacy.

.. function::  findItem(mode,(bool or string) name)

finds an item of Mode with the name of Name, searches alongside maps so if mode is "ghost" it will search at
maps/your_map/ghosts and ghosts/

if name is bool then it will return a table all items of the same mode.

Otherwise it will return path, [set, setPath] = if you are looking for a card.

.. function::  getParents(string map,string(optional) tail)

returns a table of parents for a map with string format.

.. function::  imagestencil(function fn)

returns a function within which a shader is applied to render a stencil mask.



Standard lib extensions
***********************
**table.zsort(table t)**

sorts a table by the z index  when a.zmap < b.zmap

**math.round(int number,int decimalPlaces)**

Data
****
**Colors**

Contains defined colors, allows the use of setColor(color), eg setColor(colors.yellow)

defined colors are;

	red,darkRed,

	green,darkGreen

	blue,darkBlue,cyan,

	lightBlue,paleBlue,

	yellow,orange,

	ambient,black,

	gray,lightGray,darkGray,

	violet,white

**debug_text**

table full of the text printed using print(t,t2,..)

**crystals**

table full of crystals from the main menu.

basic,blue,cyan,green,inverted,pink,player,silver

structure is as follows
::

 {
     w = w, (width)
     h = h, (height)
     delay = delay,
     anim = Animation,
     data = {image,w,h,delay}

  }

**effectColors**

Effect data used internally in battle mode.
contains:

    Poison,fire,curse,drown

**stock_effects**

contains stock effects.
::

 {
    jump = {
        image image,
        Animation anim.
    }
 }

**mColors**

contains colors used in battle mode.

**icons**

contains icons as seen here:

**playersMobs**

contains all of the player mobs for the current active run.

**playersCards**

**playerData**
::

 {
   saveName = string,
   essence = int,
   playTime = string,
   children_maps = {},
 }


**keys**

Long table of keys, described here:

**alt_keys**

Long table of keys, alternative edition.

**misc**

Misc settings:
::

 {
    showFps = bool
    scaleFactor = int
    cameraSlide = bool
    cameraSlideB = bool
    battleCamera = bool
    mouseLock = bool
    trapMouse = bool
    textSpeed = int -- Not implemented yet!!
    sfvol = int -- sound effect volume. may be nil at times
    bgmvol = int -- bgm vol, may be nil at times
    voicebol = int -- voice volume, may be nil at times
    mastervol = int -- may be nil at times.
    seenIntro = bool

 }

**video**
Video settings
::

 {
    width = int
    height = int
    trapMouse = bool
    mouseVisible = bool
    flags = {
        fullscreentype = string
        fullscreen = bool
        vsync = bool
        highdpi = bool
        display = int
        borderless = bool
        srgb = bool
    }
 }


States
******
**Intro**

**Credits**

**Editor**

**Battle**

**PlayMap**

Constructors
************
**net**

work in progress do not use.

**Flux**

flux instance. `Documentation
<https://github.com/rxi/flux/>`_.


**Gamestate**

hump gamestate. `Documentation
<http://hump.readthedocs.org/en/latest/gamestate.html>`_.


**Timer**

hump timer, `Documentation
<http://hump.readthedocs.org/en/latest/timer.html>`_.


**Vector**

hump vector, `Documentation
<http://hump.readthedocs.org/en/latest/vector.html>`_.


**HC**

Hardon Collider, `Documentation
<http://vrld.github.io/HardonCollider/>`_.

**ui_package**

the inbuilt UI,

**msgQue**

the message que for npc's and other

**loadGhost**

ghost system, used for loading:

**loadCards**

card system, used for loading:

**keyControl**

controls the keys

**Profiler**
the profiler, `Documentation
<https://github.com/devfirefly/Piefiller>`_.

**Tserial**
packs table to string.
`Documentation
<https://love2d.org/wiki/Tserial>`_.

Other
*****
**eCurrentMap**

    The current map, full length string of the current map directory.

**mapAdmin**

    map admin module.

**MaxCapture**

is part of the capture timer before engagement starts

**playerMaskCategory**

the box2D category for player

**uniBody**

uniBody font to be used alongside love.graphics.newFont

**Glyphs**

Image font used for writing strange text

**basicFrameColor**

**basicButtonColor**

**LOCKCONTROLS**

locks all the controls (bool)

**_RELEASE**

string of version

**SHOWUI**

bool, shows or hides the ui, please use removeHud to remove HUD only works in play mode.

**DEBUG**

bool, enables debug mode

**PROFILER**

bool, allows to profile if P key is pressed

**STATS**

bool, shows stats

**globals**

the global gamestate.

