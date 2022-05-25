project(
    'phosphor-ledcontroller', 'cpp',
    version : '1.0.0',
    meson_version: '>=0.57.0',
    default_options: [
        'warning_level=3',
        'werror=true',
        'cpp_std=c++20',
        'buildtype=debugoptimized'
    ]
)

conf_data = configuration_data()
conf_data.set_quoted('BUSNAME', 'xyz.openbmc_project.LED.Controller')
conf_data.set_quoted('OBJPATH', '/xyz/openbmc_project/led/physical')
conf_data.set_quoted('DEVPATH', '/sys/class/leds/')

sdbusplus_dep = dependency('sdbusplus')
phosphor_dbus_interfaces_dep = dependency('phosphor-dbus-interfaces')

deps = [
    sdbusplus_dep,
    phosphor_dbus_interfaces_dep,
]


configure_file(output: 'config.h',
    configuration: conf_data
)

sources = [
    'argument.cpp',
    'controller.cpp',
    'physical.cpp',
    'sysfs.cpp',
]

executable(
    'phosphor-ledcontroller',
    sources,
    implicit_include_directories: true,
    dependencies: deps,
    install: true,
    install_dir: '/usr/sbin'
)

build_tests = get_option('tests')
if build_tests.enabled()
  subdir('test')
endif
