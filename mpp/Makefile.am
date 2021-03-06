#***********************************************************************
#*                   GNU Lesser General Public License
#*
#* This file is part of the GFDL Flexible Modeling System (FMS).
#*
#* FMS is free software: you can redistribute it and/or modify it under
#* the terms of the GNU Lesser General Public License as published by
#* the Free Software Foundation, either version 3 of the License, or (at
#* your option) any later version.
#*
#* FMS is distributed in the hope that it will be useful, but WITHOUT
#* ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or
#* FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License
#* for more details.
#*
#* You should have received a copy of the GNU Lesser General Public
#* License along with FMS.  If not, see <http://www.gnu.org/licenses/>.
#***********************************************************************

# This is an automake file for the mpp directory of the MPP
# package.

# Ed Hartnett 2/22/19

# Descend into include directory.
SUBDIRS = include

# Include .h and .mod files.
AM_CPPFLAGS = -I${top_srcdir}/include
AM_CPPFLAGS += -I${top_srcdir}/mpp/include

# Build these uninstalled convenience libraries.
noinst_LTLIBRARIES = libmpp_parameter.la libmpp_data.la libmpp.la \
libmpp_utilities.la libmpp_memutils.la libmpp_pset.la libmpp_efp.la \
libmpp_domains.la libmpp_io.la libmpp_c.la libmpp_memuse_c.la

# Each convenience library depends on its source.
libmpp_parameter_la_SOURCES = mpp_parameter.F90
libmpp_la_SOURCES = mpp.F90
libmpp_data_la_SOURCES = mpp_data.F90
libmpp_utilities_la_SOURCES = mpp_utilities.F90
libmpp_domains_la_SOURCES = mpp_domains.F90
libmpp_io_la_SOURCES = mpp_io.F90
libmpp_pset_la_SOURCES = mpp_pset.F90
libmpp_efp_la_SOURCES = mpp_efp.F90
libmpp_c_la_SOURCES = nsclock.c threadloc.c
libmpp_memutils_la_SOURCES = mpp_memutils.F90
libmpp_memuse_c_la_SOURCES = mpp_memuse.c

# Each mod file depends on the .o file.
mpp_parameter_mod.mod: mpp_parameter.lo
mpp_data_mod.mod: mpp_data.lo
mpp_mod.mod: mpp.lo
mpp_pset_mod.mod: mpp_pset.lo
mpp_utilities_mod.mod: mpp_utilities.lo
mpp_memutils_mod.mod: mpp_memutils.lo
mpp_efp_mod.mod: mpp_efp.lo
mpp_domains_mod.mod: mpp_domains.lo
mpp_io_mod.mod: mpp_io.lo

# Some mods are dependant on other mods in this dir.
mpp_data.lo: mpp_parameter_mod.mod
mpp.lo: mpp_data_mod.mod
mpp_utilities.lo: mpp_mod.mod mpp_efp_mod.mod
mpp_memutils.lo: mpp_mod.mod
mpp_pset.lo: mpp_mod.mod
mpp_efp.lo: mpp_parameter_mod.mod mpp_mod.mod
mpp_domains.lo: mpp_data_mod.mod mpp_parameter_mod.mod mpp_mod.mod	\
mpp_memutils_mod.mod mpp_pset_mod.mod mpp_efp_mod.mod
mpp_io.lo: mpp_parameter_mod.mod mpp_mod.mod mpp_domains_mod.mod

# Mod files are built and then installed as headers.
MODFILES = mpp_parameter_mod.mod mpp_data_mod.mod mpp_mod.mod \
mpp_utilities_mod.mod mpp_memutils_mod.mod mpp_pset_mod.mod \
mpp_efp_mod.mod mpp_domains_mod.mod mpp_io_mod.mod
include_HEADERS = $(MODFILES)
BUILT_SOURCES = $(MODFILES)

CLEANFILES = *.mod
