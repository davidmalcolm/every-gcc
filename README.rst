every-gcc
=========
This is an experimental hack to try to ease working on all 204
configurations of GCC, inspired by `contrib/config-list.mk`.

.. code-block:: bash

  $ ./every-gcc list | wc -l
  204
  $ ./every-gcc list | head -n 5
  aarch64-elf
  aarch64-linux-gnu
  alpha-linux-gnu
  alpha-freebsd6
  alpha-netbsd

Running a shell command on every config.

%CONFIG and %OPTIONS are substituted.

stdout and stderr lines have the config name prepended:

.. code-block:: bash

  $ ./every-gcc shell "echo %CONFIG: %OPTIONS" | tail -n 5
  i686-interix3OPT-enable-obsolete: --target=i686-interix3 --enable-obsolete [i686-interix3OPT-enable-obsolete]
  score-elfOPT-enable-obsolete: --target=score-elf --enable-obsolete [score-elfOPT-enable-obsolete]
  xtensa-elf: --target=xtensa-elf [xtensa-elf]
  xtensa-linux: --target=xtensa-linux [xtensa-linux]
  204 success(es); 0 failure(s)

Managing/querying a config-list.mk build:

.. code-block:: bash

  # Get last line of each top-level configure invocation:
  [multi-mk]$ every-gcc shell "tail -n1 log/%CONFIG-config.out"
  [...snip...]
  config.status: creating Makefile [x86_64-mingw32OPT-enable-sjlj-exceptions=yes]
  config.status: creating Makefile [xtensa-elf]
  config.status: creating Makefile [xstormy16-elf]
  config.status: creating Makefile [xtensa-linux]
  tail: cannot open ‘log/sparc-sun-solaris2.9OPT-enable-obsolete-config.out’ for reading: No such file or directory [sparc-sun-solaris2.9OPT-enable-obsolete]
  tail: cannot open ‘log/i686-solaris2.9OPT-enable-obsolete-config.out’ for reading: No such file or directory [i686-solaris2.9OPT-enable-obsolete]
  config.status: creating Makefile [score-elfOPT-enable-obsolete]
  config.status: creating Makefile [i686-interix3OPT-enable-obsolete]
  202 success(es); 2 failure(s)

  # Get current last line of each "make" invocation:
  [multi-mk]$ every-gcc shell "tail -n1 log/%CONFIG-make.out"
