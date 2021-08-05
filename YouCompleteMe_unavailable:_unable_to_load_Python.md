# YouCompleteMe unavailable: unable to load Python 

https://github.com/ycm-core/YouCompleteMe/issues/3635

vim's doc is http://vimdoc.sourceforge.net/htmldoc/if_pyth.html#python-dynamic
this document say , many other software also would be crashed because use more than one python version in one environment.
so this tiltle problem is not only YouCompleteMe's problem.
I find resolution from vim's document which I paste blew:

Vim can be built in four ways (:version output):

No Python support (-python, -python3)
Python 2 support only (+python or +python/dyn, -python3)
Python 3 support only (-python, +python3 or +python3/dyn)
Python 2 and 3 support (+python/dyn, +python3/dyn)
Some more details on the special case 4:

When Python 2 and Python 3 are both supported they must be loaded dynamically.

When doing this on Linux/Unix systems and importing global symbols, this leads
to a crash when the second Python version is used. So either global symbols
are loaded but only one Python version is activated, or no global symbols are
loaded. The latter makes Python's "import" fail on libraries that expect the
symbols to be provided by Vim.

						*E836* *E837*
Vim's configuration script makes a guess for all libraries based on one
standard Python library (termios). If importing this library succeeds for
both Python versions, then both will be made available in Vim at the same
time. If not, only the version first used in a session will be enabled.
When trying to use the other one you will get the E836 or E837 error message.

Here Vim's behavior depends on the system in which it was configured. In a
system where both versions of Python were configured with --enable-shared,
both versions of Python will be activated at the same time. There will still
be problems with other third party libraries that were not linked to
libPython.

To work around such problems there are these options:

The problematic library is recompiled to link to the according
libpython.so.
Vim is recompiled for only one Python version.
You undefine PY_NO_RTLD_GLOBAL in auto/config.h after configuration. This
may crash Vim though.
==================================================================
so I resolve this problem by change vim compile script from
./configure --with-features=huge
--enable-multibyte
--enable-gtk3-check
--enable-rubyinterp=yes
--enable-pythoninterp=yes
--with-python3-command=python3.7
--enable-python3interp=yes
--enable-perlinterp=yes
--enable-luainterp=yes
--enable-cscope

to be:
./configure --with-features=huge
--enable-multibyte
--enable-gtk3-check
--enable-rubyinterp=yes
--with-python3-command=python3.7
--enable-python3interp=yes
--enable-perlinterp=yes
--enable-luainterp=yes
--enable-cscope

you can see ,I need erase "--enable-pythoninterp=yes" configuration . make vim olny use one python version.
