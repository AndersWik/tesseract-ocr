# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
    # The most common configuration options are documented and commented below.
    # For a complete reference, please see the online documentation at
    # https://docs.vagrantup.com.
  
    # Every Vagrant development environment requires a box. You can search for
    # boxes at https://vagrantcloud.com/search.
    config.vm.box = "debian/bookworm64"
  
    # Disable automatic box update checking. If you disable this, then
    # boxes will only be checked for updates when the user runs
    # `vagrant box outdated`. This is not recommended.
    # config.vm.box_check_update = false
  
    # Create a forwarded port mapping which allows access to a specific port
    # within the machine from a port on the host machine. In the example below,
    # accessing "localhost:8080" will access port 80 on the guest machine.
    # NOTE: This will enable public access to the opened port
    # config.vm.network "forwarded_port", guest: 80, host: 8080
  
    # Create a forwarded port mapping which allows access to a specific port
    # within the machine from a port on the host machine and only allow access
    # via 127.0.0.1 to disable public access
    # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"
  
    # Create a private network, which allows host-only access to the machine
    # using a specific IP.
    config.vm.network "private_network", ip: "192.168.33.37"
    config.vm.network "private_network", type: "dhcp"
    config.vm.hostname = "dev.tesseract.test"
  
    # Create a public network, which generally matched to bridged network.
    # Bridged networks make the machine appear as another physical device on
    # your network.
    # config.vm.network "public_network"
  
    # Share an additional folder to the guest VM. The first argument is
    # the path on the host to the actual folder. The second argument is
    # the path on the guest to mount the folder. And the optional third
    # argument is a set of non-required options.
    config.vm.synced_folder "public_html", "/var/www/public_html/",
      group: "nogroup",
      mount_options: ["dmode=775,fmode=775"]
  
    # Provider-specific configuration so you can fine-tune various
    # backing providers for Vagrant. These expose provider-specific options.
    # Example for VirtualBox:
    #
    config.vm.provider "virtualbox" do |vb|
    #   # Display the VirtualBox GUI when booting the machine
    #   vb.gui = true
    #
    #   # Customize the amount of memory on the VM:
    vb.memory = "4203"
    end
    #
    # View the documentation for the provider you are using for more
    # information on available options.
  
    # Enable provisioning with a shell script. Additional provisioners such as
    # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
    # documentation for more information about their specific syntax and use.
    config.vm.provision "shell", inline: <<-SHELL
  
    # Updating Debian
    sudo apt update
    sudo apt upgrade<<EOF
Y
EOF

  echo "##############################"
  echo "#### Install tesseract-ocr ###"
  echo "##############################"

  sudo apt install tesseract-ocr<<EOF
Y
EOF

  sudo apt install tesseract-ocr-eng<<EOF
Y
EOF

  sudo apt install tesseract-ocr-swe<<EOF
Y
EOF

  sudo tesseract — version

  echo "##############################"
  echo "#### Test tesseract-ocr ######"
  echo "##############################"

  cd /var/www/public_html
  sudo tesseract eurotext.png - -l eng > eurotext.txt

  # The (quick) [brown] {fox} jumps!
  # Over the $43,456.78 <lazy> #90 dog
  # & duck/goose, as 12.5% of E-mail
  # from aspammer@website.com is spam.
  # Der ,.schnelle” braune Fuchs springt
  # tiber den faulen Hund. Le renard brun
  # «rapide» saute par-dessus le chien
  # paresseux. La volpe marrone rapida
  # salta sopra il cane pigro. El zorro
  # marron rapido salta sobre el perro
  # perezoso. A raposa marrom rapida
  # salta sobre 0 cdo preguicoso.

  # For use multiple languages
  # sudo tesseract images/eurotext.png - -l eng+swe

  sudo tesseract eurotext.png - -l eng hocr > eurotext.html

  sudo tesseract 2col.png - --psm 3 > 2col.txt

  # Cautionary Statement

  # ON FORWARD-LOOKING STATEMENTS: This presentation includes
  # information, statements, beliefs and opinions which are forward-looking, and
  # which reflect current estimates, expectations and projections about future
  # events, referred to herein as “forward-looking statements” within the meaning
  # of the U.S> Private Securities Litigation Reform Act of 1995 or “forward-looking
  # information” under applicable securities laws. Statements containing the words
  # “believe’, “expect”, “continue”, “could”, ‘potential’, “predict”, “would”,

  # “intend”, “should”, “seek”, “anticipate”, “will”, “opportunity,” “positioned”,

  # “poised,” ‘project’, “risk”, “plan”, “may’, “estimate” or, in each case, their

  # Historical Information: Historical statements contained in this document
  # regarding past trends or activities should not be taken as a representation that
  # such trends or activities will continue in the future. In this regard, certain
  # financial information contained herein has been extracted from, or based upon,
  # information available in the public domain and/or provided by the Company. In
  # particular, historical results should not be taken as a representation that such
  # trends will be replicated in the future. No statement in this document is
  # intended to be nor may be construed as a profit forecast.

  sudo tesseract toc.png - --psm 6 > toc.txt

  # Contents

  # Introduction to the Tenth Anniversary Edition page xvii
  # Afterword to the Tenth Anniversary Edition xix
  # Preface xxi
  # Acknowledgements xxvii
  # Nomenclature and notation xxix
  # Part I Fundamental concepts 1
  # 1 Introduction and overview 1
  # 1.1 Global perspectives 1

  # 1.1.1 History of quantum computation and quantum
  # information 2
  # 1.1.2 Future directions 2
  # 1.2 Quantum bits 13
  # 1.2.1 Multiple qubits 16
  # 1.3 Quantum computation 7
  # 1.3.1 Single qubit gates 7
  # 1.3.2. Multiple qubit gates 20
  # 1.3.3. Measurements in bases other than the computational basis 2
  # 1.3.4 Quantum circuits 2
  # 1.3.5 Qubit copying circuit? 4
    SHELL
  end
  