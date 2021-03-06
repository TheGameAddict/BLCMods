Apocalyptech's Borderlands 2 Mods
=================================

Aegrus Not-So-Rare Monsters
---------------------------

This is a real simple mod which just alters the spawn rates of the "rare"
creature types in Sir Hammerlock's Big Game Hunt.  This is really only
useful if you're looking to complete the
[I Like My Monsters Rare](http://borderlands.wikia.com/wiki/I_Like_My_Monsters_Rare)
mission without having to do any extra farming.

BL2 Better Loot Mod
-------------------

This mod's general goal is to make loot drops in Borderlands 2 "better",
as in skewing very much towards the rarer loot.
Legendaries/Uniques/Pearls/Seraphs will drop far more frequently than they
do in vanilla B2, etc.

It's essentially a cheat mod, intended for those BL2 players like myself who
tend to play in Normal most of the time, dislike grinding, get bored easily by
the uninteresting and drab loot that typically gets dropped in-game, and who
often end up just resorting to Gibbed to be able to play around with some
better gear.  The README in the mod dir itself should provide a lot more info.

BL2 Cold Dead Hands
-------------------

This mod completely revamps the way in which weapons and shields are
acquired during the game.  Instead of dropping weapons/shields from a
random loot pool, enemies will now *always* drop the specific gun and
shield that they're using.  In the default configuration, enemy gear
quality is also improved considerably.

BL2 Early Bloomer
-----------------

Unlocks all weapons/items to be able to spawn right at the beginning of the game.
A more powerful version of the same functionality provided by UCP.  (This is
technically a subset of Better Loot; if you're already running Better Loot then
you already have this.)

BL2 Movement Speed Cheats
-------------------------

This mod increases movement speed of all BL2 characters (including while
crouched, and while in FFYL).  It also increases the jump height a bit, and
increases air control by quite a lot.  If you're looking to zip through
some levels like there's no tomorrow, this is for you.

BL2 No Wasted COMs
------------------

This mod changes the Class Mod drop pools such that the only COMs which drop
are for characters who are actually playing the game.  For a singleplayer
game, that means you'll only ever get COMs for your one character, for
instance.

Configurable Catch-A-Ride
-------------------------

This mod is a souped-up version of FromDarkHell's "CarReplacements" mod,
which changed some of the Catch-A-Ride locations so that you can spawn
various types of vehicles throughout all the game's content.  That version
just had a few hardcoded replacements, though.  This one lets you fully
customize every single Catch-A-Ride slot in the game!

Guaranteed Omnd-Omnd-Ohk
------------------------

Gives all Badass Savages a 100% chance of evolving into Omnd-Omnd-Ohk, when
left in the presence of a Witch Doctor.  Mostly just useful if you want to
farm OOO without having to gamble on its spawn chances.

Guaranteed Varkid Evolution
---------------------------

Gives all Varkids a 100% chance of evolution, regardless of player count or
playthrough.  Mostly just useful if you want to farm Vermivorous without
having to gamble on its spawn chances.

More Loot Midget Containers
---------------------------

Alters a few levels (specifically: Arid Nexus Badlands, Hero's Pass, Opportunity,
Sawtooth Cauldron, and Tundra Express) so that as many containers as possible
can spawn loot midgets.  This doesn't meant that *all* containers can spawn
midgets, but there'll be more than there were.

More Muscles
------------

This simple mod improves the spawn rate for Muscles, a unique Bruiser who
appears in Thousand Cuts.  He will be fairly likely to appear during a full
playthrough of the level.

Speedier Sandskiffs
-------------------

Improves the speed (and afterburner capability) of Sandskiffs.

Stalkers Use Shields
--------------------

Stalkers already use shields, of course, but this mod equips them with "real"
shields, of the sort your characters equip.  Optionally, you can have them
only use Maylay shields, as well.

Utilities
=========

The statements used in Borderlands mod files are often fairly gigantic, and
difficult to understand quickly without viewing them with a bunch of linebreaks
inserted, to provide a more visual structure to the statements.  The FilterTool
utility actually provides mod-editing capabilities which include viewing/editing
mod statements as nicely-readable multiline segments, and that's probably the
easiest solution for most people.

However, I wanted to generate some mods using scripts, and anyway always prefer
editing in my text editor of choice, so I wrote a couple of quick-n-dirty
utilities in Python to automate that kind of thing for me.  This way, I can
edit multiline versions of the mod statements in whatever editor I want, then
export to the "real" version which Borderlands / FilterTool can understand.

Both of these utilities are written in Python, and probably require Python 3.
They're intended to just be run from a commandline, which may pose some
logistical problems for folks on Windows/Mac who may not be used to doing that.
(Also, Python probably isn't already installed by default on those platforms.)
Folks running Linux, like myself, should be able to just run 'em as per usual
from a terminal.

Also note that neither of these utilities attempt to process any hotfix-style
mods - they only really support the more straightforward "`set`" style patches.
Both *should* be nice and leave hotfix lines alone, though be sure to
doublecheck the output if you use them on any files with hotfixes in 'em.

conv_to_human.py
----------------

This utility can take an existing Borderlands patch/mod file, or the output
from an `obj dump <foo>` from the Borderlands console, and convert it into a
much easier-to-read-and-edit multiline file.  For instance, if you've got a
file which contains the following:

    BalancedItems(0)=(ItmPoolDefinition=None,InvBalanceDefinition=InventoryBalanceDefinition'GD_Artifacts.A_Item.A_Vitality_Rare',Probability=(BaseValueConstant=1.000000,BaseValueAttribute=None,InitializationDefinition=None,BaseValueScaleConstant=1.000000),bDropOnDeath=True)

... this utility would convert it to something like:

    BalancedItems(
        0
    )=(
        ItmPoolDefinition=None,
        InvBalanceDefinition=InventoryBalanceDefinition'GD_Artifacts.A_Item.A_Vitality_Rare',
        Probability=(
            BaseValueConstant=1.000000,
            BaseValueAttribute=None,
            InitializationDefinition=None,
            BaseValueScaleConstant=1.000000
        ),
        bDropOnDeath=True
    )

Much nicer!  For instance, to convert the main UCP patch to something more
readable, you could do:

    $ ./conv_to_human.py Patch.txt Patch-unpacked.txt

Or whatever.  If you don't specify any filenames, this util will read/write
to STDIN/STDOUT.  You an also use `-` as either of the filenames, if you
wanted to use STDIN/STDOUT for one end but not the other.

The utility will ask you to overwrite the output file, if it's specified and
already exists.  You can use the `-f` or `--force` option to automatically
overwrite without confirmation.  You can also use `-h` or `--help` as you'd
hope, though there's no features not already mentioned here.

conv_to_mod.py
--------------

Conversely, this is the utility to turn one of those nicely-human-editable
files into something which Borderlands/FilterTool can understand.  It'll just
do the reverse of `conv_to_human.py`.

Unlike `conv_to_human.py`, this utility will not read from STDIN/STDOUT,
enforces some conventions about the filenames being used, and only accepts a
single filename in the argument list.  The source file it reads from is required
to have a suffix of `-source.txt`, so for instance my own Better Lood Mod source
filename is `BL2 Better Loot Mod by Apocalyptech-source.txt`.

The destination file it uses will be identical to the source filename, minus the
`-source` suffix, so for my own mod, the output filename will be plain ol'
`BL2 Better Loot Mod by Apocalyptech.txt`.

For the filename argument, you can specify either the source or destination file,
and the utility will figure out which one you mean.  So, the following two
commands will do the exact same thing:

    $ ./conv_to_mod.py "BL2 Better Loot Mod by Apocalyptech-source.txt"
    $ ./conv_to_mod.py "BL2 Better Loot Mod by Apocalyptech"

In general I just tab-complete and whichever gets picked works fine.

As with `conv_to_human.py`, this will ask you to overwrite the destination file,
if it already exists.  You can use the `-f` or `--force` option to automatically
overwrite without confirmation.  You can also use `-h` or `--help` as you'd hope,
though there's no features not already mentioned here.

I intend to convert all of my mods which make use of this to use `modprocessor.py`
instead, once BLCMM is out and I have enough free time, so this utility's time is
numbered.

hotfixes.py
-----------

This is actually a helper library script used by the generation script for a
couple of my mods, to make dealing with hotfixes a bit easier.  It's pretty
straightforward, though unless you're me, you're unlikely to ever bother with
it.

I intend to convert all of my mods which make use of this to use `modprocessor.py`
instead, once BLCMM is out and I have enough free time, so this utility's time is
numbered.

modprocessor.py
---------------

This is my latest mod-construction library, which lets me build mods
programmatically the way I'm used to while exporting in a BLCMM-compatible
file format.  This one's mostly intended to be used by my generation code
itself, but it can be invoked on the commandline just like `conv_to_mod.py`.
It uses a custom intermediate file format which is very similar to
FilterTool's format, which then gets converted to BLCMM.  That way I can
easily continue to use code-assisted templates for mod construction, which
is the way I still prefer to do things.

Licenses
========

All the code here is licensed under the
[3-clause BSD license](https://opensource.org/licenses/BSD-3-Clause),
which should be permissive enough to do just about whatever with.

Mods under this folder are licensed under
[Public Domain / CC0 1.0 Universal](https://creativecommons.org/publicdomain/zero/1.0/).

See [COPYING-code.txt](COPYING-code.txt) and [COPYING-mods.txt](COPYING-mods.txt)
for the full text.
