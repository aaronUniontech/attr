# Copyright (C) 2009  Andreas Gruenbacher <agruen@suse.de>
#
# This program is free software: you can redistribute it and/or modify it
# under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 2 of the License, or
# (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program.  If not, see <http://www.gnu.org/licenses/>.
#

AC_PREREQ([2.59])
AC_INIT([attr], [2.5.1], [acl-devel@nongnu.org])
AC_CONFIG_AUX_DIR([build-aux])
AC_CONFIG_MACRO_DIR([m4])
AC_CONFIG_HEADER([include/config.h])
AC_PREFIX_DEFAULT(/usr)

AM_INIT_AUTOMAKE([-Wall foreign 1.11 dist-xz subdir-objects])
AM_SILENT_RULES([yes])

AC_CANONICAL_HOST
AC_PROG_CC
AM_PROG_CC_C_O
AC_USE_SYSTEM_EXTENSIONS
AC_C_CONST
AC_TYPE_MODE_T
AC_FUNC_ALLOCA
AC_FUNC_GCC_VISIBILITY
AC_SYS_LARGEFILE

AM_PROG_AR
LT_INIT

# Require at least this gettext version, but will take any later version too.
AM_GNU_GETTEXT_REQUIRE_VERSION([0.19.8])
# XXX: We cannot remove the following macro due to backwards compatibility
# reasons. The above macro is set unconditionally to the minimal version
# required, and the below is set to 0.19.6, the first version introducing
# the AM_GNU_GETTEXT_REQUIRE_VERSION macro.
AM_GNU_GETTEXT_VERSION([0.19.6])
AM_GNU_GETTEXT([external])

AC_ARG_ENABLE([debug],
	[AS_HELP_STRING([--enable-debug], [Enable extra debugging])])
AS_IF([test "x$enable_debug" = "xyes"],
	[CPPFLAGS="$CPPFLAGS -DDEBUG"],
	[CPPFLAGS="$CPPFLAGS -DNDEBUG"])

dnl Automatically increment the revision for every release.
set -- $(IFS=.; echo ${PACKAGE_VERSION})
if test $# -ne 3 -o ${#1} -gt 1 -o ${#2} -gt 1 -o ${#3} -gt 2; then
	echo "This PACKAGE_VERSION breaks LT_REVISION" >&2
	exit 1
fi
LT_REVISION=$(printf "%d%d%02d" "$1" "$2" "$3")
AC_SUBST(LT_REVISION)

AS_CASE([$host_os],
	[linux*], [os_linux=yes],
)
AM_CONDITIONAL([OS_LINUX], [test "x$os_linux" = "xyes"])

AC_CONFIG_COMMANDS([include/attr],
	[dnl
	rm -rf include/attr
	$as_ln_s "$ac_abs_top_srcdir/include" include/attr
	])
AC_CONFIG_FILES([
	libattr.pc
	Makefile
	po/Makefile.in
])
AC_OUTPUT
