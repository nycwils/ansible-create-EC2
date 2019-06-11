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
            sh "chmod -R 777 /var/lib/jenkins/workspace/wilson-test-EC2-audit-ansible"
            sh "cp \$mySecretKey /var/lib/jenkins/workspace/wilson-test-EC2-audit-ansible"
            sh "ls"
            sh "chmod 0400 Wilson-Test-EC2KeyPair.pem"
            sh "ansible-playbook playbook-ansible-scripts.yaml -i inventory.txt"
        }
            
          
        }
       
    

  
    stage("Wipe Out Jenkins Temp Workspace") {

      deleteDir()
       
    }

}