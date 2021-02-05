# SPDX-License-Identifier: LGPL-2.1-or-later

sources = files('''
        lldp-internal.h
        lldp-network.h
        lldp-network.c
        lldp-neighbor.h
        lldp-neighbor.c
        sd-lldp.c
'''.split())

libsystemd_lldp = static_library(
        'systemd-lldp',
        sources,
        include_directories : includes)

libsystemd_lldp_sym = files('libsystemd-lldp.sym')
libsystemd_lldp_sym_path = join_paths(meson.current_source_dir(), 'libsystemd-lldp.sym')

configure_file(
        input : 'libsystemd-lldp.pc.in',
        output : 'libsystemd-lldp.pc',
        configuration : substs,
        install_dir : pkgconfiglibdir == 'no' ? '' : pkgconfiglibdir)

libsystemd_lldp_includes = [includes, include_directories('.')]

############################################################

tests += [
        [['src/libsystemd-lldp/test-lldp.c'],
         [libshared,
          libsystemd_lldp]],
]

fuzzers += [
        [['src/libsystemd-lldp/fuzz-lldp.c'],
         [libshared,
          libsystemd_lldp]],
]
