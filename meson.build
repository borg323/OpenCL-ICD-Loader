project('OPENCL_ICD_LOADER', 'c', default_options : ['default_library=static'])

cc = meson.get_compiler('c')

add_project_arguments('-DCL_TARGET_OPENCL_VERSION=220', language : 'c')

run_command('git', 'clone', '--depth=1',
            'https://github.com/KhronosGroup/OpenCL-Headers.git',
            'include')
deps = []

opencl_icd_loader_sources = ['loader/icd.c', 'loader/icd_dispatch.c']

if host_machine.system() == 'windows'
  deps += cc.find_library('Cfgmgr32')
  opencl_icd_loader_sources += ['loader/windows/icd_windows.c',
                                'loader/windows/icd_windows_hkr.c']
else
  deps += [cc.find_library('pthread'), cc.find_library('dl')]
  opencl_icd_loader_sources += 'loader/linux/icd_linux.c'
endif

opencl_headers = include_directories('include')

opencl_lib = library('OpenCL', opencl_icd_loader_sources,
                     dependencies: deps,
                     include_directories: [include_directories('loader'), opencl_headers])

opencl_dep = declare_dependency(link_with : opencl_lib, include_directories : opencl_headers)


