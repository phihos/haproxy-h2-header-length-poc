# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "base"

  config.vm.define "hp-nginx" do |c|
    c.vm.box = "ubuntu/focal64"
    c.vm.network "forwarded_port", guest: 8080, host: 8080
    c.vm.network "forwarded_port", guest: 80, host: 8081
    c.vm.network "forwarded_port", guest: 81, host: 8082

    c.vm.provision "file", source: "haproxy.cfg", destination: "/tmp/haproxy.cfg"
    c.vm.provision "file", source: "nginx_default_site", destination: "/tmp/nginx_default_site"
    c.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y --no-install-recommends software-properties-common
      add-apt-repository -y ppa:vbernat/haproxy-2.6
      apt-get install -y haproxy=2.6.\* nginx
      mv /tmp/haproxy.cfg /etc/haproxy/haproxy.cfg
      chown haproxy:haproxy /etc/haproxy/haproxy.cfg
      systemctl restart haproxy
      mv /tmp/nginx_default_site /etc/nginx/sites-available/default
      systemctl restart nginx
    SHELL
  end

  config.vm.provision "shell", inline: <<-SHELL

  SHELL
end
