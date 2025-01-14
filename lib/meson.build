vapi_sources = files(
  
)

vala_sources = files(
  'folder.vala',
  'folders.vala',
)

sources = [
  vapi_sources,
  vala_sources,
]

lib = shared_library(
  versioned_name,
  sources,
  dependencies: dependencies,
  vala_header: header_name,
  vala_vapi: vapi_name,
  vala_gir: gir_name,
  version: meson.project_version(),
  install: true,
  install_dir: [ true, true, true, true ],
)

lib_dep = declare_dependency(
  link_with: lib,
  include_directories: include_directories('.'),
  dependencies: dependencies
)

deps_conf = configuration_data()
deps_conf.set ('DEPS',  '\n'.join (deps_pkgs))

configure_file(
  input: 'lib.deps.in',
  output: deps_name,
  configuration: deps_conf,
  install: true,
  install_dir: get_option('datadir') / 'vala' / 'vapi',
)

if get_option('introspection')
  g_ir_compiler = find_program('g-ir-compiler')
  custom_target(
    'typelib',
    command: [
      g_ir_compiler,
      '--shared-library', '@PLAINNAME@',
      '--output', '@OUTPUT@',
      meson.current_build_dir() / gir_name,
    ],
    input: lib,
    output: typelib_name,
    depends: lib,
    install: true,
    install_dir: get_option('libdir') / 'girepository-1.0',
  )
endif

pkgconfig.generate(
  lib,
  name: versioned_lib_name,
  requires: dependencies,
  subdirs: [ versioned_name ],
  description: 'Functions for work with folders on GNOME',
  version: meson.project_version(),
  url: 'https://github.com/alt-gnome/libfoldy',
)
