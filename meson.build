project ('compact_enc_det',
	'cpp',
	meson_version: '>=0.53.0',
	default_options : ['cpp_std=c++11','buildtype=debugoptimized'],
	license: ['GPL3']
)

thread_dep = dependency('threads')

ced_sources = [
	'compact_enc_det/compact_enc_det.cc',
	'compact_enc_det/compact_enc_det_hint_code.cc',
	'util/encodings/encodings.cc',
	'util/languages/languages.cc']
	
compiler=meson.get_compiler('cpp')

if compiler.get_id() == 'gcc'
	add_project_arguments('-Wno-narrowing', language:'cpp')
elif compiler.get_id() == 'clang'
	add_project_arguments('-Wno-c++11-narrowing', language: 'cpp')
elif compiler.get_id() == 'msvc'
	add_project_arguments('/MT', language: 'cpp')
endif

if build_machine.system() == 'windows'
	add_project_arguments(
		'-DUNICODE',
		'-D_UNICODE',
		'-DSTRICT',
		'-DNOMINMAX',
		language: 'cpp'
	)
endif

compact_enc_det = static_library(
	'compact_enc_det',
	ced_sources,
	include_directories:'compact_enc_det',
	dependencies: thread_dep
)

compact_enc_det_dep = declare_dependency(
	link_with: compact_enc_det,
	include_directories:'compact_enc_det'
)