# Man Page Development

I have come to greatly appreciate the offline document available
on Linux, **man** and **info** pages.

When developing my own projects, I eventually get around to writing
my own offline documentation.  The problem is that I forget a lot
bewteen man-writing sessions, and I'm never quite sure I'm doing it
right.

This guide, and associated files, is intended to provide assistance
in writing **man** pages through examples and downloaded reference
materials in the form of further **man** and **info** pages.

Typically, **man** pages are written in **groff** format, which
is an Gnu-extension of **roff**.  **groff** and **roff** are
typesetting specifications that can use macros to simplify
certain output.  There is a special set of **man** macros that
help *man-page* developers achieve a structure that is consistent
with most other *man-pages*.

**NOTE** The *Style Guide* section below directs the reader to a very
useful resource.

## Purpose of the Guide

This document is not meant to be a guide for writing man pages.
It is, rather, a guide to available reference, especially offline
man and info pages.


## Resources

This is a guide to resources, so it begins with a list of resources,
where to find them, and what they cover, with suggestions about how
to use them.

### Downloading Resources

While man pages *man*, *man-pages*, and *groff* were available in
a fresh install of *Ubuntu*, several other resources were not.  The
other resources used in this guide are found in the **groff**
package.  Install this package (a Ubuntu example):

~~~sh
user@computer:~/$ sudo apt-get install groff
~~~

### Utilities

- **groffer** is a utility found in the **groff** package.
  **groffer** can view man pages in development.  That is, it can
  display the local in-process man page without first having to
  install the man page.
  
  `groffer --mode=tty new_program.1`

### Documentation

These first man pages were available in my default *Ubuntu*
installation.

- `man man`  The *man-page* of **man** includes some guidelines
  for writing *man-pages* in the **DESCRIPTION** section.  This 
  includes section numbers 1-9 (document programs, system calls,
  and library calls, among others), section names (NAME, SYNOPSIS,
  DESCRIPTION, etc.), as well as styling conventions (when to use
  bold, italic, etc.).  

- `man man-pages` provides a lot more detail about formatting
   and content conventions to use when writing man pages.

- `man 7 man` documents several *groff* macros and other methods
  for creating the formatting suggested by `man man-pages`.  This
  document also includes an example macro definition (.URL)

- `info groff` (in **groff** package)  has a great wealth of
  information about writing *groff* files, a subset of which are
  man pages.

- `info groff --node=man` (in **groff** package)  Compared to
  `man 7 man`, this is more comprehensive, listing more defined
  macros and explaining their use.

- `man groff_man`  (in **groff** package) Compared with
  `info groff --node=man` this is less complete and much more
  brief,  but is easier to scan to jog one's memory about available
   macros.

## Writing Man Pages

### Sample Man File

This repository include a man file template, `sample.1` that can
serve as starting point.  It will likely change as my man-writing
skills improve.

### Man Page Structure

The DESCRIPTION section of the **man** man-page documents several
man page conventions:

- Man information is often organized into multiple man files,
  designated by different **section numbers** that describe the man
  page type.  For example section number 1 refers to an executable,
  section 3 refers to library calls.  An example to illustrate this
  is **printf**.  **printf** is both a utility (man 1 printf) that
  can be invoked on the command line or in a shell script, and a
  library function (man 3 printf).

- Commonly-used **section names** within a man page file.

- Formatting conventions for the SYNOPSIS section that can be
  used to guide formatting decisions in the rest of the man file.

### Man Page Formatting

The **groff** document formatting system is a Gnu extension to the
older **roff** version.  **groff** processes macros to simplify
the construction of common elements.  There is a set of *groff*
macros specifically-designed to support man page development.

Please refer to `man 7 groff_man` and `info groff --node=man`
for as described in the **References** section earlier in this
document.

There is also some benefit to learning specific *groff*
commands.  Please refer to `man 7 groff` to learn more about
the *groff* description language.  Despite the length of the *groff*
man page, it is a brief and incomplete reference.  Refer to the
many chapters of the *groff* info document (`info groff`) for a
more complete and authoritative reference.

### Man Page Content

#### Style Guide

The **man-pages** man page contains a comprehensive style guide.
Access this style guide with this command string:

~~~sh
man -P 'less +/STYLE\ GUIDE' man-pages
~~~

This is **very** helpful.  I had been looking for something like
this for a very long time.

## Installing a **man** Page

A *man-page* document is not very useful if it cannot be invoked
wherever necessary.  These are the steps for installing a *man-page*.

- Write the *man-page* with an extension according to the 1-9
  section number of *man-page* its contents fall.

  For example, if you are documenting a program you wrote, you
  will write a *man-page* section #1 with a *1* extension:
  `new_program.1`  Make sure the *man-page* name is the same name
  as the invocation of the program.

- Copy the uncompressed *man-page* to the appropriate directory.
  `cp new_program.1 /usr/share/man/man1/new_program.1`

- Compress the *man-page* in the man directory:
  `gzip -f /usr/share/man/man1/new_program.1`

Having followed the steps above, the *man-page* of the
*new_program* application can be invoked with `man new_program`

