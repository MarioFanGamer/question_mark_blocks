             Customisable Question Mark Block
                    by MarioFanGamer
            ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

What do these blocks do?
----------------------------------------------------------
These are pretty customisable question mark-blocks.
With these blocks, you can use pretty true, a near perfect
replica of ?-block without either hijacking the spawn
routine or use these ugly custom ?-blocks (yes, I'm
looking at you, Jagfillit and Roy).
This pack contains following blocks
- question_block_base.asm
- question_block_single.asm
- question_block_double.asm
- question_block_enemy.asm
- question_block_item_box.asm
- question_block_coin.asm
- question_block_egg_single.asm (LX5)
- question_block_egg_double.asm (LX5)
- giant versions of the above
- a shared routine to check for kicked sprites
- an example list
- graphics for the giant blocks
- a patch to fix the egg blocks
- and an object code for item memory dependent ?-blocks
  (to be used with ObjecTool)

----------------------------------------------------------
question_block_base.asm is the base block i.e. every other
block in this pack is including its code.
It must be put in the same folder with the blocks you're
inserting and you can not insert it on your own since it
is depending on other defines as well as a definition.
See below on how to use it

question_block_single.asm is the standard question mark
block i.e. what it does is to spawn a single sprite out of
a block.

question_block_double.asm spawns a different sprite if a
specific RAM address is zero or not (by default the power
up state in order to simulate the flower and cape blocks).

question_block_enemy.asm, on other side, is used to spawn
an enemy sprite which is set to spawn on the earlier
sprite slots (the last two slots are intended for non-
enemy sprites and the side effects can be seen on the
Koopa shell spawned from a ?-block).
Be aware that the latter is sprite memory dependent. Each
of these sprite memory settings have got a max limit of
processing sprites. And if said limit is reached, the
block fails to spawn a sprite.

question_block_egg_single.asm is a block to spawn a Yoshi
egg. They are more limited than the regular blocks because
of the egg's own limitation but that way, you can spawn
these sprites without any problems. You can also set it to
spawn a (baby) Yoshi but remember that the egg colour
determines Yoshi's colour. They also spawn a one up or
whatever you have set in the ASM file if Yoshi already
exists.

question_block_egg_double.asm is like
question_block_double.asm except it spawns (as you might
have guessed) a Yoshi egg.
Note: This one is NOT intended to spawn Yoshi. I don't
think you want to spawn a Yoshi from a power up dependent
block so I included no such option for these blocks.

question_block_item_box.asm is used to put a sprite to the
item box. The sprite number depends on whether you use the
vanilla item box or item box special.
In case of the former, you put the $9E value (that's the
sprite number), though you might want to fix the GFX,
whereas Item Box Special stores the value into $0DC2
directly. Which values you have to put there is defined in
ibstables_xxx.asm.

Link to Item Box GFX Fix:
https://www.smwcentral.net/?p=section&a=details&id=12388

Link to Item Box special:
https://www.smwcentral.net/?p=section&a=details&id=12694

question_block_coin.asm recreates the coin block in its
function. That's how much the code is doing, really.
You could use to spawn custom spinning coins if you have
implemented them, at least.

question_block_block.asm is special in the sense that it
doesn't spawn any sprite but rather spawns a block on top
of the ?-block.

----------------------------------------------------------
Another customisation is the initial sprite state. That
way, you can spawn both, normal and carryable sprites.
You can also use the initial state but it is not always
recommend because some sprites won't work properly if
they're spawned that way.
That is, however, also true for the opposite - some
sprites only work if they are spawned in the initial
state.

----------------------------------------------------------
You have to patch Yoshiegg.asm in order to use the egg
blocks without glitching.

----------------------------------------------------------
In addition, you can also change the YXPPCCCT properties
of the bounce block. On regular basis, it doesn't matter
because most blocks are either turn or question mark
blocks but in cases like the !-blocks, the bounce sprite
is in a different palette than palette 8.

