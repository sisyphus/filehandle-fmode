NAME
====

       FileHandle::Fmode - determine whether a filehandle is opened for
       reading, writing, or both.

SYNOPSIS
========

        use FileHandle::Fmode qw(:all);
        .
        .
        #$fh and FH are open filehandles
        print is_R($fh), "\n";
        print is_W(\*FH), "\n";

FUNCTIONS
=========

        $bool = is_FH($fh);
        $bool = is_FH(\*FH);

This is just a (more intuitively named) alias for is_arg_ok().
Returns 1 if its argument is an open filehandle.
Returns 0 if its argument is something other than an open filehandle.

        $bool = is_arg_ok($fh);
        $bool = is_arg_ok(\*FH);

Returns 1 if its argument is an open filehandle.
Returns 0 if its argument is something other than an open filehandle.

Arguments to the following functions  must be open filehandles. If
any of those functions receive an argument that is not an open
filehandle then the function dies with an appropriate error message.
To ensure that your script won't suffer such a death, you could first
check by passing the argument to is_FH(). Or you could wrap the
function call in an eval{} block.

Note that it may be possible that a filehandle opened for writing may
become unwritable. If for example the disk runs full on Linux, a write
attempt will fail, while is_W($fh) still reports true. The behavior
for other platforms is not tested.

        $bool = is_R($fh);
        $bool = is_R(\*FH);

Returns true if the filehandle is readable.
Else returns false.

        $bool = is_W($fh);
        $bool = is_W(\*FH);

Returns true if the filehandle is writable.
Else returns false.

        $bool = is_RO($fh);
        $bool = is_RO(\*FH);

Returns true if the filehandle is readable but not writable.
Else returns false.

        $bool = is_WO($fh);
        $bool = is_WO(\*FH);

Returns true if the filehandle is writable but not readable.
Else returns false.

        $bool = is_RW($fh);
        $bool = is_RW(\*FH);

Returns true if the filehandle is both readable and writable.
Else returns false.

        $bool = is_A($fh);
        $bool = is_A(\*FH);

Returns true if the filehandle was opened for appending.
Else returns false.
Not currently implemented on Win32 with pre-5.6.1 versions of perl (and
dies with appropriate error message if called on such a platform).

CREDITS
=======

Inspired (hmmm ... is that the right word ?) by an idea from BrowserUK
posted on PerlMonks in response to a question from dragonchild. Win32
code (including XS code) provided by BrowserUK. Zaxo presented the idea
of using fcntl() in an earlier PerlMonks thread.

Thanks to dragonchild and BrowserUK for steering this module in
the right direction.

Thanks to attn.steven.kuo for directing me to the perliol routines
that enable us to query filehandles attached to memory objects.

And thanks to Jost Krieger for helping to sort out the test failures that
were occurring on Solaris (and some other operating systems too).

TODO
====

I don't know that anyone still runs pre-5.6.1 perl on Win32. However, if
someone likes to tell me how is_A() could be made to work on pre-5.6.1
Win32 perl, I would be quite happy to implement it.

LICENSE
=======

This program is free software; you may redistribute it and/or
modify it under the same terms as Perl itself.
Copyright 2006-2008, 2009, 2010, 2012 Sisyphus

AUTHOR
======

Sisyphus <sisyphus at cpan dot org>
