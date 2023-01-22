Vagrant.require_version ">= 1.8.0"
Vagrant.configure('2') do | config |
    config.vm.define 'angularpage' do |angularpage|
        angularpage.vm.box = 'Ubuntu-Vagrant'
        angularpage.vm.hostname = 'base.lab'
        angularpage.vm.provider 'virtualbox' do |vb|
            vb.customize ['modifyvm', :id, '--memory', '1024']
        end
	angularpage.vm.network "private_network", ip: "192.168.99.101"
        angularpage.vm.network "forwarded_port", guest: 80, host: 8080
    end
    config.vm.define 'ans' do |ans|
        ans.vm.box = 'Ubuntu-Vagrant'
        ans.vm.hostname = 'base.lab'
        ans.vm.provider 'virtualbox' do |vb|
            vb.customize ['modifyvm', :id, '--memory', '1024']
        end
	ans.vm.network "private_network", ip: "192.168.99.100"
	ans.vm.provision "shell",
	    inline: "sudo apt-add-repository ppa:ansible/ansible"
	ans.vm.provision "shell",
	    inline: "sudo apt-get update"
	ans.vm.provision "shell",
	    inline: "yes Y | sudo apt-get install ansible"
	ans.vm.provision "shell",
	    inline: "echo 'angularpage ansible_host=192.168.99.101 ansible_user=vagrant ansible_pass=root' >> /etc/ansible/hosts"
	ans.vm.provision "shell",
	    inline: "ssh-keyscan 192.168.99.101 >> ~/.ssh/known_hosts"
	ans.vm.provision "file", source: "C:/KarpukhinCoursework/playbook.yml", destination: "playbooks/playbook.yml"
	ans.vm.provision "shell",
	    inline: "ansible-playbook playbooks/playbook.yml -l angularpage -u vagrant"
    end  
end