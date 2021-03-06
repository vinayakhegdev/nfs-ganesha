if(USE_DBUS)
  include_directories(
    ${DBUS_INCLUDE_DIRS}
    )
endif(USE_DBUS)

# string utilities.  This should eventually go into src/os
# because BSD has them and Linux doesn't

set(string_utils_STAT_SRCS
   strlcpy.c
   strnlen.c
)

add_library(string_utils STATIC ${string_utils_STAT_SRCS})

# hash function libraries

set(hash_SRCS
   murmur3.c
   city.c
)

add_library(hash STATIC ${hash_SRCS})

# uid2grp mapper
set( uid2grp_SRCS
     uid2grp.c
     uid2grp_cache.c
)

add_library( uid2grp STATIC ${uid2grp_SRCS} )

# netgroup cache
set(netgroup_cache_SRCS
    netgroup_cache.c
)
add_library(netgroup_cache STATIC ${netgroup_cache_SRCS} )

########### next target ###############

SET(support_STAT_SRCS
   nfs4_acls.c
   nfs_creds.c
   nfs_filehandle_mgmt.c
   nfs_read_conf.c
   nfs_convert.c
   nfs_ip_name.c
   ds.c
   exports.c
   fridgethr.c
   delayed_exec.c
   misc.c
   bsd-base64.c
   server_stats.c
   export_mgr.c
)

if(ERROR_INJECTION)
  set(support_STAT_SRCS
    ${support_STAT_SRCS}
    err_inject.c
    )
endif(ERROR_INJECTION)

if(APPLE)
  set(support_STAT_SRCS
    ${support_STAT_SRCS}
    misc.c
    )
endif(APPLE)

add_library(support STATIC ${support_STAT_SRCS})

########### install files ###############
