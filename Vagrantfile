Vagrant.configure("2") do |config|
  
  # consul
  (1..3).each do |i|
    config.vm.define vm_name="consul#{i}" do |node|
      node.vm.box = "apopa/bionic64"
      node.vm.hostname = vm_name
      node.vm.network "public_network", ip: "192.168.178.#{50+i}", bridge: "en7: Dell Universal Dock D6000"
      node.vm.provision "shell", path: "https://raw.githubusercontent.com/andrewpopa/bash-provisioning/main/consul/latest.sh"
    end
  end

  # prometheus / grafana / node_exporter
  config.vm.define vm_name="grafana" do |node|
    node.vm.box = "apopa/bionic64"
    node.vm.hostname = vm_name
    node.vm.network "public_network", ip: "192.168.178.55", bridge: "en7: Dell Universal Dock D6000"
    node.vm.provision "shell", path: "https://raw.githubusercontent.com/andrewpopa/bash-provisioning/main/consul/latest_client.sh"
    node.vm.provision "shell", env: { "NODE_VERSION" => "1.0.1" }, path: "https://raw.githubusercontent.com/andrewpopa/bash-provisioning/main/prometheus/node.sh"
    node.vm.provision "shell", env: { "PROMETHEUS_VERSION" => "2.24.0" }, path: "https://raw.githubusercontent.com/andrewpopa/bash-provisioning/main/prometheus/prometheus.sh"
    node.vm.provision "shell", path: "https://raw.githubusercontent.com/andrewpopa/bash-provisioning/main/grafana/grafana.sh"
  end
end
