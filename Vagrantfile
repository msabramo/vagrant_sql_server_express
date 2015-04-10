# -*- mode: ruby -*-
# vi: set ft=ruby :

$script = <<'SCRIPT'
# You can add PowerShell stuff here if you want...
echo "Executing script in Vagrantfile..."
# choco install -y cyg-get
# git clone ...
SCRIPT

Vagrant.configure(2) do |config|
  config.vm.box = "msabramo/mssqlserver2014express"
  config.vm.provision "shell", inline: $script
end
