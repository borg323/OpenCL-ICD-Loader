project('OPENCL_ICD_LOADER', 'c', default_options : ['default_library=static'])

run_command('git', 'clone', '--depth=1',
            'https://github.com/KhronosGroup/OpenCL-Headers.git',
            'include')

opencl_icd_loader_sources = ['loader/icd.c', 'loader/icd_dispatch.c']
# ['loader/windows/icd_windows.c', 'loader/windows/icd_windows_hkr.c', 'loader/windows/OpenCL.def', 'loader/windows/OpenCL.rc']
opencl_icd_loader_sources += ['loader/linux/icd_linux.c']

opencl_headers = include_directories('include')

opencl_lib = library('OpenCL', opencl_icd_loader_sources,
                     include_directories: [include_directories('loader'), opencl_headers])

opencl_dep = declare_dependency(
  link_with : opencl_lib,
  include_directories : opencl_headers)


