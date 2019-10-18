# -*- mode: ruby -*-
# vi: set ft=ruby :

DIR = File.dirname(__FILE__)

require "yaml"

$env_config = YAML.load_file(File.join(DIR, "env.yml"))

Vagrant.configure("2") do |config|
  config.vm.box = $env_config["box"]

  $env_config["instances"].each do |instance|
    instance_name = instance["name"]
    config.vm.define instance_name do |instance_config|

      # instance is the yaml configuration hash for the node
      # instance_config is the Vagrant configuration for the instance

      instance_config.vm.hostname = instance_name
      instance_config.vm.network :private_network, ip: instance["box_ip"]

      # set up the provider for the instance
      instance_config.vm.provider "virtualbox" do |v|
        v.customize ["modifyvm", :id, "--memory", instance["memory"]]
        v.customize ["modifyvm", :id, "--cpus", instance["cpu"]]
        v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      end
    end
  end
end
