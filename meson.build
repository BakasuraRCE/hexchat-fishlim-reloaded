project('fishlim_reloaded', 'c',
  version: '1.0.0',
  meson_version: '>= 0.40.0',
  default_options: [
    'c_std=gnu89',
    'buildtype=debugoptimized',
    'warning_level=1',
  ]
)

hexchat_dep = dependency('hexchat-plugin')

libgio_dep = dependency('gio-2.0', version: '>= 2.34.0')

cc = meson.get_compiler('c')

if cc.get_id() == 'msvc'
  libssl_dep = cc.find_library('libeay32')
else
  libssl_dep = dependency('openssl', version: '>= 0.9.8')
endif

if not libssl_dep.found()
  error('fish plugin requires openssl')
endif

config_h = configuration_data()

config_h.set('HAVE_DH_SET0_PQG',
  cc.has_function('DH_set0_pqg', dependencies: libssl_dep)
)
config_h.set('HAVE_DH_GET0_KEY',
  cc.has_function('DH_get0_key', dependencies: libssl_dep)
)
config_h.set('HAVE_DH_SET0_KEY',
  cc.has_function('DH_set0_key', dependencies: libssl_dep)
)

configure_file(output: 'config.h', configuration: config_h)
config_h_include = include_directories('.')

fishlim_sources = [
  'dh1080.c',
  'fish.c',
  'irc.c',
  'keystore.c',
  'plugin_hexchat.c'
]

if get_option('local_install')
  message('Using local install')
  # Replace this with check: true in 0.47+
  ret = run_command([find_program('hexchat'), '--configdir'])
  if ret.returncode() != 0
    error('Failed to get hexchat configdir')
  endif
  hexchatplugindir = join_paths(ret.stdout().strip(), 'addons')
else
  message('Using global install')
  hexchatplugindir = hexchat_dep.get_pkgconfig_variable('hexchatlibdir')
endif
message('Install location: ' + hexchatplugindir)

shared_module('fishlim_reloaded', fishlim_sources,
  dependencies: [libgio_dep, libssl_dep],
  include_directories: config_h_include,
  install: true,
  install_dir: hexchatplugindir,
  name_prefix: '',
)
