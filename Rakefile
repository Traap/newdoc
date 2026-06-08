# frozen_string_literal: true

require 'fileutils'
require 'rake'
require 'tmpdir'

SMOKE_ROOT = '/tmp/newdoc'
SMOKE_DOC_DIR = 'smoke/tech-report'
SMOKE_PDF = File.join(SMOKE_ROOT, '_build', 'tech-report.pdf')

task default: %i[lint smoke]

desc 'Run RuboCop'
task :lint do
  sh({ 'RUBOCOP_CACHE_ROOT' => Dir.tmpdir }, 'rubocop')
end

desc 'Generate and build a persistent smoke document under /tmp/newdoc'
task :smoke do
  prepare_smoke_root

  Dir.chdir(SMOKE_ROOT) do
    sh smoke_env, *newdoc_command
    assert_file 'smoke/tech-report/tech-report.tex'
    assert_file 'smoke/tech-report/tech-report.texx'
    assert_file 'smoke/tech-report/data/additional-layout.tex'
    assert_file 'smoke/tech-report/data/header-footer.tex'
    assert_file 'smoke/tech-report/data/logo.png'
    assert_file 'smoke/tech-report/test-output/test-results.tex'
    assert_file 'smoke/shared/data/additional-layout.tex'
    assert_file 'smoke/shared/data/header-footer.tex'
    sh smoke_env, 'docbld', 'deploy'
  end

  assert_file SMOKE_PDF
end

def assert_file(path)
  return if File.file?(path)

  raise "Expected #{path} to be generated"
end

def prepare_smoke_root
  FileUtils.mkdir_p(SMOKE_ROOT)
  FileUtils.rm_rf(File.join(SMOKE_ROOT, 'smoke'))
  FileUtils.rm_rf(File.join(SMOKE_ROOT, '_build'))
end

def smoke_env
  {
    'NEWDOCPATH' => __dir__,
    'RUBOCOP_CACHE_ROOT' => Dir.tmpdir
  }
end

def newdoc_command
  [
    Gem.ruby,
    File.join(__dir__, 'newdoc'),
    "--dir=#{SMOKE_DOC_DIR}",
    '--file=tech-report',
    '--title=Smoke Technical Report',
    '--type=stdTechReportDoc',
    '--shared',
    '--logo',
    '--tof'
  ]
end
