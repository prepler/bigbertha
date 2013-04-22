require 'bundler'

Bundler.require

Bundler::GemHelper.install_tasks

$LOAD_PATH.unshift File.expand_path("../lib", __FILE__)
load 'tasks/auth_token.rake'

require 'rspec/core/rake_task'
RSpec::Core::RakeTask.new(:spec) do |t|
  t.verbose = false
  t.ruby_opts = "-I./spec"
end

desc 'Cleanup build artifacts'
task :clean do
  cov = File.expand_path( File.join( %w(.. coverage) ), __FILE__ ) 
  FileUtils.rm_r( cov ) if File.exists?( cov )
  pkg = File.expand_path( File.join( %w(.. pkg) ), __FILE__ ) 
  FileUtils.rm_r( pkg ) if File.exists?( pkg )  
end

desc 'Run samples'
task :samples do
  path = File.expand_path( File.join( %w(.. examples ** *.rb) ), __FILE__ )
puts path.inspect  
  Dir.glob(path).sort.each { |example| puts example;%x(ruby #{example}) }
end

task default: :spec