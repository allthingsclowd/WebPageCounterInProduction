Vagrant.configure("2") do |config|

    #global mountpount for our code
    config.vm.synced_folder ".", "/usr/local/bootstrap"

    config.vm.define "redis01" do |redis01|
        redis01.vm.box = "cbednarski/ubuntu-1604"
        redis01.vm.hostname = ENV['REDIS_MASTER_NAME']
        redis01.vm.network "private_network", ip: ENV['REDIS_MASTER_IP']
        redis01.vm.provision :shell, path: "redis_base.sh"
        redis01.vm.provision "file", source: "master.redis.conf", destination: "master.redis.conf"
        redis01.vm.provision :shell, path: "redis_master.sh"
    end
    
    config.vm.define "redis02" do |redis02|
        redis02.vm.box = "cbednarski/ubuntu-1604"
        redis02.vm.hostname = ENV['REDIS_SLAVE_NAME']
        redis02.vm.network "private_network", ip: ENV['REDIS_SLAVE_IP']
        redis02.vm.provision :shell, path: "redis_base.sh"
        redis02.vm.provision "file", source: "slave.redis.conf", destination: "slave.redis.conf"
        redis02.vm.provision :shell, path: "redis_slave.sh"
    end
    
    config.vm.define "godev01" do |devsvr|
        devsvr.vm.box = "cbednarski/ubuntu-1604"
        devsvr.vm.network "private_network", ip: ENV['GO_DEV_IP']
        devsvr.vm.hostname = ENV['GO_DEV_NAME']
        devsvr.vm.network "forwarded_port", guest: ENV['GO_GUEST_PORT'], host: ENV['GO_HOST_PORT']
        devsvr.vm.provision "shell", path: "go_init.sh"
        devsvr.vm.provision "shell", path: "go_vagrant_user.sh"
    end

    config.vm.define "web01" do |web01|
        web01.vm.box = "cbednarski/ubuntu-1604"
        web01.vm.hostname = ENV['NGINX_NAME']
        web01.vm.network "private_network", ip: ENV['NGINX_IP']
        web01.vm.network "forwarded_port", guest: ENV['NGINX_GUEST_PORT'], host: ENV['NGINX_HOST_PORT']
        web01.vm.provision "file", source: "nginx.conf", destination: "nginx.conf"
        web01.vm.provision :shell, path: "webserver_install.sh"
   end

end