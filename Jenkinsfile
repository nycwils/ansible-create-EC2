node('master') {
    def app



    stage("Clone repository") {
        checkout scm
        }



    stage("Run Ancible Playbook") {

        
            withCredentials([file(credentialsId: '92045f3a-fdb3-491e-ad2e-d6b9fe7aa3e5', variable: 'mySecretKey')]){
            //sh "ssh ec2-user@3.93.218.251 -i \$mySecretKey -o 'StrictHostKeyChecking=no' 'ls; pwd; pwd; cd /var/www/html; pwd; ls; ansible-playbook playbook-wilson-test-ansible.yaml -i inventory.txt; 'StrictHostKeyChecking=no';'"
            //sh "ssh ec2-user@54.175.182.142 -i \$mySecretKey -o 'StrictHostKeyChecking=no' 'ls; pwd; pwd; '"
            //sleep(240)


            sh "pwd"
            sh "pwd"
            sh "ls"
            //sh "rm Wilson-Test-EC2KeyPair.pem"
            sh "chmod -R 777 /var/lib/jenkins/workspace/wilson-test-create-ec22"
            sh "cp \$mySecretKey /var/lib/jenkins/workspace/wilson-test-create-ec22"
            sh "ls"
            //sh "chmod 0400 Wilson-Test-EC2KeyPair.pem"
            sh "chmod 0400 Wilson-Test-EC2KeyPair.pem"
            sh "python --version"
            sh "pip --version"
            sh "pip install --user boto"
            sh "pip install --user boto3"
            
            //sh "pip install boto"
            //sh "pip install boto3"
            //sh "pip install boto3 --ignore-installed ${six}"
            //sh "vi ~/.boto"

            //sh "ansible-playbook playbook2.yaml -vvv -i inventory2.txt"
            //sleep(300)
            sh "ansible-playbook playbook-ansible-create-ec2.yaml -i inventory.txt"

            //here is where i get the ip and session file name and fix it up, and put it in inventory file
            
            //sh "touch inventory2.txt"


            //save the instance id
            //sh "var1=\$(find . -name 'i-*') && var11=\${var1:2} && varSession=\${var11::-4} && echo \$varSession" 
            
            //copying to below
            //sh "var1=\$(find . -name 'i-*') && var11=\${var1:2} && varSession=\${var11::-4} && echo \$varSession > instanceid.txt" 
            
            //save the ip address
            sh "var2=\$(find . -name [0-9]*) && var22=\${var2:2} && varIP=\${var22::-4} && echo \$varIP && echo \$varIP > inventory2.txt"
            sh "sed -i '1s/^/target2 ansible_host=ec2-user@/' inventory2.txt"
            sh "sed -i '\$ s/\$/ ansible_ssh_private_key_file=\\/var\\/lib\\/jenkins\\/workspace\\/wilson-test-create-ec22\\/Wilson-Test-EC2KeyPair.pem/' inventory2.txt"

            //sleep(240)
            //sh "ssh ec2-user@3.93.218.251 -i \$mySecretKey -o 'StrictHostKeyChecking=no' 'ls; pwd; pwd; cd /var/www/html; pwd; ls; ansible-playbook playbook-wilson-test-ansible.yaml -i inventory.txt; 'StrictHostKeyChecking=no';'"

            //connect to playbook 2 here to launch ec2 instance and install stuffs
            // sed -i '$ s/$/ ansible_ssh_common_args='-o StrictHostKeyChecking=no' /' inventory.txt
            
            sh "sed -i \"\$ s/\$/ public_file=\\/var\\/lib\\/jenkins\\/workspace\\/test-project\\ ansible_ssh_common_args='-o StrictHostKeyChecking=no'/\" inventory2.txt"
            sh "ansible-playbook playbook2.yaml -vvv -i inventory2.txt"

            //playbook 3 run
            sh "ansible-playbook playbook3.yaml -vvv -i inventory.txt"
            sh "> instanceid.txt"
            sh "var1=\$(find . -name 'i-*') && var11=\${var1:2} && varSession=\${var11::-4} && echo \$varSession > instanceid.txt" 
            sh "rm inventory2.txt"
            //sh "git checkout master; git update; git commit instanceid.txt; git add .; git push origin master; "
            // sh "git push https://nycwils:alksdjfa;lskdjfa;sldjk@github.com/nycwils/ansible-create-EC2.git"


        }
            //sh "sed -i '\$ s/\$/ public_file=\\/var\\/lib\\/jenkins\\/workspace\\/test-project\\ ansible_ssh_common_args='-o StrictHostKeyChecking=no'  /' inventory2.txt"
          
        }

       stage('update github with new isntance id') {
       git branch: 'master', credentialsId: 'wilson-github', url: 'https://github.com/nycwils/ansible-create-EC2.git'
       
            sh "git fetch --all;"
            sh "ls"
            sh" git add instanceid.txt;"
            sh" git commit instanceid.txt -m 'aa';"

                   withCredentials([usernamePassword(credentialsId: 'wilson-github', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh" git push https://$USERNAME:$PASSWORD@github.com/nycwils/ansible-create-EC2.git;"

                    }
   }
       
    //sed -i '$ s/$/ ansible_ssh_private_key_file=\/var\/lib\/jenkins\/workspace\/wilson-test-create-ec2\/Wilson-Test-EC2KeyPair.pem/' inventory2.txt
    //sed -i '$ s/$/ Wilson-Test-EC2KeyPair.pem ansible_ssh_common_args='"'"'-o StrictHostKeyChecking=no'"'"'  /'"'" inventory.txt
  


  
    stage("Wipe Out Jenkins Temp Workspace") {

      deleteDir()
       
    }

}