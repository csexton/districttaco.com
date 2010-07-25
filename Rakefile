task :default => :server

desc 'Build site with Jekyll'
task :build do
  jekyll
end

desc 'Start server with --auto'
task :server do
  jekyll('--server --auto')
end

namespace :prod do
  desc 'Build and deploy'
  task :deploy => :build do
    sh 'rsync -rtzh --progress --delete _site/ districttaco.com:districttaco.com/'
  end
end
namespace :dev do
  desc 'Build and deploy'
  task :deploy => :build do
    sh 'rsync -rtzh --progress --delete _site/ districttaco.com:dev.districttaco.com/'
  end
end

def jekyll(opts = '')
  sh 'rm -rf _site'
  sh 'jekyll ' + opts
end

