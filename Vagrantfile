# simple lab build of clustered splunk enterprise (6.5.1)
# v.0.1
# bryan oakley-wiggins (brybinary)
# 9.12.16

########
# env #
######
# running selinux on the base CentOS 7 OS (ootb)
# 1x cluster master (inc deployer + license master)
# 3x index cluster peers, 
# 2x heavy forwarders
# 3x search head cluster members (inc captain)


###############################
# future versions to include #
#############################

# using packer to pull down certain OS bulds
# more efficient use of vault
# better use of groups
# dynamic inventory
# ldap endpoints
# tls security with LetsEncrypt certificates
# added modules (restAPI + more)
# vcenter as a provider (using vm template)
# haproxy load balance pool
# universal forwarder client
# multi-site with routing (+ firewall)
# blue-green topology
# container based (kub-pods/photon/lxd/docker/openstack)
# other


VAGRANTFILE_API_VERSION = "2"

# change this value for number of nodes to be built
 NUM_BOXES = 9
 IP_OFFSET = 10

# change ip range to suit
 def ip_from_num(i)
   "10.91.0.#{100+i+IP_OFFSET}"
end

 Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

   (1..NUM_BOXES).each do |i|

     is_main = (i == 1)

# create your own naming convention, cpu and mem count can be added to - currently 1x cpu and 512 mem
     config.vm.define "splunklabnode#{i}".to_sym do |bbin|
       bbin.vm.hostname = "splunklabnode#{i}"
       bbin.vm.box = "centos/7"
       bbin.vm.provider :virtualbox do |vb|
        vb.cpus = 1
       bbin.vm.network "private_network", ip: ip_from_num(i)
       bbin.vm.network "forwarded_port", guest: 8000, host: 49100, auto_correct: true 
      end

# point at your own playbook to suit  
     config.vm.provision "buildcluster", type: "ansible" do |ansible|
       ansible.ask_vault_pass = true
       ansible.playbook = "splunk-live-lab-dev-commit_v.01.yml"
     end
   end
 end
end