# TECO - DATE.TEC A real-world example

## Description

TECO code helps enter a date on RT-11 system boot.

## Abstract

TECO gets a certain amount of bad press because the code is cryptic.
Cryptic code is unavoidable in a computer language
that mostly uses single-character symbols and punctuation for
keywords. Here's some example TECO code for you to judge for
yourself.

The code manages a calendar date and provides a simple mechanism
to let a user change and save the date while registering it with the
OS, usually at boot time.

## Introduction

On a DEC LSI-11/03 computer running RT-11 this macro,
DATE.TEC, presents a nifty full-screen [1] prompt at system boot time.
It includes the last-used system date and usually all the user must
do is type _RETURN_ to get the date entered.

Our shop used PDP-11 computers in-house. The larger RSX-11 systems
had few issues with system dates. The smaller RT-11 systems that booted
from floppy disks were another story.

A major nuisance was having systems and files with no date.
Code management back then was pretty
lame and we needed all the help we could get. I have vivid memories of
having three floppy disks with identically named files none of which
had a date.
Which file was edited today???

We tried printing reminders like
**Hey, stupid, remember to enter a system date!** at then end of
STARTx.COM. That didn't always work since the reminder was lost in
the sea of boot-time console messages.

[1] Gasp! Full-screen _anything_ on RT-11!

## Background

### TECO is a programming language

One day I saw a full-screen editor running in TECO.
That, I said, is for me. So I went off the deep
end and learned enough TECO to figure out how it worked. Then I started
writing my own TECO programs for fun and profit.

DATE.TEC is one example. It made a huge difference at our shop.

### Open Source, kind of

The macro was also my first venture into open source programming.
I published the macro in _DEC Professional_ magazine sometime in mid-1983.
That led to correspondence from users around the world.
To top that off I got paid for my code submission!

## Using the code

The code was run by inserting a few lines at the end of STARTx.COM.

    SET TT NOCRLF
    SET TT SCOPE
    EDIT/EXEC/TECO SY:DATE

Picture editing AUTOEXEC.BAT on a DOS system. This is the same deal.

## Points of Interest

### Literal text representations of control characters in source file

TECO macros usually have ESC and FF characters in them. This one
is no exception. However, the source version of DATE.TEC in this repo
is meant to be printed and not to be executed by TECO. 

* ESC escape is shown as a dollar sign *$*. The *$* is usually good enough but some versions of TECO may prefer *^[*.
* FF form feed is shown as *<^L>*

### Constant width comments

It was extra work to get the trailing exclamation marks to line up
on every comment line. To me the improved code legibility is worth
the effort.

### Scope-mode terminals

Rather than real DEC VT-52 terminals we had some cheap Heath knockoffs.
Regardless, this macro running on a hard-copy console leads to some
hilarious results with CTRL-W redrawing the screen on paper over and over
again.

### Debugging

* Debugging a TECO macro is a challenge.
* You can not put a breakpoint in the code stream and examine variables.
* Console printout is overwritten by CTRL-W screen refreshes.
* Simple rookie mistakes usually cause disasters.

In the case of this application
a command procedure, _STARTx.COM_, has started TECO which in turn
spawns a system command, _EG_, to set the system date.
By the end of all that the STARTx.COM
procedure usually does not process any further work.

### Re-typed in 2022

None of the floppy disks or RK-05s holding the original code is still
accessible.
I have only hard copy. For this publication I had to type
the code again and
that means that there is most likely a typo or two in the code. For
a TECO program that spells sure run-time disaster.

I got to fix a few comments to correct some half-truths along the way.

### Y2K compliance

Hah!

### Prior art

This macro mentions VEG.TEC, a publicly available macro for editing in
full screen mode. Good luck finding out anything about it.

## License

This code is released under Apache License Version 2.0. Please see
file LICENSE.txt for details.

## History

