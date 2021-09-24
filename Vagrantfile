# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "dummy"
  config.vm.provider :aws do |aws, override|
    aws.access_key_id = "AKIASIX4VFN7ZA45UZOB"
    aws.secret_access_key = "IdevldVEJG/2uFmtujunplOFJ2/HzcgSstdzPLVx"

    aws.ami = "ami-02e2a5679226e293c"

    override.ssh.username = "admin"
    override.ssh.private_key_path = "~/.vagrant.d/insecure_private_key"
  end
end
