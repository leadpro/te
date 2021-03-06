te
==

v1.40 / 08 Mar 2020 for CP/M

(c) 2015-2020 Miguel Garcia / FloppySoftware

www.floppysoftware.es

**NOTE**: This project has been extracted from my [RetroProjects](https://github.com/MiguelVis/RetroProjects) repository.

Introduction
------------

The `te` text editor is small, humble, and useful.

It's screen oriented, and can be easily adapted to a lot of computers.

It's written in the C language, and there are ports for various
operating systems: CP/M, DOS, Windows and GNU/Linux.

![te image](http://www.floppysoftware.es/images/cpm-te.jpg "te image")

Command line
------------

It's simple (for the PCW adaptation; see below for the name of the rest
of available adaptations):

```
te_pcw [filename]
```

Examples:

```
te_pcw           - To start an empty document.
te_pcw notes.txt - To edit the document 'notes.txt'.
```

You could rename the adaptation of your choice to simply `te`.


The screen layout
-----------------

On the first screen line, you will see something like:

```
te: NOTES.TXT - The file name of the document your are editing.
```

And something like:

```
--- | Lin:0015/0042/0512 Col:32/90 Len:36
```

The very first field, can have one of the following values:

```
--- Means the clipboard is empty.
CLP Means the clipboard has data.
```
 
The numbers following 'Lin' are:

```
0015 - The line number you are editing right now.
0042 - The current total number of lines.
0512 - The maximum number of lines.
```

The numbers following 'Col' are:

```
32 - The column number on which you are.
90 - The number of screen columns.
```

And, finally, the number following 'Len' is:

```
36 - The length of the current line.
```

On the last screen line, you will see program messages and questions.


The options menu
----------------

You can enter to the menu, by pressing the `ESCAPE` key, as shown
in the messages line:

```
Press [ESC] to show the menu.
```

Note that the exact name of your `ESCAPE` key may differ, depending of
the program adaptation.

The options are:

```
New       - To start a new document
Open      - To open a document
Save      - To save the current document
save As   - To save the current document under another filename.
Help      - To show the help screen.
aBout te  - To show some te information.
eXit te   - To quit the program.
```

You can select an option by pressing the character in uppercase.

To leave the menu, you must press `ESCAPE`.

If you select one of the options `New`, `Open` or `eXit`, and there are any
changes that are not saved yet, te will ask you for confirmation
before proceed (both `INTRO` or Y mean YES).

If you start a new document, the `Save` option will redirect to you to
the `save As` option.

The help screen will show the keyboard configuration, which depends
of the program adaptation.

For example, in the case of TE_WS100 (25x80 VT100 and WordStar keys) you
could see something like this:

```
Up       ^E           | Down     ^X           | Tab      ^I  TAB
Left     ^S           | Right    ^D           | Intro    ^M  or ^N
Begin    ^QS          | End      ^QD          | Escape   ^[  ESC
Top      ^QR          | Bottom   ^QC          | Macro    ^QM
PgUp     ^C           | PgDown   ^R           |
<-Word   ^A           | Word->   ^F           |
<-Del    ^H  or DEL   | Del->    ^G           |
BlkStart ^KB          | BlkEnd   ^KK          | BlkUnset ^KU
Cut      ^Y           | Copy     ^O           | Paste    ^W
Delete   ^KY          | ClrClip  ^T           |
Find     ^QF          | F.Next   ^L           | GoLine   ^J
```

The clipboard
-------------

The clipboard contents is not cleared after file operations (new, open,
save...). That makes possible to share text between files.

But it's a good practice to clear the clipboard when you don't need it
anymore, to free some memory.


Key bindings
------------

As you can see in the help screen of example, there are some key bindings
to perform actions when you are editing the file.

The exact keys you must press to do an action, depend on the adaptation
you are running, but the meanings are the same:
- Up, Down, Left, Right: to move the cursor one character at a time.
- Begin, End: to move the cursor to the begin or the end of the
  current line.
- Top, Bottom: to move the cursor to the begin or the end of the
  current file.
- PgUp, PgDown: to move the cursor to the previous or next page.
- <-Word, Word->: to move the cursor to the previous or next word.
- <-Del, Del->: to delete the previous or next character.
- Find, F.Next: to find a string or repeat the search.
- GoLine: to go to a line number.
- BlkStart: to mark the start of a block of lines.
- BlkEnd: to mark the end of a block of lines.
- BlkUnset: to unselect a block of lines.
- Cut, Copy, Paste, Delete: to cut, copy, paste or delete a line
  or block of lines.
- ClrClip: to clear the clipboard data.
- Macro: to run a macro.
- Tab: to insert spaces as indentation.
- Intro: to insert a break or empty line.
- Esc: to exit the menu or cancel an action.

Take into account that some actions could not be available in all te
adaptations to save memory space. These actions are: <-Word, Word->,
Find, F.Next, GoLine, BlkStart, BlkEnd, BlkUnset and Macro.

If you miss one or more of the mentioned actions, you can edit the exact
file of the te adaptation and recompile it to include them.


Auto-completion
---------------

If the text editor is compiled with the auto-completion option enabled,
the input of some characters will cause the automatic input of some other.

Very useful for programmers:
-[ --> ]
-{ --> }
-( --> )
-" --> "
-' --> '

Also, for C language style comments:
-/* --> */


Auto-indentation
----------------

The text editor supports automatic indentation of lines, according
to the indentation of the previous one.


Macros
------

Macros are a powerful way to perform repetitive tasks at editing level.

For example, you could create a macro with your signature to include it
in all letters you write.

Or, being a programmer, you could create a gdoc block macro to document
your own C functions.

Each time you want to run a macro, just press the corresponding key
for the Macro action, enter the filename you choose when you saved it
to disk, and press the key for the Intro action. That's all.

There are some special symbols you can use in your macros:

```
{up} {down} {left} {right}
{begin} {end}
{top} {bottom}
{intro}
{tab}
{cut} {copy} {paste} {delete}
{clrclip}
{blkstart} {blkend}
{filename}
```

As you can see, they are self explanatory.

The symbol names are case insensitive - ie: `{ClrClip}` and `{clrclip}`
are equivalents.

Additionally, you can repeat a symbol as in:

```
{up:12}
```

Take into account that line endings in the macro are not translated to Intro
actions. Use `{intro}` for that.

If you need to insert the `{` or `}` characters in the text of the macro, just
write `\{` and `\}`.

For example, a macro to insert a banner at the top of the document, could
be written as:

```
{top}{intro}{up}
=============={intro}
FloppySoftware{intro}
=============={intro}
```


File backup
-----------

Each time a file is saved, te does a backup of the previous file
contents if it exists.

It is renamed as `te.bkp`.


Adaptations
-----------

The program adaptation is done by editing a small source code file.

In this file, you must specify the key bindings for the editor actions,
according to your preferences and / or keyboard, and complete a few C
language functions to clear the screen, etc.

As there are some adaptations already done, it's possible that your
machine is already included between them.

If not, don't worry, you can start from a similar adaptation.

See the source code files for more information.

Current CP/M adaptations are:
- te_pcw:   Amstrad PCW and CP/M Plus (31x90 VT52 like terminal).
- te_cpc3:  Amstrad CPC and CP/M Plus (24x80 VT52 like terminal).
- te_spec:  Spectrum +3 and CP/M Plus (23x51 VT52 like terminal).
- te_mur:   K. Murakami's CP/M emulator (25x80 VT100/Ansi).
- te_tak:   Takeda Toshiya's CP/M emulator (25x80 VT100/Ansi).
- te_ws100: Generic 25x80 VT100 and WordStar keys.
- te_kp:    Kaypro II, 4 and 10 (24x80 ADM-3A like terminal),
  contributed by Stephen S. Mitchell (thanks!).
- te_px8:   Epson PX-8 "Geneva".

Adaptations for other OS are (they are distributed apart):
- Windows 32 bit (25x80), compiled with Pelles C
  and its 'conio.h' library.
- DOS (25x80), compiled with Turbo C, and
  its 'conio.h' library.
- GNU/Linux (24x80), compiled with GCC and ncurses.


License
-------

This program is freeware, and it's licensed under the GNU GPL license.

See the file `copying.txt` for more details.


About this file
---------------

Of course, this text file has been created and edited with te.
