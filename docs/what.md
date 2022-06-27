NAME
====

**what**(1f) - \[DEVELOPER\] extract SCCS-style metadata from a file
(LICENSE:PD)

SYNOPSIS
========

what \[ **filename**(*s*) \[ -*s*\] \[ **-q**\] \[
**-html**\|**-table**\] \] \| \[ \[ **-help**\] \[ **-version**\] \]

DESCRIPTION
===========

The **what**(1) utility searches each filename for occurrences of the
SCCS identification string @\#\#\# and prints what follows up to a
",\>,\\, or any non-printable ASCII
**character**(NULL,NEWLINE,TAB,\`\`\`..).

This allows files to quickly be scanned for metadata such as simple
descriptions, versions and pedigree placed in the files.

OPTIONS
=======

The following options are supported:

****-single**, -*s***

:   Stops after the first occurrence of the pattern in each file.

****--html**, **-H****

:   Print output as a table in an HTML document.

****--table**, **-t****

:   Print output as a HTML table.

****--verbose**, **-q****

:   Quiet mode (do not report errors when opening filenames)

****--help**, **-h****

:   Print description of this program.

****--version**, **-v****

:   Print version information for this program

EXAMPLES
========

Example 1: Extracting SCCS version information

Text files are generally easy to place a @\#\#\# string into by using
the appropriate format for a comment in the language being used. Exactly
how to place a string into an object file or executable may vary
depending on your compiler or optimization level. Generally the
following strings will work:

> -   C/C++ \#ident "@\#\#\#identification info"
>
> -   C: char sccsid\[\] = "@\#\#\#identification info" /\* must be
>     global scope or optimization usually removes it \*/
>
> -   C++: \#pragma ident "@\#\#\#identification info" /\* many
>     references say this should work, but unreliable \*/
>
> -   Fortran: **character**(len=\*),parameter::sccsid=
>     @\#\#\#identification info be careful it is not removed by high
>     optimization levels
>
For example, if program.f90 were compiled to yield program.o and
executable a.out, the command: what program.f90 program.o a.out should
produce:

            program.f90:
                  identification info
            program.o:
                  identification info
            a.out:
                  identification info

A few tips for common interpreted file types:

> -   shell script: \#@\#\#\#identification info
>
> -   HTML: \<!--"@\#\#\#identification info"--\>
>
EXIT STATUS
===========

The following exit values are returned:

> **0**
>
> :   Any matches were found.
>
> **1**
>
> :   No matches found.
>
ENVIRONMENT VARIABLES
=====================

AUTHOR
======

John S. Urban

LICENSE
=======

Public Domain

SEE ALSO
========

The following commands can help identify file contents **file**(1),
**strings**(1), **nm**(1), **ldd**(1), **cpp**(1), **fpp**(1),
**ident**(1), **ar**(1), **objdump**(1), **ranlib**(1), \[if SCCS
installed \] **sccs**(1), **sccs-admin**(1), **sccs-get**(1), \`\`\`

Related topics: schema, IDL (Information Description Language), \`\`\`

BUGS
====

There is a remote possibility that a spurious occurrence of the
"@\#\#\#" pattern could be found by **what**(1).

If standard input is processed it must be a text file with line width
less than 4,096 characters or errors may occur.

The length of the file arguments may be limited depending on what
command-line argument parser is used.
