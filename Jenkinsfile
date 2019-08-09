node('master') {
    def app

    stage("Clone repository") {
        checkout scm
        }



    stage("Run Ancible Playbook") {

        
            withCredentials([file(credentialsId: '92045f3a-fdb3-491e-ad2e-d6b9fe7aa3e5', variable: 'mySecretKey')]){
            //sh "ssh ec2-user@3.93.218.251 -i \$mySecretKey -o 'StrictHostKeyChecking=no' 'ls; pwd; pwd; cd /var/www/html; pwd; ls; ansible-playbook playbook-wilson-test-ansible.yaml -i inventory.txt; 'StrictHostKeyChecking=no';'"
            sh "pwd"
            sh "pwd"
            sh "ls"
            //sh "rm Wilson-Test-EC2KeyPair.pem"
            sh "chmod -R 777 /var/lib/jenkins/workspace/wilson-test-create-ec2"
            sh "cp \$mySecretKey /var/lib/jenkins/workspace/wilson-test-create-ec2"
            sh "ls"
            sh "chmod 0400 Wilson-Test-EC2KeyPair.pem"
            sh "python --version"
            sh "pip --version"
            sh "pip install --user boto"
            sh "pip install --user boto3"
            
            //sh "pip install boto"
            //sh "pip install boto3"
            //sh "pip install boto3 --ignore-installed ${six}"
            //sh "vi ~/.boto"
            sh "ansible-playbook playbook-ansible-create-ec2.yaml -vvv -i inventory.txt"

            //here is where i get the ip and session file name and fix it up, and put it in inventory file
            
            sh "touch inventory2.txt"
            sh "var1=\$(find . -name 'i-*') && var11=\${var1:2} && varSession=\${var11::-4} && echo \$varSession" 
            sh "var2=\$(find . -name [0-9]*) && var22=\${var2:2} && varIP=\${var22::-4} && echo \$varIP && echo \$varIP > inventory2.txt"
            sh "sed -i '1s/^/target2 ansible_host=ec2-user@/' inventory2.txt"
            sh "sed -i '\$ s/\$/ ansible_ssh_private_key_file=\\/var\\/lib\\/jenkins\\/workspace\\/wilson-test-create-ec2\\/Wilson-Test-EC2KeyPair.pem/' inventory2.txt"

            //connect to playbook 2 here to launch ec2 instance and install stuffs
            sh "ansible-playbook playbook2.yaml -vvv -i inventory2.txt"
        }
            
          
        }
       
    //sed -i '$ s/$/ ansible_ssh_private_key_file=\/var\/lib\/jenkins\/workspace\/wilson-test-create-ec2\/Wilson-Test-EC2KeyPair.pem/' inventory2.txt


  
    stage("Wipe Out Jenkins Temp Workspace") {

      //deleteDir()
       
    }

}