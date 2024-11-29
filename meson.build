project(
  'libfoldy',
  ['c', 'vala'],
  version: '1.4',
  meson_version: '>= 1.0.0',
  license: 'GPL-3.0-or-later',
)

api_version = '1'
glib_min_version = '2.76'

lib_name = 'foldy'
project_name = meson.project_name()
gir_name = 'Foldy'

versioned_name = meson.project_name() + '-' + api_version
versioned_gir_name = gir_name + '-' + api_version

deps_name = versioned_name + '.deps'
header_name = project_name + '.h'
vapi_name = versioned_name + '.vapi'
gir_name = versioned_gir_name + '.gir'
typelib_name = versioned_gir_name + '.typelib'

pkgconfig = import('pkgconfig')
gnome = import('gnome')

deps_pkgs = [
  'gio-2.0',
]

gio_dep = dependency('gio-2.0')

dependencies = [
  gio_dep,
]

add_project_arguments(
  '-DGETTEXT_PACKAGE="@0@"'.format(meson.project_name()),
  # GCC14 COMPILE ERROR
  '-Wno-int-conversion',
  language: ['c'],
)

add_project_arguments(
  '--abi-stability',
  '--hide-internal',
  '--target-glib', glib_min_version,
  '--vapidir', meson.current_source_dir(),
  language: ['vala'],
)

subdir('lib')

if get_option('documentation')
  subdir('doc')
endif

gnome.post_install()
