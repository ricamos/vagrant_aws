# -*- mode: ruby -*-
# vi: set ft=ruby :

# Chamando modulo YAML
require 'yaml'

aws = YAML.load_file('files/secret.yml')
aws_secret = aws['configs'][aws['configs']['use']]

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
    aws.access_key_id = aws_secret['AWSAccessKeyId']
    aws.secret_access_key = aws_secret['AWSSecretKey']
    aws.region = "sa-east-1"
    aws.availability_zone = "sa-east-1a"
    aws.instance_type = "t2.micro"
    aws.ami = "ami-02e2a5679226e293c"
    aws.keypair_name = "vagrant"
    override.ssh.username = "admin"
    override.ssh.private_key_path = "~/.vagrant.d/insecure_private_key"
  end
end