----------------------------------------------------------
giant_xxx.asm are pretty self explaining. They are giant
version of the normal ?-block and only doesn't include a
version which spawns a block (ever spawned a block
in-between two others?). They are made of one block but
use the Map16 number to determine the quarter (how its
done is determined below).
Another difference between the regular and giant question
mark-blocks is that the latter can be set to shake the
screen (similar to the non-world 4 / bonus giant ?-blocks
in SMB3).

----------------------------------------------------------
The example folder contain some... well examples to show
some... features. They are inserted like any custom block
but here is a note for both xxx_switch_block.asm:
In order to insert them as the !-blocks, you can't insert
them with the same Map16 tile number as these blocks (GPS
doesn't allow to insert custom blocks on the first two
pages) but you need to insert them as any other custom
block and then change the acts like of the actual
!-blocks to the custom block number.

----------------------------------------------------------
check_sprite_kicked_horiz_alt.asm is a routine and should
not be inserted as a block directly but rather put in the
included "routines" folder or whatever you renamed it.

----------------------------------------------------------
I've also included two other TXT files:
question-block-object.txt is used for item memory
dependent blocks. See the F.A.Q. what it means. 
The other one is just a block list with pre-inserted
blocks. Use it together with the Map16 block.
Both of them are optional, at least if you don't use.

How can I customize the blocks?
----------------------------------------------------------
There are defines inside both, the inserted ASM files as
well the base blocks.

Of particular note are global settings. These include a
small boop when touched from below underwater while
carrying an item (kind of like in SMM2), enabling a fix
for block duplication (or rather, disable the bug since it
is actually harder to code) and for giant blocks, the
block layout.

In order to determine the corner, the giant question mark
blocks look at their Map16 number (not to be confused with
the acts like number).
How the corners are finally determined can be set within
the blocks themselves: By default, the Map16 layout is
rectangular i.e. the blocks look at the first and second
digit from the right. If the first digit is odd

Think of it as this way:
12 12 12 12
34 34 34 34
with 1, 2, 3, 4 as the top left, top right, bottom left
and bottom right corner, respectively.

In contrast, linear layout puts them all on the same line
where only the rightmost digit is taken care off and the
corner repeat every four blocks.

The tile layout is more like this:
12 34 12 34
12 34 12 34
with the same definition of the numbers as above.

As a tip: You can assign multiple Map16 tiles with one
custom block in GPS with:
<first ID>-<second ID>
A prefix with "R" defines a rectangle like this:
R<first ID>-<second ID>
The latter is used in the example block list included in
this patch.

Do I must give you credits?
----------------------------------------------------------
For the normal blocks, you don't need to credit me. They
are pretty free to use, mostly because they are fairly
easy to create (at least, most codes) and while I had to
do some researches, there were pretty small. If you want
to, you can upload these blocks somewhere else without my
permission. Just don't claim these as yours.
You also don't.
For the older versions, credits is very much necessary
but by including a base block, I managed to simplify a lot
of work with using only block for each corner which is why
they need to be credited as much as regular blocks (i.e.
it can be uncredited).

Have you done everything by yourself?
----------------------------------------------------------
The blocks itself: Made by me.
   Exception: The main code for the egg blocks were made
   by LX5.

Why did you make these blocks?
----------------------------------------------------------
Once again, I wasn't really happy about the already
existing stuff (both, the regular blocks and the giant
blocks) so I tried to recreate a better version.
Of course, I also could use the original spawning routine
but that is pretty limited, especially when used with
custom sprites.

I've got a question!
----------------------------------------------------------
Post it to the forums. In the worst case, you can PM me.

Is that really all?
----------------------------------------------------------
Not all sprites are compatible or don't work as properly
when spawned from the block as they do in game because
these requires some other steps which this block doesn't
cover without modifying it.
In that case, you likely need to spawn the sprite in its
initial state ($01) as opposite to the normal and
carryable state ($08 and $09) but there no guarantee
about it.

"F".A.Q.
----------------------------------------------------------
Q: I can't get to insert yoshiegg.asm and
   question-block-object.txt with GPS or if they do,
   they crash the game!
A: yoshiegg.asm is a patch and not a block.
   question-block-object.txt is a code for ObjecTool.
   None of them are supposed to be inserted as blocks.

