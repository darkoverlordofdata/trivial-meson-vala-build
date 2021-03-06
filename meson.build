# project name and programming language
project('com.github.darkoverlordofdata.trivial', ['vala', 'c'], version: '0.0.1')

# Add vapi files
add_project_arguments(
  [
    '--vapidir',
    join_paths(meson.current_source_dir(), 'vapi')
  ],
  language: 'vala'
)

# Set configuration data
conf = configuration_data()
conf.set_quoted('GETTEXT_PACKAGE', meson.project_name())
conf.set_quoted('PREFIX', get_option('prefix'))
conf.set_quoted('VERSION', meson.project_version())
conf.set_quoted('PACKAGE', meson.project_name())
conf.set_quoted('LOCALE_DIR', join_paths(get_option('prefix'), get_option('localedir')))
conf.set_quoted('DATADIR', join_paths(get_option('prefix'), get_option('datadir')))
conf.set_quoted('PKG_DATADIR', join_paths(get_option('prefix'), get_option('datadir'), meson.project_name()))

configure_file(
  output: 'config.h',
  configuration: conf
)

subdir('data')

# Create a new executable
executable(
    meson.project_name(),
    'src/main.vala', 
    'src/constants.vala',
    'src/application.vala',
    'src/application-window.vala',
    'src/application-preferences.vala',
    import('gnome').compile_resources(
        'gresource', join_paths('data', meson.project_name() + '.gresource.xml'),
        source_dir: 'data',
        c_name: 'trivial'
    ),
    c_args: [
      '-include', 'config.h',
      '-w', 
      '-DGETTEXT_PACKAGE="' + meson.project_name() + '"'
    ],
    vala_args: [
        meson.source_root() + '/vapi/config.vapi'
    ],
    dependencies: [
        dependency('gio-2.0'),
        dependency('gobject-2.0'),
        dependency('gee-0.8'),
        dependency('glib-2.0'),
        dependency('gtk+-3.0'),
        meson.get_compiler('c').find_library('m', required: false)        
    ],
    # link_args: ['-lm'],
    install: true
)

# Add post install script
meson.add_install_script('meson/post_install.py')
