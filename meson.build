project('py-design', 'c', 'fortran',
  version: '2.1.0',
  default_options: [
    'warning_level=1',
  ],
)

py = import('python').find_installation(pure: false)
py_dep = py.dependency()

incdir_numpy = run_command(py,
  ['-c', 'import numpy; print(numpy.get_include())'],
  check: true
).stdout().strip()

incdir_f2py = incdir_numpy / '..' / '..' / 'f2py' / 'src'

fortran_sources = [
  'src/faure.f90',
  'src/halton.f90',
  'src/hammersley.f90',
  'src/ihs.f90',
  'src/lambert.f90',
  'src/latin_center.f90',
  'src/latin_cover.f90',
  'src/latin_edge.f90',
  'src/latin_random.f90',
  'src/latinize.f90',
  'src/sandia_sparse.f90',
  'src/sobol.f90',
]

inc_dirs = include_directories(incdir_numpy, incdir_f2py)

# Platform-specific link args
extra_link_args = []
if host_machine.system() == 'darwin'
  extra_link_args = ['-undefined', 'dynamic_lookup']
endif

py.extension_module(
  '_design',
  fortran_sources,
  include_directories: inc_dirs,
  dependencies: py_dep,
  link_args: extra_link_args,
  install: true,
  subdir: 'design',
)

py.install_sources(
  ['design/__init__.py'],
  subdir: 'design',
)