Q: Which sprites can be set to be carryable?
A: All sprites which are either always carryable or can
   be attacked to stun them.
   There are a few notable sprites:
   - Koopas and Koopa shells are the same sprite number.
     Yes, I know LM says it differently but only because
     "sprites" $DA-$DF spawn an already stunned Koopa.
   - You can set Yoshi eggs to be stunned too.
     The differences between the "normal" and "stunned"
     eggs are that the former spawns a baby Yoshi and the
     latter to what you have set in $151C,x.
     (Be aware to use the xxx_egg.asm blocks if you want
	 to spawn Yoshi eggs. They don't work in the regular
	 blocks)
   - Sprite $53 is a bit special. Both, its initial and
     main routine point to an RTS. It does, however, have
     a code for being carryable.
     It is the throw block.

Q: What do "!1540_val" and "RAM_1540_val" do?
A: $1540,x is used as a timer for various sprites. What it
   exactly does in various sprites is different but here
   are a few notable sprites:
   - The power ups use it as the timer they are coming out
     of the block. It should be set to $3E (60 frames / 1
     second).
   - It is the stun timer for stunned / carryable sprites.
     It means that the carryable sprite will turn normal /
     disappear if the sprite is timed (exception: Koopas
     which spawn a shell-less Koopa, throw blocks which
     disappear and bob-ombs which, while technically
	 really unstun themselves, explode).
     If set to zero, the sprite will never unstun.
	 
     Keep in mind that, the Koopa behaviour is the default
     behaviour meaning that if you have set a non-zero
     value for !1540_val on carryable-only sprites like
     keys or p-switches, they will spawn a sprite after
     some time.

Q: Help, the sprite spawns inside the block and it can't
   get out!
A: A side effect that you spawned a static sprite. To fix
   all what you need to do is to add 0x10 to "!YPlacement"
   Either that or you just spawned it wrongly (can be
   caused by this too - see a feather spawned in the
   initial state).

Q: Help, when I activate the block, sprites disappear!
A: That is because you reached the sprite limit. Vanilla
   SMW can only run up to 12 sprites on-screen and
   maximally only 10 can be spawned from the level itself
   but this limit doesn't exist on blocks except if it
   should do it that way like with the enemy blocks.
   Any more, and sprites either fail to spawn or in case
   with the normal question mark-blocks, it has to delete
   other sprites.
   Yes, I chose the latter. After all, these blocks ARE
   replicas of vanilla question blocks.
   If you prefer the failing way, replace "%spawn_sprite_block()"
   with "%spawn_sprite()" and add on the next line
   "BCC .Return".
   This, however, doesn't apply to the aforementioned
   enemy blocks. In this case, the sprite will just fail
   to spawn.

Q: How can I make the block invisible?
A: It's one of the settings in this version. Just make
   sure to set !invisible_block to 1 and the acts like to
   $25

Q: What does "!item_memory_dependent" mean?
A: It means that if you active the block, it will set a
   bit to the "item memory". The item memory remembers,
   whether something was collected in a column or not (or
   in this case, whether the block was activated or not).
   Be aware that you need to use ObjecTool to make it
   work. Because of that, I have include an object which
   uses the item memory. Don't be stupid and insert it as
   a block, though!
   If you spawn used blocks, however, you can change the
   tile the block should generate, to 0x16. This is the
   same as 0x0D (both spawn a used block) except that it
   also calls the item memory routine (similar to how 0x01
   and 0x02 spawns an empty block but the former also sets
   the corresponding item memory bit). That way, you can
   save some space and time (I still keep it since it only
   works with used blocks).
   Another thing you have too keep in mind is that item
   memory works per columns. Just think about, how many
   tiles you can place maximally inside a vertical level
   (vertical because these hold a couple of more tiles
   than horizontal one). As such, it's much easier to keep
   track of that way then the other way.

Q: What is !activate_per_spin_jump?
A: That allows you to activate the blocks with a spin
   jump. It's like breaking a turn block in SMW or
   activate a block with a ground pound in modern games.
   Due to limitations, the block still acts like it has
   been hit from the bottom, though.

