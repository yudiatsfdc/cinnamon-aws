# encoding: utf-8
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"    
  config.ssh.forward_agent = true

  config.vm.provider :aws do |aws, override|
    override.vm.box = "dummy"                               # overrides virtuabox config to use empty box as will load ami below...
    override.vm.box_url = "https://github.com/mitchellh/vagrant-aws/raw/master/dummy.box"
    aws.access_key_id = ENV['AWS_ACCESS_KEY_ID']            # Export as an env var or replace this with yours   
    aws.secret_access_key = ENV['AWS_SECRET_ACCESS_KEY']    # Export as an env var or replace this with yours  
    aws.keypair_name = 'webdriver'                          # the name of the keypair instance should use
    aws.ami = 'ami-aa941e9a'                                # ubuntu 12.04 64bit precise instance backed
    aws.region = 'us-west-2'                                # overriding default aws region
    override.ssh.username = 'ubuntu'                        # username override from default of vagrant
    override.ssh.private_key_path = ENV['AWS_PEM_FILEPATH'] # path to my amazon pem file
    aws.security_groups = ['webdriver']                     # name of the security group i have preconfigured in AWS with port 22 and 4444 open
    
    # below are the tags to help me easily identify these guys in the console
    aws.tags = {
      'Name' => 'vagrant-webdriver',
      'webdriver' => 'true'
    }
  end

  # tells vagrant to run the setup.sh when the shell is available
  config.vm.provision :shell, :path => "setup.sh"
  # tells vagrant to make the VM port 4444 accessible on host port 4444 (only works for VirtuaBox provider)
  config.vm.network :forwarded_port, guest:4444, host:4444

end
