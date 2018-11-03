Vagrant.configure("2") do |config|
   config.vm.box = "centos/7"
   config.ssh.forward_agent = true
   config.ssh.insert_key = false
   config.vm.provider :virtualbox do |v|
     v.memory = 512
    v.cpus = 1
    end
   
#Define two VMs with static private IP addresses.
     VMs = [
      { :name => "server1", :ip => "10.2.0.10" },
      { :name => "server2", :ip => "10.3.0.11" },
      { :name => "server3", :ip => "10.4.0.12" },
			]     
VMs.each do |opts|
   config.vm.define opts[:name] do |config|
   config.vm.hostname = opts[:name]
   config.vm.network :private_network, ip: opts[:ip]
   config.vm.network :public_network, bridge: "eno1", use_dhcp_assigned_default_route: true 
   config.vm.network :forwarded_port, guest: 80, host: 8089
   config.vm.provision  "ansible" do |ansible|
   ansible.playbook = "haproxy.yml"
   ansible.inventory_path = "hosts"     
   ansible.verbose = "v"
    ansible.limit = "all"    
 
 end
 end
 end
 end
