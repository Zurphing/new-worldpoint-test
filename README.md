# new-worldpoint-test
A test for adding in entirely new warp points to the game. </br>

At least three files must be edited: </br>
.ard of the map you want to make into a warpable save point </br>
70landing.bar </br>
00worldpoint.bin </br>


70landing.bar has two parts that must be edited, the land.list & adding in the appropriate IMGD file in sequential order. May not be required, but name your IMGD file the same room name as the world; so a warp to HB26 should have the IMGD named HB26. </br>

land.list structure: </br>
First 0x4 bytes are BAR type </br>
Next 0x4 bytes are count of warp points. </br>
After that are entries for land.list. </br>

Each entry in land.list is 0x4 bytes long. </br>
0x1 is the "ID" of the warp point </br>
0x2 is the World ID of the warp point </br>
0x3 is the # of warp point it is (This is unrelated to Room ID. If this is the fifth entry for a warp point, pointing to HB26, then its value is equal to 5, for example.). </br>
0x4 is which IMGD to use. Usually -1 from the warp points ID. </br>

IMGD's are loaded in sequential order. </br>

00worldpoint.bin is where the warp points will actually lead to. Warp Points must be located in the same area as the rest of the world. </br>
Example: You can notice that every warp point in Hollow Bastion is all grouped together, no World ID #4 is found anywhere else within the file. </br>

00worldpoint.bin structure: 0x4 bytes long; </br>
0x1 is World ID </br>
0x2 is Room Number </br>
0x3 is set to 0x63, to indicate this is a Save Point. </br>
0x4 purpose unknown, set to 0x00 </br>

Note that you CAN force a warp to an entirely different world, just change the World ID & Room Number, and ensure that warp is near the other warps for a world.
I.E, if you have 5 Hollow Bastion Warps set up, and you want your 5th Warp to lead to Destiny Islands, set World ID to 03 and Room Number to whichever room # you want.
Ensure these 5 are all grouped together, and you can warp in.
Please note however, that the String it will show for the room you're warping into will match the room number of the world you're warping into.
I.E, we warp into World 3 (Destiny Islands) to Room 1 (Main Island).
On the Land Selection screen, when we hover over that warp, it will instead show Room 1's text to be "Dark Depths", which is what Room 01 is in Hollow Bastion.


ARD FILE:
The simplest way to handle this is to add in "Warp Point Spawn"s into an .ard files m_00 spawnscript. </br>
Unpoint the m_00 spawnscript with OpenKH's SpawnScript tool, then copy-paste a block that has "ObjectID: 566", "567", and "568" </br>
These are Sora, Friend1 and Friend2. </br>

Then, under SpawnArgument, change it from whatever it is to 99. This is an argument that afaik, will tell the game that spawnpoint is reserved for warping in from the world map.
</br>

Then repoint the changed m_00.yml file, and import it into your .ard file (or alternatively, patch in the YML via OpenKH). </br>

Once you have your files ready, put them in the appropriate places (70landing.bar & 00worldpoint.bin in the root directory of mod/kh2, and the .ard file in ard/region)


Currently, unsure how to make entries past 35 appear in the "Select a Room" menu. May be related to possible Story Flags?
