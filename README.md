# Vagrant e Amazon Web Service (AWS).

## Sumário:

1. [Motivação](#motivacao)
2. [Descrição de arquivos](#file)
3. [Interação com o projeto](#interact)
4. [Autor e referências](#autor)
5. [Base de conhecimento](#ack)

## Motivação <a name="motivacao"></a>
O vagrant é uma ferramenta que possibilita a criação, configuração, destruição e reconstrução de ambientes de desenvolvimento e testes de infraestrutura. Geralmente utilizado em conjunto com softwares de virtualização, como virtual box, VMware e KVM. Porém com a necessidade de criar ambientes mais complexos e com consumo de poder computacional alto o computador hospedeiro pode não ser capaz de fornecer a configuração necessaria para rodar o ambiente. Para resolver este problema podemos investir em um computador mais potente ou de forma imediata em uma plataforma de serviços de computação em nuvem como a Amazon Web Service (AWS). 

## Descrição de arquivos <a name="file"></a>
Vagrantfile - Descrição, configuração e provisionamento do ambiente.

## Interação com o projeto <a name="interact"></a>

### Preparação do ambiente

```
$ vagrant plugin install vagrant-aws

$ vagrant box add dummy https://github.com/mitchellh/vagrant-aws/raw/master/dummy.box
```

### Variaveis da AWS

#### [Gerenciar chaves de acesso](https://docs.aws.amazon.com/pt_br/IAM/latest/UserGuide/id_credentials_access-keys.html#Using_CreateAccessKey)

```
aws.access_key_id = "YOUR KEY"
aws.secret_access_key = "YOUR SECRET KEY"
```
Estas duas variaveis são preenchidas com chaves obtidas no [console do IAM](https://console.aws.amazon.com/iam) de sua conta AWS e devem ser mantidas em segredo. Crie um usuário com permissão de "AmazonEC2FullAccess" e crie as chaves de acesso.

#### [Amazon Machine Images (AMI)](https://docs.aws.amazon.com/pt_br/AWSEC2/latest/UserGuide/AMIs.html)
```
aws.ami = "ami-02e2a5679226e293c"

```
Uma Imagem de máquina da Amazon (AMI) é um codigo que faz referência a uma imagem de um Sistema operacional da AWS.

#### Username e private Key ssh
```
override.ssh.username = "username"

```
São necessarias para conexão SSH com a instância criada.

O Username deve seguir a tabela abaixo:

| Sistema Operacional |	  SSH user          |
| ------------------- | ------------------- |
| Amazon Linux 	  	  |  Amazon Linux       |
| Ubuntu              |  Ubuntu             |
| Debian			  |  Admin              |
| RHEL 6.4 and later  |	 ec2-user           |
| RHEL 6.3 and earlier|  root               |
| Fedora              |  fedora             |
| CentOS			  |  centos             |
| Suse                |  root               |

#### [Pares de chaves do Amazon EC2](https://docs.aws.amazon.com/pt_br/AWSEC2/latest/UserGuide/ec2-key-pairs.html)
```
override.ssh.private_key_path = "PATH TO YOUR PRIVATE KEY"
```
A private deve ser configurada para funcionar junto ao vagrant. Para isso podemos fazer o seguinte:
```
$ openssl rsa -in ~/.vagrant.d/insecure_private_key -pubout > vagrant.pub
```

Ao invés de [criar um par de chaves usando o Amazon EC2](https://docs.aws.amazon.com/pt_br/AWSEC2/latest/UserGuide/ec2-key-pairs.html#having-ec2-create-your-key-pair) nós vamos usar a chave armazenada em vagrant.pub

[Abra o console do Amazon EC2]( https://console.aws.amazon.com/ec2/) em Redes e segurança selecione pares de chaves. Em ações selecione importar pares de chaves e cole o conteúdo do arquivo vagrant.pub criado anteriormente. Em nosso exemplo nomeamos esta chave no console AWS como vagrant.

```
aws.keypair_name = "vagrant"
``` 
Esta configuração diz respeito ao nome da chave criada anteriormente no console do Amazon EC2. Como criamos nossa chave com nome de vagrant, configuramos desta maneira.

#### Interação com o ambiente.
```
$ vagrant up --provider=aws #Cria o ambiente 
$ vagrant up --debug --provider=aws #Cria o ambiente em modo debug.
$ vagrant destroy -f #Destrói todo ambiente.
```

## Autor e referências <a name="autor"></a>
Ricardo Coelho

https://github.com/mitchellh/vagrant-aws
http://anzpiper.blogspot.com/2017/08/use-vagrant-to-deploy-to-aws.html

## Base de conhecimento <a name="ack"></a>
Vagrant 

Amazon Web Service 