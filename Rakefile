require 'bundler'
Bundler.setup

require "rspec"
require "rspec/core/rake_task"

$LOAD_PATH.unshift File.expand_path("../lib", __FILE__)
require "avburn/version"

desc "Builds the gem"
task :gem => :build
task :build do
  system "gem build avburn.gemspec"
  Dir.mkdir("pkg") unless Dir.exists?("pkg")
  system "mv avburn-#{Avburn::VERSION}.gem pkg/"
end

task :install => :build do
  system "sudo gem install pkg/avburn-#{Avburn::VERSION}.gem"
end

desc "Release the gem - Gemcutter"
task :release => :build do
  system "git tag -a v#{Avburn::VERSION} -m 'Tagging #{Avburn::VERSION}'"
  system "git push --tags"
  system "gem push pkg/avburn-#{Avburn::VERSION}.gem"
end


RSpec::Core::RakeTask.new(:spec) do |spec|
  spec.pattern = "spec/**/*_spec.rb"
end

task :default => [:spec]
