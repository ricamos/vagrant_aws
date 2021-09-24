# -*- mode: ruby -*-
# vi: set ft=ruby :

class Hash
  def slice(*keep_keys)
    h = {}
    keep_keys.each { |key| h[key] = fetch(key) if has_key?(key) }
    h
  end unless Hash.method_defined?(:slice)
  def except(*less_keys)
    slice(*keys - less_keys)
  end unless Hash.method_defined?(:except)
end

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
