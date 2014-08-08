# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = '2'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
	config.vm.box = 'puphpet/debian75-x64'

	# Add you network card for the bridge or vagrant ask you every start
	config.vm.network 'public_network'

	# If true, then any SSH connections made will enable agent forwarding.
	# Default value: false
	config.ssh.forward_agent = true

	# Share an additional folder to the guest VM.
	# Sync local folders in VM and ignore git folders.
	config.vm.synced_folder 'data/ext/', '/var/www/typo3conf/ext/', type: 'rsync', rsync__auto: true, id: 'fluidTYPO3'

	config.vm.provider 'virtualbox' do |vb|
		# Disable headless mode
		# vb.gui = true

		# Use VBoxManage to customize the VM. For example to change memory:
		vb.customize ['modifyvm', :id, '--memory', '2048','--cpus', '2','--ioapic', 'on']
	end

	config.vm.provision :puppet do |puppet|
		puppet.manifests_path = 'puppet/manifests'
		puppet.manifest_file  = 'base.pp'
		puppet.module_path    = 'puppet/modules'
		puppet.options = '--hiera_config /vagrant/hiera.yaml'
		puppet.facter = {
			'document_root' => '/var/www',
			'fqdn' => 'fluidtypo3.dev',
			'typo3_branch' => 'TYPO3_6-2',
			'operatingsystem' => 'Debian',
			'osfamily' => 'Debian',
			'osversion' => 'wheezy',
		}
	end

end