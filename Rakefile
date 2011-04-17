require 'rake/clean'
require 'haml'
require 'sass'

HAML = FileList.new('**/*.haml').ext('html')
SCSS = FileList.new('**/*.scss').ext('css')
CLOBBER.include HAML + SCSS

rule '.html' => '.haml' do |t|
  puts "Generating #{t.name}"
  File.open(t.name, 'w') { |f| f << Haml::Engine.new(open(t.source).read).render }
end

rule '.css' => '.scss' do |t|
  puts "Generating #{t.name}"
  File.open(t.name, 'w') { |f| f << Sass::Engine.new(open(t.source).read, :syntax => :scss, :style => :compressed).render }
end

desc 'Generate html and css from sources'
task :default => HAML + SCSS do
end

desc 'Build and start server'
task :server => :default do
  sh %{ jekyll --server --safe }
end

