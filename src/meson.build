
sources = files(
    'area.vala',
    'axis.vala',
    'background.vala',
    'bar.vala',
    'bezier.vala',
    'bounds.vala',
    'chart.vala',
    'config.vala',
    'drawable.vala',
    'font.vala',
    'geometry.vala',
    'grid.vala',
    'labels.vala',
    'legend.vala',
    'line_area.vala',
    'line.vala',
    'max_bound_line.vala',
    'min_bound_line.vala',
    'path.vala',
    'points.vala',
    'region/region.vala',
    'region/curve_resolver.vala',
    'region/intersections.vala',
    'region/bezier_intersector.vala',
    'region/segment_intersector.vala',
    'serie.vala',
    'serie_renderer.vala',
    'series.vala',
    'smooth_line_area.vala',
    'smooth_line.vala',
    'time_seek.vala',
    'threshold_line.vala',
    'utils.vala',
    'values.vala',
    'static/static_chart.vala',
    'static/static_series.vala',
    'static/static_serie.vala',
    'static/static_values.vala',
    'static/static_serie_renderer.vala',
    'static/static_line.vala',
    'static/static_grid.vala',
    'static/static_points.vala'
)

livechart_static_lib = static_library('livechart_static', [sources], dependencies: deps, vala_args: vala_args)
livechart_static_dep = declare_dependency(include_directories: include_directories('.'), link_with: livechart_static_lib)

livechart_lib = library(
    'livechart',
    [sources],
    dependencies: deps,
    vala_args: vala_args,
    vala_gir: 'LiveChart-1.10.gir',
    version: meson.project_version(),
    install: true,
    install_dir: [true, true, true, true]
)

pkg = import('pkgconfig')
pkg.generate(
    version: meson.project_version(),
    libraries: livechart_lib,
    description: 'Live-chart headers',
    name: 'livechart',
    filebase: 'livechart'
)

livechart_dep = declare_dependency(
    link_with: livechart_lib,
    dependencies: deps,
    include_directories: [include_directories('.')]
)

gir_file = meson.current_build_dir() / 'LiveChart-1.10.gir'

g_ir_compiler = find_program('g-ir-compiler')

typelib = custom_target('LiveChart typelib',
  input: gir_file,
  output: 'LiveChart-1.10.typelib',
  command: [g_ir_compiler, '--output=@OUTPUT@', '@INPUT@'],
  install: true,
  install_dir: get_option('libdir') / 'girepository-1.0',
  depends: livechart_lib
  )
