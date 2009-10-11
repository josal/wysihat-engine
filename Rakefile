require 'rake'
require 'rake/testtask'
require 'rake/rdoctask'

desc 'Default: run unit tests.'
task :default => :test

desc 'Test the wysihat_engine plugin.'
Rake::TestTask.new(:test) do |t|
  t.libs << 'lib'
  t.libs << 'test'
  t.pattern = 'test/**/*_test.rb'
  t.verbose = true
end

desc 'Generate documentation for the wysihat_engine plugin.'
Rake::RDocTask.new(:rdoc) do |rdoc|
  rdoc.rdoc_dir = 'rdoc'
  rdoc.title    = 'WysihatEngine'
  rdoc.options << '--line-numbers' << '--inline-source'
  rdoc.rdoc_files.include('README')
  rdoc.rdoc_files.include('lib/**/*.rb')
end

desc 'minify and concatenate the javascript files to make a pack'
task :minify do
  require "yui/compressor"

  compressor = YUI::JavaScriptCompressor.new(:munge => true)
  dir = 'generators/wysihat/templates/javascripts'
  pack = File.new("#{dir}/wysihat_engine_pack.js", "w")

  string = ''
  files = ['facebox', 'wysihat', 'wysihat_engine']
  files.each do |file|
    file = open("#{dir}/#{file}.js")
    string << file.read
    file.close
  end
  
  pack.write(compressor.compress(string))
  pack.close
end  

begin
  require 'jeweler'
  Jeweler::Tasks.new do |gem|
    gem.name = "wysihat-engine"
    gem.summary = "A Rails engine to help integrate the 37signals WyshiHat rich text editor to your application."
    gem.description = "A Rails engine to help integrate the 37signals WyshiHat rich text editor to your application."
    gem.email = "jeff@80beans.com"
    gem.homepage = "http://www.80beans.com/2009/10/01/wysihat-engine/"
    gem.authors = ["Jeff Kreeftmeijer"]
    gem.add_development_dependency "yui-compressor", ">= 0.9.1"
    gem.add_dependency 'thoughtbot-paperclip', ">= 2.3.1"
  end
rescue LoadError
  puts "Jeweler not available. Install it with: sudo gem install technicalpickles-jeweler -s http://gems.github.com"
end                                                                    

Jeweler::GemcutterTasks.new