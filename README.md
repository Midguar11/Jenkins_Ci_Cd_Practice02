# Setup Complie Job

- Start new job " Free Style "
- Configure, Source Code Managment " Select git "
- paste:" https://github.com/Midguar11/Jenkins_Ci_Cd_Practice02.git "
- Branch Specifier (blank for 'any' ) type here: " */main "
- Build select " Invoke top-level Maven targets "
- Select maven version
- Goals " Complie "
- Save
- Test: Build now
- Fine it is green

# Setup Review Job

- Start new job " Free Style "
- Configure, Source Code Managment " Select git "
- paste:" https://github.com/Midguar11/Jenkins_Ci_Cd_Practice02.git "
- Branch Specifier (blank for 'any' ) type here: " */main "
- Build select " Invoke top-level Maven targets "
- Select maven version
- Goals " -P matrix pmd:pmd "
- Save
- Test: Build now
- Fine it is green
- Post-build Actions " Publish HTML reports " 

# Setup Test Job

- Start new job " Free Style "
- Configure, Source Code Managment " Select git "
- paste:" https://github.com/Midguar11/Jenkins_Ci_Cd_Practice02.git "
- Branch Specifier (blank for 'any' ) type here: " */main "
- Build select " Invoke top-level Maven targets "
- Select maven version
- Goals " -P matrix pmd:pmd "
- Save
- Test: Build now
- Fine it is green
- Post-build Actions " Publish HTML reports " 

# New view

- Plugins install Build Pipeline
- Add new view
- upstream / downstream config
- Select inital job: Complie job
- No of displayed Builds " 5 "
- ok 

# Setup Triggers

- Configure Review Job
- Build Triggers " Build after other projects are build 
- Type " Complie job "
- Trigger even if the build fails

- Configure Test Job
- Build Triggers " Build after other projects are build 
- Type " Review Job "
- Trigger even if the build fails

# Test Pipeline

- change to pipeline view and click run

# Install Docker on Jenkins server

- If Docker hasen't been installed on on jenkins server, do it now

        sudo apt-get install ca-certificates
        sudo apt-get install curl
        sudo apt-get install gnupg
        sudo apt-get install lsb-release
        sudo mkdir -p /etc/apt/keyrings
        curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
        
        echo \  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

        sudo apt-get update
        sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
        sudo service docker start
        systemctl status docker
        sudo docker run hello-world
        docker images

# Prepare Image

    sudo docker pull centos
    sudo docker run -it centos
    exit
    clear

# Install Docker Compose on Jenkins server

    sudo apt-get install python3-pip
    sudo pip install docker-compose

# Expand virutal Machine Storage

- Go ESXI expand VM storage 
- Reboot
- Connect to Jenkins server with SSH
- change user to root

        sudo su -
        fdisk -l
        fdisk /dev/sda

- here delete "d" sda3 " n "new partition and adds max. " w" write. Delete can't lost data only label.

- cheking pv label and copy

        pv
        sudo lvextend -r -l +100%FREE /dev/mapper/ubuntu--vg-ubuntu--lv
        df -h
- Reboot

# Nginx in container use the Docker-Compose

    mkdir nginx
    cd nginx
    sudo nano docker-compose.yml

- writing in docker-compose.yml

        sudo docker-compose -f docker-compose.yml up -d
        docker images

- Continue next git repo:

https://github.com/Midguar11/Jenkins_Ci_Cd_Practice02_dockerrepo.git