require_relative 'lib/calaboose'

require 'bundler/gem_tasks'
require 'rspec/core/rake_task'

begin
  require_relative 'config'
rescue LoadError
  CONFIG = {}
end

inmate_dir = File.join(File.dirname(__FILE__), 'spec', 'test_inmate')
CONFIG[:inmate_dir] = inmate_dir
CONFIG[:image_name] = Calaboose.new(CONFIG).image_name

RSpec::Core::RakeTask.new(:spec)
Rake::Task[:spec].prerequisites << :bootstrap_docker
task :default => :spec

def calaboose
  @calaboose ||= CalabooseTest.new CONFIG
end

desc "Benchmark render_reverse run in docker"
task :benchmark => :bootstrap_docker do
  10.times do |i|
    sleep 0.5
    start = Time.now
    each_calaboose "foobar"
    puts "render_reverse run ##{i} took #{Time.now - start} seconds"
  end
  Calaboose.cleanup
end

desc "Building docker image."
task :bootstrap_docker do
  each_calaboose.build_image unless calaboose.image_exists?
end