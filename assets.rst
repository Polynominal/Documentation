.. |folder| image:: assets/structure/folder.png
.. |file| image:: assets/structure/file.png

Assets
******

This portion of the guide is specifically designed to tell you all about where and how you should keep your assets and how to minimise the space your assets take.

Maps
----
Maps are independent objects, meaning that there are no dynamic links outside of them.

This in turn means that any object outside of the map cannot be used to enchance or add to the map, however there are cases where some outside elements are required.
One of them is other maps, if you don't want to include a map as a child you need to include it in **either maps/** or **inbuilt_maps/** folders.

The maps are neatly divided into their file structure as described here :ref:`FileStructure`.

It is important to notice that resources are close to the same syntax:

|folder| resources

    |folder| image

    |folder| spritesheets

    |folder| modules

    |folder| skyboxes

    |folder| sound [reserved]

    |folder| special [reserved]

The folder spritesheet and image will look **identical**, however the reason behind this is that the spritesheets are named the same as their parent images.

So if you have an image called *I-am-an-image.png* then the spritesheet will be called:  *I-am-an-image.png*, the extension wont change.

This is done deliberately to allow for appropriate naming and prevent name clashes.

.. note::

    All saved files are actually made up of readable text so if you want to you can just *write* the map.

    This means that if you want to merge a spritesheet you can just copy ones content into another, but beware that there may be some internal name clashes.



Inheritance
-----------

the inheritance law applies to all maps and states the following:

**All children have the same resources as their parent.**

Therefore if you have a child of a map it will be able to use all the resources found in its parent.

This is moderated by you, meaning that if a resource is copied you will have to delete it to save space, it is important that you do this to ensure small file size.

.. note::
    Lucidity will **NEVER** delete files that you make.

    If you notice that Lucidity is in any way removing files other than *.troll* files, make sure to check the modules you are using.

Save data
---------

**How does it work?**

Save data works by scanning through the registry of the modules and saving them, when loading the registry matches that of the saved modules.

The data is recorded in either a save file or *one_use.troll*, which is used for once only loads.

One use
=======

The *one_use.troll* is created before you switch a state, in most cases a transition from Play to Battle.

However the save file is removed on load, this is done by checking its extension, if it has a *.troll* it will be removed.

**I found a 'one_use.troll' in my saves, why is that?**

The *one_use.troll* was created to allow for loading just in case you crash when switching states, this allows for an easy recovery and prevents loss of data.

Modules
-------

When you pick a module from the *Resources* pool, it will always copy in full, in other words it will copy the module and all the files in its folder but ignore any derivatives.

Derivatives
===========

When picking a derivative for the module it will only copy the single derivative and its dependencies.

As afro mentioned in modules, everything will be copied in the derivative's own folder.
