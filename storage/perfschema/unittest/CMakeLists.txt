# Copyright (c) 2009, 2015, Oracle and/or its affiliates. All rights reserved.
#
# This program is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; version 2 of the License.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 51 Franklin St, Fifth Floor, Boston, MA  02110-1301  USA

INCLUDE_DIRECTORIES(${CMAKE_SOURCE_DIR}/include
                    ${CMAKE_SOURCE_DIR}/include/mysql
                    ${PCRE_INCLUDES}
                    ${CMAKE_SOURCE_DIR}/sql
                    ${SSL_INCLUDE_DIRS}
                    ${CMAKE_SOURCE_DIR}/unittest/mytap
                    ${CMAKE_SOURCE_DIR}/storage/perfschema)

ADD_DEFINITIONS(-DMYSQL_SERVER ${SSL_DEFINES})

ADD_CONVENIENCE_LIBRARY(pfs_server_stubs pfs_server_stubs.cc)

ADD_DEPENDENCIES(pfs_server_stubs GenError)

MY_ADD_TESTS(pfs_instr_class pfs_instr_class-oom pfs_instr pfs_instr-oom
             pfs_account-oom pfs_host-oom pfs_timer pfs_user-oom pfs
  EXT "cc" LINK_LIBRARIES perfschema mysys pfs_server_stubs)
