\page cmake Building jedi-bundle on the Mac with FMS@2023.04
# Instructions for building jedi-bundle on the Mac with FMS@2023.04

## 1. Set up a work area

You will need to clone FMS and jedi-bundle, plus have directories for building both, and one more directory for installing FMS.
Here is an example directory structure:

```
~/projects/JEDI/
             fms-build
             fms-install
             jedi-build

```

Note that you need to do a `module unload fms` after you source your setup file and before you continue with the following steps.

## 2. Build and install FMS

Using the example directory structure above:

```
# clone FMS
cd ~/projects/JEDI
git clone https://github.com/JCSDA/FMS.git
cd FMS
git checkout feature/mac-fms-2023.04

# build/install FMS
cd ~/project/JEDI/fms-build
cmake -DCMAKE_INSTALL_PREFIX=~/projects/JEDI/fms-install ../FMS
make -j<n>
make install
```

Currently, only the RelWithDebInfo build of FMS is working.
The Debug build did not work when I tried it, but I'm sure it can be fixed (and perhaps it is in the latest FMS version).

## 3. Build and test jedi-bundle

Currently, you will need to set two paths for FMS so that all the packages in jedi-bundle can find the installation you just built.
This is because some packages list "FMS" as a dependency (used in find_package) and others list "fms".

```
cd ~/projects/JEDI/jedi-build
export fms_ROOT=~/projects/JEDI/fms-install
export FMS_ROOT=~/projects/JEDI/fms-install
ecbuild -DCMAKE_SHARED_LINKER_FLAGS="-ld_classic ${llvm_openmp_ROOT}/lib/libomp.dylib" -DCMAKE_EXE_LINKER_FLAGS="-ld_classic" -DCMAKE_MODULE_LINKER_FLAGS="-ld_classic" ../jedi-bundle
make -j<n>
ctest

```
