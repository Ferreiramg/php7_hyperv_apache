#-------------------------------------------------------------------------
# Copyright (c) Microsoft Open Technologies, Inc.
# All Rights Reserved. Licensed under the Apache 2.0 License.
#--------------------------------------------------------------------------
# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

	config.vm.box = "ericmann/trusty64"
	
	config.vm.network "forwarded_port", guest: 80, host: 8080
	config.vm.network "forwarded_port", guest: 3000, host: 3000
	config.vm.network "public_network"
	
	config.vm.synced_folder "C:/php7", "/var/www", :mount_options => ["file_mode=0777,dir_mode=0777"],
		:type => "smb",
		:smb_username => 'user@windowsys.com',
		:smb_password => 'password'
end