Q: Why doesn't !bounce_Map16 work?
A: You can only use it if !bounce_block is set to $FF due
   to the patch has it set set up that way.
   The patch in question:
   https://www.smwcentral.net/?p=section&a=details&id=12504
   Alternatively, you can use it if you disable bounce
   blocks (for whatever reason)

Q: The Yoshi eggs don't let me spawn stunned / custom
   sprites!
A: That's the Yoshi eggs' limitations, not our blocks!
   You need to hijack the routine where the sprite is
   spawned and modify our blocks.

Q: Why doesn't the giant blocks spawn a bounce block?
A: There aren't any 32x32 bounce block in vanilla SMW, you
   silly. As such, you need a custom bounce block to make
   it work.
   Be aware that you would need to use Kaijuu's custom
   bounce block (the bounce unrestrictor doesn't really
   let you create real custom bounce blocks) patch (how
   else would you insert custom bounce blocks) and, if you
   want to avoid incompatibility with non-normal sprites,
   imamelia's extended no more sprite tile limits.
   A downside for the avoiding to use bounce sprites is
   that the sprite pops out in the middle from the block
   if the sprite don't go behind the layers anyway.

Q: Extra bytes?
A: Yes. PIXI and GIEPY include support to extra bytes.
   They're known as extension in Lunar Magic. The idea is
   that some sprites are very customisable with the
   inclusion of extra bytes. Unfortunately, they're only
   set during placement but have to be manually set if
   spawned otherwise which is why I included this feature
   in the first place.
   Furthermore, only four extra bytes are supporting since
   any more requires the use of pointers. There are few
   sprites which really need that many bytes, particularly
   those which you want to spawn.

Q: Help, black bars appear on top of the screen / the
   background glitches when I activate a giant block!
A: An unfortunate side effect that four blocks changes at
   time. The game has to update 16 (graphical) tiles at
   time. Every. Single. Of. Them. (Granted, the game
   updates these into eight pairs but still...)
   And in order to upload them, you need to specify the
   position and some other settings. That it is obviously
   not really fast.
   Said problem is called a "v-blank overflow". v-blank
   is used to upload graphics and tiles and do some other
   stuff. There is major problem, though: The time is
   limited. You can lower the chances of it if you use
   FastROM, because the console/ emulator reads the ROM
   faster in that mode but it obviously won't fix it
   altogether.
   Because of that, any dynamic change of graphics (e.g.
   ExAnimation, dynamic sprites, sprite status bar,
   VWF dialogues, etc.) rises the chance of this problem.
   Interestingly, it also affects HDMA (it uses h-blank
   as opposite to v-blank).
   It should be noted that the glitch likely appears if
   low nibbles of the position of either one or both
   layers are on zero because it signalises the game, it
   should upload new tiles from the level itself.
   Yeah, there is nothing much to fix about unless someone
   optimises the stripe image routine a bit.
   A small fix is Lunar Magic's "VRAM Patch" Optimization:
   https://www.smwcentral.net/?p=section&a=details&id=28028
   That one optimises the stripe image routine caused by
   a Lunar Magic update bit and will be integrated to a
   newer version of Lunar Magic at some point.

Q: Can I update the block on my own?
A: Sure, you can. There is even a list below for people
   who has worked on this block too and preferably, write
   down, what you have changed.
   Remember to write on the change log. Any minor updates
   increments the sub-subversion by one (i.e. e.g. 1.0.0
   becomes 1.0.1), any new features increments the
   subversion by one and the sub-subversion gets zero'ed
   (i.e. e.g. 1.3.2 becomes 1.4.0).
   Minor updates are so small that you shouldn't add your
   name on the author field but you are allowed to if you
   add new features.

Q: What values do I have to enter for the item box
   blocks?
