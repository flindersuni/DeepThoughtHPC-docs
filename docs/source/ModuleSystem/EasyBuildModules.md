# EasyBuild Modules

These are the modules that are not-quite-the-default yet. EasyBuild enforces nice, strict versioning. Compilers/toolchains are programs and have their own bugs. **THESE MODULES ARE NOT USABLE BY DEFAULT**.

Just to make that nice and clear.

**YOU WILL NOT SEE THESE MODULES BY DEFAULT**.

You can, however, opt-in to use them. Issue the below on the command line for a once off(gone when you logout), or add the same line to your ~/.bashrc file so it applies when you login.

`module use /cm/shared/apps/easybuild/modules/all`

|                                                   |                                                   |                                           |
|---------------------------------------------------|--------------------------------------------------|-------------------------------------------|
|  ANSYS/2019.R1-foss-2019a                         | OpenMPI/3.1.3-GCC-8.2.0-2.31.1                  | foss/2019a|
|  ANSYS/2019.R1-intel-2020.00                      | OpenMPI/3.1.3-gcccuda-2019a                     | foss/2019b                               (D)|
|  ANSYS/2019.R1                             (D)    | OpenMPI/3.1.4-GCC-8.3.0                     (D) | freetype/2.9.1-GCCcore-8.2.0|
|  Autoconf-archive/2019.01.06-GCCcore-8.2.0        | PCRE/8.43-GCCcore-8.2.0                         | gcccuda/2019a|
|  Autoconf/2.69-GCCcore-8.2.0                      | Perl/5.28.1-GCCcore-8.2.0                       | gemini/0.30.2|
|  Autoconf/2.69-GCCcore-8.3.0               (D)    | Perl/5.30.0-GCCcore-8.2.0                       | gettext/0.19.8.1-GCCcore-8.2.0|
|  Automake/1.16.1-GCCcore-8.2.0                    | Perl/5.30.0-GCCcore-8.3.0                   (D) | gettext/0.19.8.1|
|  Automake/1.16.1-GCCcore-8.3.0             (D)    | Python/2.7.15-GCCcore-8.2.0                     | gettext/0.20.1-GCC-9.2.0                 (D)|
|  Autotools/20180311-GCCcore-8.2.0                 | Python/3.7.2-GCCcore-8.2.0                      | gompi/2019a|
|  Autotools/20180311-GCCcore-8.3.0          (D)    | Python/3.8.2-GCC-9.2.0                      (D) | gompi/2019b                              (D)|
|  BWA/0.7.17-GCC-8.2.0-2.31.1                      | QUAST/5.0.2-foss-2019a-Python-3.7.2             | gompic/2019a|
|  BWA/0.7.17-GCC-8.3.0                      (D)    | SAMtools/1.9-GCC-8.2.0-2.31.1                   | gperf/3.1-GCCcore-8.2.0|
|  BioPerl/1.7.2-GCCcore-8.2.0-Perl-5.28.1          | SAMtools/1.10-GCC-8.3.0                     (D) | help2man/1.47.7-GCCcore-8.2.0|
|  Bison/3.0.5-GCCcore-8.2.0                        | SOAPdenovo2/r241-GCC-8.2.0-2.31.1               | help2man/1.47.8-GCCcore-8.3.0|
|  Bison/3.0.5                                      | SQLite/3.27.2-GCCcore-8.2.0                     | help2man/1.47.10-GCCcore-9.2.0           (D)|
|  Bison/3.3.2-GCCcore-8.3.0                        | SQLite/3.31.1-GCC-9.2.0                     (D) | hwloc/1.11.11-GCCcore-8.2.0|
|  Bison/3.3.2-GCCcore-9.2.0                        | Salmon/1.0.0-gompi-2019a                        | hwloc/1.11.12-GCCcore-8.3.0              (D)|
|  Bison/3.3.2                               (D)    | ScaLAPACK/2.0.2-gompi-2019a-OpenBLAS-0.3.5      | iccifort/2020.0.166|
|  Boost.Python/1.70.0-gompi-2019a                  | ScaLAPACK/2.0.2-gompi-2019b                 (D) | iimpi/2020.00|
|  Boost/1.70.0-gompi-2019a                         | SciPy-bundle/2019.03-foss-2019a                 | imkl/2020.0.166-iimpi-2020.00|
|  Bowtie2/2.3.5.1-GCC-8.2.0-2.31.1                 | Singularity/2.5.2-GCC-8.2.0-2.31.1              | impi/2019.6.166-iccifort-2020.0.166|
|  CMake/3.13.3-GCCcore-8.2.0                       | Singularity/3.5.3-GCC-8.2.0-2.31.1          (D) | intel/2020.00|
|  CUDA/10.1.105-GCC-8.2.0-2.31.1                   | Structure/2.3.4-GCC-8.2.0-2.31.1                | intltool/0.51.0-GCCcore-8.2.0|
|  DBus/1.13.8-GCCcore-8.2.0                        | Szip/2.1.1-GCCcore-8.2.0                        | jemalloc/5.2.0-GCCcore-8.2.0|
|  EasyBuild/4.1.0                                  | Tcl/8.6.9-GCCcore-8.2.0                         | libarchive/3.4.0-GCCcore-8.2.0|
|  EasyBuild/4.1.1                           (D)    | Tcl/8.6.10-GCC-9.2.0                        (D) | libffi/3.2.1-GCCcore-8.2.0|
|  FFTW/3.3.8-gompi-2019a                           | Tk/8.6.9-GCCcore-8.2.0                          | libffi/3.3-GCC-9.2.0                     (D)|
|  FFTW/3.3.8-gompi-2019b                    (D)    | Tkinter/3.7.2-GCCcore-8.2.0                     | libpciaccess/0.14-GCCcore-8.2.0|
|  GCC/8.2.0-2.31.1                                 | Trimmomatic/0.39-Java-11                        | libpciaccess/0.14-GCCcore-8.3.0          (D)|
|  GCC/8.3.0                                        | Trinity/2.9.0-foss-2019a                        | libpng/1.6.36-GCCcore-8.2.0|
|  GCC/9.2.0                                 (D)    | X11/20190311-GCCcore-8.2.0                      | libreadline/8.0-GCC-9.2.0|
|  GCCcore/8.2.0                                    | XML-LibXML/2.0200-GCCcore-8.2.0-Perl-5.28.1     | libreadline/8.0-GCCcore-8.2.0            (D)|
|  GCCcore/8.3.0                                    | XZ/5.2.4-GCC-9.2.0                              | libtool/2.4.6-GCCcore-8.2.0|
|  GCCcore/9.2.0                             (D)    | XZ/5.2.4-GCCcore-8.2.0                          | libtool/2.4.6-GCCcore-8.3.0              (D)|
|  GLib/2.60.1-GCCcore-8.2.0                        | XZ/5.2.4-GCCcore-8.3.0                      (D) | libxml2/2.9.8-GCCcore-8.2.0|
|  GMP/6.1.2-GCCcore-8.2.0                          | amrplusplus/v2                                  | libxml2/2.9.9-GCCcore-8.3.0              (D)|
|  GMP/6.2.0-GCC-9.2.0                       (D)    | amrplusplus/2.0-GCC-8.3.0                       | manta/1.6.0|
|  GSL/2.6-GCC-9.2.0                                | amrplusplus/2.0                             (D) | matplotlib/3.0.3-foss-2019a-Python-3.7.2|
|  Go/1.14                                          | ant/1.10.7-Java-11                              | ncurses/6.0|
|  Gubbins/2.4.0                                    | ant/1.10.7-Java-11.0                        (D) | ncurses/6.1-GCCcore-8.2.0|
|  HDF5/1.10.5-gompic-2019a                         | binutils/2.31.1-GCCcore-8.2.0                   | ncurses/6.1-GCCcore-8.3.0|
|  HTSlib/1.9-GCC-8.2.0-2.31.1                      | binutils/2.31.1                                 | ncurses/6.2-GCC-9.2.0                    (D)|
|  IntelDAAL/2019.4.007                             | binutils/2.32-GCCcore-8.3.0                     | nullarbor/2.0.20191013|
|  Java/11.0.2                               (11)   | binutils/2.32-GCCcore-9.2.0                     | numactl/2.0.12-GCCcore-8.2.0|
|  Jellyfish/2.3.0-foss-2019a                       | binutils/2.32                               (D) | numactl/2.0.12-GCCcore-8.3.0             (D)|
|  M4/1.4.18-GCCcore-8.2.0                          | bzip2/1.0.6-GCCcore-8.2.0                       | pkg-config/0.29.2-GCCcore-8.2.0|
|  M4/1.4.18-GCCcore-8.3.0                          | bzip2/1.0.8-GCC-9.2.0                           | tbb/2019_U4-GCCcore-8.2.0|
|  M4/1.4.18-GCCcore-9.2.0                          | bzip2/1.0.8-GCCcore-8.3.0                   (D) | util-linux/2.33-GCCcore-8.2.0|
|  M4/1.4.18                                 (D)    | cURL/7.63.0-GCCcore-8.2.0                       | xorg-macros/1.19.2-GCCcore-8.2.0|
|  MPFR/4.0.2-GCC-9.2.0                             | cURL/7.66.0-GCCcore-8.3.0                   (D) | xorg-macros/1.19.2-GCCcore-8.3.0         (D)|
|  Meson/0.50.0-GCCcore-8.2.0-Python-3.7.2          | dbus-glib/0.110-GCCcore-8.2.0                   | zlib/1.2.11-GCC-9.2.0|
|  Miniconda3/4.7.10                                | expat/2.2.6-GCCcore-8.2.0                       | zlib/1.2.11-GCCcore-8.2.0|
|  Mothur/1.43.0-foss-2019a                         | expat/2.2.7-GCCcore-8.3.0                   (D) | zlib/1.2.11-GCCcore-8.3.0|
|  Nextflow/19.12.0                                 | flex/2.6.4-GCCcore-8.2.0                        | zlib/1.2.11-GCCcore-9.2.0|
|  Ninja/1.9.0-GCCcore-8.2.0                        | flex/2.6.4-GCCcore-8.3.0                        | zlib/1.2.11                              (D)|
|  OpenBLAS/0.3.5-GCC-8.2.0-2.31.1                  | flex/2.6.4-GCCcore-9.2.0                    (D)|
|  OpenBLAS/0.3.7-GCC-8.3.0                  (D)    | fontconfig/2.13.1-GCCcore-8.2.0|