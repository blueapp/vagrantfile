VAGRANTFILE_API_VERSION = "2"

# コメントを追加
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "centos6.5"

  # 利用するboxのurl
  # 該当boxがなければ、ここで指定したboxが自動でDLされる
  config.vm.box_url = "https://github.com/2creatives/vagrant-centos/releases/download/v6.5.3/centos65-x86_64-20140116.box"

  # localhostの8080番にアクセスすると仮想マシンの80番ポートにポートフォワード
  #config.vm.network :forwarded_port, guest: 80, host: 8080

  # ホストマシンからのみ参照できるようにプライベート化
  config.vm.network :private_network , ip: "192.168.50.4"

  # ホストの ../proj-repo を ゲストの /var/www/として共有フォルダ化
  # ここでのホスト側のパスは、Vagrantfileからの相対
  # config.vm.synced_folder "../proj-repo", "/var/www/"

  # VirtualBoxの設定
  config.vm.provider :virtualbox do |vb|
    # VMに割り当てるメモリ量
    #vb.customize ["modifyvm", :id, "--memory", "4096"]

    # VMに割り当てるCPUのコア数
    #vb.customize ["modifyvm", :id, "--cpus", "4"]

    # やたらネットワークが遅い現象の対策 (ipv6絡み)
    # see https://github.com/mitchellh/vagrant/issues/1172
    #vb.customize ["modifyvm", :id, "--natdnsproxy1", "off"]
    #vb.customize ["modifyvm", :id, "--natdnshostresolver1", "off"]
  end

  #chef関連
  config.omnibus.chef_version = :latest
  config.vm.provision :chef_solo do |chef|
      #chef.log_level = "debug"

      # 一般的に、cookbooksには第三者が公開しているクックブック、
      # site-cookbooksには自分で作成したクックブックを入れる
      chef.cookbooks_path = ["./chef-repo/site-cookbooks"]

      # レシピ
      chef.add_recipe "gen_base"
  end
end