A: That depends whether you use the Item Box Special or
   not.
   If you use it (be it directly or indirectly), the value
   you enter for the item box item is the value for $0DC2
   directly.
   If you don't use, all you have to enter is the sprite
   number, my block takes care of everything.
   That being said, without Item Box Special, you should
   at least apply Item Box GFX fix and possibly stunned
   item box items fix if you want to put any vanilla
   sprite other then the power ups.
   And one note with stunned sprite: Be careful with them
   as they're always spawned non-stunned without Item Box
   Special.
   
   Item Box Special:
   https://www.smwcentral.net/?p=section&a=details&id=12694
   
   Item Box GFX:
   https://www.smwcentral.net/?p=section&a=details&id=4255
   
   Stunned Item Box Items Fix:
   https://www.smwcentral.net/?p=section&a=details&id=12388

Q: Why is the description for power up dependent blocks
   different from the normal blocks?
A: A limitation of the descriptions because it doesn't
   allow to read them from tables (at least in custom
   blocks). You can edit them however you want, though.

Q: Why does the giant block act like it's always the
   <insert corner here> corner?
A: You didn't read the readme, did you? :P
   To explain what's happening again: The block uses the
   Map16 number to determine the corner of the block.
   This uses a very simple formula which is described
   above and must use the raw Map16 number, never the
   acts like.

Q: How can I use the block duplication glitch?
A: This is a setting in the block. It's a global setting
   and thus set within the base blocks.

Q: How can I build custom question mark blocks?
A: For that, you should refer to question_block.asm and
   giant_question_block.asm. These are the minimum
   requirements to have a working question mark block.
   The code for when a block is activated is located
   below "SpawnThing".

Q: OMG! HWO KAN UR COED B EVN AXEPTD ON SMWC DEPID RIN
   TOLATY SH!T?!? I NWO IT CUS I IS ADBANSD HAXOR!!1!ONE
A: Thank you for you compliment (albeit a pretty harsh
   one, I actually won't thank you). If you have got any
   advices or crash reports, please let me know.
   I will sometime take a look at it.
   (No, please don't write it like above.)

Contributors
----------------------------------------------------------
- MarioFanGamer (original creator)
- LX5 (egg blocks)

Changelog
----------------------------------------------------------
v1.0.0:
 - First version of the block.

v1.1.0:
 - Include egg blocks (thanks LX5).
 - Include an example block list and Map16 files.
 - Optimised the blocks.
 - Made some changes on the read me.

v1.1.1:
 - Included some routines (which I have forgotten to
   include them >_>)
 - Included the giant block GFX (yeah, <.<)
 - Fixed something where I uses a RAM address to set
   something even though it should be a constant value.
   (Man, I'm so forgetful >.<)

v1.2.0:
 - Added Item Box Blocks (at the request of Skewer).
 - Added custom bounce block support.
 - Added support to move sprite to block with offset.
 - Removed the routines as these are already included with
   the latest version of GPS.
 - Change the spawn routine in the giant blocks.
 - Fixed some spelling errors in the readme.

v1.3.0:
 - Added coin block
 - Updated custom bounce block support (primary reason).
 - Added support to move eggs with an offset.
 - Added option to make blocks invisible.
 - Added feature to activate 16x16 blocks with a spinjump.
 - Added proper support for GIEPY for enemy blocks.
 - Added extra bit support for Sprite Tool and GIEPY for
   enemy blocks.
 - Added extra byte support.
 - Change the change block routine in the giant blocks.
 - Fixed even more spelling errors in the readme.

v2.0.0:
 - Fixed blocks so they work on newer versions of GPS.
 - Rewrote logic so that it works like Fernap's resources
   i.e. there is a base block which is included by every
   ASM file which contains some specific routines instead
   (e.g. spawn a sprite).
   This cuts down writing these blocks by an incredible
   amount.
 - Added ?-block which spawns a block instead of a sprite.
 - Renamed blocks with better names.
 - Added block duplication code and underwater push as
   global options.
 - Use only one type of 32x32 blocks, uses Map16 number to
   determine quarter.
 - Redrew the graphics to be less rounded and more
   angular. This is actually how the giant blocks in SMB3
   and NSMBU are designed and looks overall prettier.
 - Added support for ObjecTool 0.5 due to changes in the
   item memory routine.
