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
