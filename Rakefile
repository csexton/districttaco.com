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

desc "Creates a new _posts file using TITLE='the title' and today's date. JEKYLL_EXT=markdown by default"
task :post do
  ext = ENV['JEKYLL_EXT'] || "markdown"
  unless title = ENV['TITLE']
    puts "USAGE: rake post TITLE='the post title'"
    exit(1)
  end
  post_title = "#{Date.today.to_s}-#{title.downcase.gsub(/[^\w]+/, '-')}"
  post_file = File.dirname(__FILE__) + "/_posts/#{post_title}.#{ext}"
  File.open(post_file, "w") do |f|
    f << <<-EOS.gsub(/^    /, '')
    ---
    layout: post
    title: #{title}
    ---
    
    EOS
  end
  if (ENV['EDITOR'])
    system ("#{ENV['EDITOR']} #{post_file}") 
    system ("git add #{post_file}") 
  end
end

