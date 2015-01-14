#!/usr/bin/env rake
require File.expand_path('../lib/bootstrap-wysihtml5-rails/version', __FILE__)
require 'json'

BASE_FOLDER = 'bootstrap3-wysihtml5/dist'

def copy_javascript
  puts "#{BASE_FOLDER}/bootstrap3-wysihtml5.min.js"
  puts "#{BASE_FOLDER}/wysihtml5x-toolbar.min.js"
  `cp #{BASE_FOLDER}/bootstrap3-wysihtml5.min.js vendor/assets/javascripts/bootstrap-wysihtml5/bootstrap3-wysihtml5.min.js`
  `cp #{BASE_FOLDER}/wysihtml5x-toolbar.min.js vendor/assets/javascripts/bootstrap-wysihtml5/wysihtml5x-toolbar.min.js`
end

def copy_css
  `cp #{BASE_FOLDER}/bootstrap3-wysihtml5-editor.min.css vendor/assets/stylesheets/bootstrap-wysihtml5/bootstrap3-wysihtml5-editor.min.css`
  `cp #{BASE_FOLDER}/bootstrap3-wysihtml5.min.css vendor/assets/stylesheets/bootstrap-wysihtml5/bootstrap3-wysihtml5.min.css`
end

desc "Update assets"
task 'update' do
  # if Dir.exist?('bootstrap-wysihtml5')
  #   system("bower update bootstrap3-wysihtml5-bower")
  # else
  #   system("bower install bootstrap3-wysihtml5-bower")
  # end
  #
  copy_javascript
  copy_css
end

desc "Build"
task "build" do
  system("gem build bootstrap-wysihtml5-rails.gemspec")
end

desc "Publish a new version"
task :publish => :build do
  tags = `git tag`.split
  version = BootstrapWysihtml5Rails::Rails::VERSION
  system("git tag -a #{version} -m 'Release #{version}' ") unless tags.include?(version)
  system("gem push bootstrap-wysihtml5-rails-#{version}.gem")
  system("git push --follow-tags")
end
