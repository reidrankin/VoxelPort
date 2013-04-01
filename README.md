VoxelPort
=========

Overview
-----------------

For the original VoxelPort, see VoxelPort (Legacy).
__VoxelPort 2 is a schedule-based teleportation system.__ przerwap and the crack minds of The Voxel Box developed it to create theatrical transports on our server, like boats, hot-air balloons, teleporters and mystic portals that run at fixed times over the course of a Minecraft-day.
__Operating VoxelPort has always been simple:__ Activation zones are defined, named, linked together and then scheduled or configured. What makes VoxelPort unique is that the departures for teleports are flexible, and can be scheduled at regular intervals, or tied to the a specific time-of-day in the Minecraft game.
__This second iteration of VoxelPort introduces lots of new features__ like a no-typing interface for players, instant departures, one-way trips (without having to link to a second VoxelPort), and ticketed travel, all achieved with a bare minimum of server resources. This update makes VoxelPort a wonderful choice for more different kinds of servers than ever before.
__Legacy VoxelPort users will want to be thorough with the documentation this release,__ as VoxelPort's entire command structure has been changed to allow for a far more robust teleport system than before. The good news is that everything starts with one single command: `/vp`

Installing and Configuring VoxelPort
-----------------

Place `VoxelPort.jar` into your server's plugins folder.
Create a file named `admns.txt` (yes, that is the correct spelling!) inside your server's plugins folder. This file will contain a list of the names of people allowed to manage VoxelPorts (all players will be able to use them for travel). Enter the player names of one person per line, case-sensitive, e.g:
```
plusnine 
przerwap
ridgedog
EvilSeph
Featherblade
Ciscog33k
KupoKupo
SorrowL
```
VoxelPort will create its database and configuration files upon server startup.

 + Tip: If you are a Windows user, remember that your OS hides your file extensions from you by default. If your OS is hiding your file names from you, the admns.txt file you create will actually be named admns.txt.txt! It is highly recommended to take appropriate steps to see the proper file extensions in your OS so you know what exactly what files and file names you are working with.

Zones
----------------

Understanding zones in three-dminensional space is key to working with VoxelPort. Here is an example of a ship called "The Prefect" in Triana Harbor on the Voxel Box server. This boat in a three-stop loop from the city of Triana to the city of Aldarin Bay, down to the Lemuria Lowlands and back up to Triana. The coordinate range for this boat is highlighted in the screenshot at right:
 + `/vp point`: Marks one of two points needed to create a VoxelPort zone. This command uses the block your crosshair is pointed at. Find the opposite corner of your desired zone, aim the cursor at that block, and use the `/vp point` command a second time. You will get a message confirming when you have succesfully defined a zone by two corners.
Note: Your players will have to stay within the defined boundaries of the VoxelPort until their departure occurs, so it's best to give a little leeway in your definition for them to move around the ship / vessel, jump or do other things while they wait for departure.
 + `/vp create [name]`: Once you have defined a zone with two points, you can create a VoxelPort for it by naming it with this command.
Note: When you create a VoxelPort, it is loaded into VoxelPort's "working slot". This allows you to do several commands that apply to this VoxelPort without re-typing its name.
 + `/vp arrive [name]`: Sets the arrival point that will be used when other VoxelPorts use the current VoxelPort as a destination.
Note: This command can be issued without a VoxelPort name, and will apply to the VoxelPort in the "working slot".
 + *** NEW *** /vp redstonekey: - Relying on your first '/vp point' will allow the point to act as a redstone trigger. When the block is powered by a button, the user will be teleported to the port's destination. Instant teleport must be set for this to work.
 + *** UPDATED *** /vp set: Load the VoxelPort you're standing in or looking at into the working slot. This command is great for touching up the options, destinations or dispatch schedules of your existing VoxelPorts!
 + *** NEW *** /vp zone [name]: This command inserts the currently defined VoxelPort zone into the VoxelPort named, allowing you to adjust and redefine the activation area for your VoxelPorts without deleting and re-creating them.

Charting Destinations
----------------

There are now three ways of setting a destination point for a VoxelPort:
 + `/vp target`: Sets the VoxelPort in the "working slot"'s destination to your current location.
 + `/vp target [name-origin]`: Sets the declared VoxelPort's destination to your current location.
   + These commands are great for short-range teleports or instances where you wish your VoxelPort to be a one-way trip!
 + `/vp target [name-origin] [name-destination]`: Sets the one VoxelPort's destination to be the arrival point set for the another VoxelPort. This command is best suited for round-trip (or more complicated routing setups).

*** NEW *** Multi-world Destinations
----------------

VoxelPort supports multi-worlds!
 + `/vp targetworld [name-origin] [targetworld] [default/nether]`: Sets the VoxelPort's destination to the origin point of the world specified. If the world targeted does not exist, it will be created when you travel to it for the first time. Once you are in your new world, you can set VoxelPorts going between your two (or more!) worlds more easily. "default" worlds will be green terrain-seeded worlds, while "nether" worlds will generate a world with nether-terrain and a red sky.

Dispatch Schedules
----------------

VoxelPort uses Minecraft's 0-24000 time scale (1000 units being one Minecraft-"hour" or roughly 25 seconds of a player's lifetime). 0 is midnight, 6000 is 6am/6h, 12000 is noon, and 18000 is 6pm/18h.
 + Note: Before you add dispatches to your first VoxelPorts, you will need to restart or reload your server. Until there are VoxelPorts to load, VoxelPort does not begin its clock-timer. Once you've zoned and created your first VoxelPorts, restart the server before adding dispatches. Otherwise you will have difficulty with the following commands!
 + /vp disp [name] [0-24000]: Adds a single timed dispatch to the VoxelPort using the 24000 time scale. Use this for rare transports or events that happen daily. (like sunset and sunrise)
   + Note: This command can be used without a name declaration to affect the VoxelPort loaded into the "working slot".
 + /vp disp [name] clear: Clears a VoxelPort's entire dispatch schedule.
   + Note: This command can be used without a name declaration to affect the VoxelPort loaded into the "working slot".
 + /vp gendisp [name] [interval] [starttime]: Generates a regular dispatch schedule for a VoxelPort. If you declare only an only interval without a start time, VoxelPort will begin the first interval at midnight (0).
 + /vp instaport [name] [true/false]: When this is set to true, any passenger detected holding a ticket in their hand will be transported at the next available VoxelPort time. This defaults to false. This feature can be used to great effect over short ranges where chunks do not have to reload, really giving the feeling of "teleportation".
   + Note: This command can be used without a name declaration to affect the VoxelPort loaded into the "working slot".

Ticketing System
---------------

VoxelPort now features an optional item-based ticket system. The item used for your VoxelPort ticket is configurable. By default, the item used for a VoxelPort Ticket is Leather Hide (item id 334 / VoxelTicket on The Voxel Box).
 + /vp requireticket [name] [true/false]: When this is set to true, only passengers holding a valid ticket in their hand will be able to activate and use the VoxelPort. The ticket will be consumed when the VoxelPort activates, queueing the player to be transported at the next departure. This defaults to false.
   + Note: This command can be used without a name declaration to affect the VoxelPort loaded into the "working slot".
   + Note: Players who have their tickets accepted for departure and then leave the VoxelPort will lose their ticket!


([More...](http://www.voxelwiki.com/minecraft/VoxelPort_2))












