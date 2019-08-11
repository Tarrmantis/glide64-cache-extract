=====================
glide64_cache_extract
=====================

glide64_cache_extract is a debugging tool used to extract the content of a
Glide64 texture cache and to show extra information about the content.

USAGE
=====

The uncompressed texture cache has to be given to glide64_cache_extract using
stdin. The compressed files are usually named ``*_HIRESTEXTURES.dat`` and
``*_MEMORYCACHE.dat``. The result is a v7 tarball written to stdout.

The input and output files can also be specified using --input and --output. The
input will not be extracted (can be done using gunzip).

Extra information about the content and errors are printed on stdout.::

  $ zcat MUPEN64PLUS.dat | glide64_cache_extract -vv --bitmapv5 \
    --prefix MUPEN64PLUS | tar x
  $ for i in *.bmp; do convert -strip -define png:format=png32 \
    -define png:compression-level=9  "${i}" "${i%.bmp}.png"; done
  $ rm *.bmp

The output files don't follow the Rice hires texture naming scheme correctly.
But they should be compatible with Glide64.

More information about the parameters can be requested using::

  $ glide64_cache_extract --help

CONTRIBUTING
============

Patches can be sent to the author. Please follow the Linux CodingStyle. A quick
check can be done using::

  $ ./scripts/checkpatch.pl --strict --ignore LONG_LINE,NEW_TYPEDEFS,CAMELCASE \
    -q $PATCH
  $ make CC=cgcc
  $ cppcheck --enable=all .

EXTRA SCRIPTS
=============

contrib/ contains extra scripts which can be used for further analysis.

1. analyze_tex can be used to extract extra information from existing
   hires texture packs which are not stored inside the glide64 texture cache.
2. example_db contains some extra information from texture sets which
   can be used to rename the extracted textures
