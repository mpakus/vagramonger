# encoding: utf-8

Vagrant::Config.run do |config|

  config.vm.box = "projectnamebox"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box" # or from local box image "/Users/mpak/Downloads/precise64.box"
  config.ssh.forward_agent = true
  config.vm.forward_port 3000, 3000   # rails
  config.vm.forward_port 27017, 27017 # mongo
  config.vm.forward_port 9876, 9876   # faye

  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = ["cookbooks"]
    chef.add_recipe :apt
    chef.add_recipe 'mongodb::default'
    chef.add_recipe 'git'
    chef.add_recipe 'nodejs'
    chef.add_recipe 'rvm::vagrant'
    chef.add_recipe 'rvm::system'
    chef.json = {
      :mongodb => {
        :dbpath  => "/var/lib/mongodb",
        :logpath => "/var/log/mongodb",
        :port    => "27017",
        :package_name => "mongodb-10gen-server",
      },
      :git => {
        :prefix => "/usr/local"
      },
      :rvm => {
        'rubies' => ['1.9.3', '2.0.0']
      }
    }
  end
end
