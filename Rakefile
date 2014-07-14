
task :default => [:all]

desc "config and build RubyLive"
task :all => [:config, :build]

desc "config RubyLive"
task :config => [:clean] do
  sh 'lb config'
  if ENV['APT_HTTP_PROXY']
    sh "lb config --apt-http-proxy #{ENV['APT_HTTP_PROXY']}"
  end
end

desc "build RubyLive"
task :build => "resources:check" do
  sh 'sudo lb build'
end

desc "clean generated files"
task :clean do
  sh 'sudo lb clean'
end

desc "distclean generated files"
task :distclean => [:clean] do
  sh 'sudo lb clean --purge'
  sh 'sudo rm -f *.iso *.img *.list *.packages *.buildlog *.md5sum'
end

namespace :resources do
  require "yaml"

  desc "check resources from external"
  task :check => :fetch do
    require "digest/sha2"
    YAML.load_file("resources.yml").each do |resource|
      path = resource["path"]
      unless File.file?(path) and
          File.size(path) == resource["size"] and
          Digest::SHA256.file(path).hexdigest == resource["sha256sum"]
        warn "resource mismatched - check it out"
        warn resource.to_yaml
        abort
      end
    end
  end

  desc "fetch resources from external"
  task :fetch do
    require "open-uri"
    YAML.load_file("resources.yml").each do |resource|
      path = resource["path"]
      next if File.file?(path)
      mkdir_p File.dirname(path)
      File.open(path, "wb") do |file|
        puts "fetching #{resource["url"]}"
        file.write(open(resource["url"], &:read))
      end
    end
  end
end

# old tasks
namespace :chroot do
  desc 'install hosts, resolv and proc, do "chroot chroot" as root'
  task :install do
    sh 'sudo lb chroot_hosts  install'
    sh 'sudo lb chroot_resolv install'
    sh 'sudo "chroot chroot" as root'
    puts 'chroot install.'
  end
  desc 'remove hosts, resolv and proc'
  task :remove do
    sh 'sudo lb chroot_hosts  remove'
    sh 'sudo lb chroot_resolv remove'
    puts 'chroot remove.'
  end
end

