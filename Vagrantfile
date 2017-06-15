Vagrant.require_version ">= 1.9.5"
Vagrant.configure('2') do |config|
  
  config.vm.define ENV['VM_NAME1'] do |web|
    web.vm.box = 'azure'
    web.vm.hostname = 'web'
    web.vm.synced_folder ".", "/vagrant", disabled: true
    # web.vm.provision "shell", inline: "echo WEB"
    web.ssh.private_key_path = '~/.ssh/id_rsa'
    web.vm.provider :azure do |azure, override|    
      azure.tenant_id = ENV['AZURE_TENANT_ID']
      azure.client_id = ENV['AZURE_CLIENT_ID']
      azure.client_secret = ENV['AZURE_CLIENT_SECRET']
      azure.subscription_id = ENV['AZURE_SUBSCRIPTION_ID']
      azure.dns_name = "racidb01web"
      
      azure.vm_image_urn = 'OpenLogic:CentOS:7.2:latest'
      azure.vm_name = ENV['VM_NAME1']
      azure.vm_size = 'Standard_D1_v2'

      azure.resource_group_name = ENV['RG_NAME1']
      azure.location = ENV['LOCATION']
      azure.instance_ready_timeout = 600
      # azure.vm_password = ENV['VM_PASSW']
      azure.admin_username = "raci"
    end
    web.vm.provision "ansible" do |ansible|
      ansible.playbook = "provisioning/site.yml"
      ansible.verbose = 'vv'
    end
  end
end
