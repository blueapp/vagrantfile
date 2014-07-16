VAGRANTFILE_API_VERSION = "2"

# �R�����g��ǉ�
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "centos6.5"

  # ���p����box��url
  # �Y��box���Ȃ���΁A�����Ŏw�肵��box��������DL�����
  config.vm.box_url = "https://github.com/2creatives/vagrant-centos/releases/download/v6.5.3/centos65-x86_64-20140116.box"

  # localhost��8080�ԂɃA�N�Z�X����Ɖ��z�}�V����80�ԃ|�[�g�Ƀ|�[�g�t�H���[�h
  #config.vm.network :forwarded_port, guest: 80, host: 8080

  # �z�X�g�}�V������̂ݎQ�Ƃł���悤�Ƀv���C�x�[�g��
  config.vm.network :private_network , ip: "192.168.50.4"

  # �z�X�g�� ../proj-repo �� �Q�X�g�� /var/www/�Ƃ��ċ��L�t�H���_��
  # �����ł̃z�X�g���̃p�X�́AVagrantfile����̑���
  # config.vm.synced_folder "../proj-repo", "/var/www/"

  # VirtualBox�̐ݒ�
  config.vm.provider :virtualbox do |vb|
    # VM�Ɋ��蓖�Ă郁������
    #vb.customize ["modifyvm", :id, "--memory", "4096"]

    # VM�Ɋ��蓖�Ă�CPU�̃R�A��
    #vb.customize ["modifyvm", :id, "--cpus", "4"]

    # �₽��l�b�g���[�N���x�����ۂ̑΍� (ipv6����)
    # see https://github.com/mitchellh/vagrant/issues/1172
    #vb.customize ["modifyvm", :id, "--natdnsproxy1", "off"]
    #vb.customize ["modifyvm", :id, "--natdnshostresolver1", "off"]
  end

  #chef�֘A
  config.omnibus.chef_version = :latest
  config.vm.provision :chef_solo do |chef|
      #chef.log_level = "debug"

      # ��ʓI�ɁAcookbooks�ɂ͑�O�҂����J���Ă���N�b�N�u�b�N�A
      # site-cookbooks�ɂ͎����ō쐬�����N�b�N�u�b�N������
      chef.cookbooks_path = ["./chef-repo/site-cookbooks"]

      # ���V�s
      chef.add_recipe "gen_base"
  end
end
