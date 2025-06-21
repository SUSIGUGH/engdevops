pipeline{
    agent any
    stages{
        
        stage('Start Docker if stopped'){
            steps{
            sh 'ssh ec2-user@13.201.117.157 "sudo systemctl is-active --quiet docker || sudo systemctl start docker"'
            sh 'ssh ec2-user@13.201.117.157 "sudo systemctl status docker"'
            }
        }
        
        stage('Send Dockerfile and crdb.sql to docker server'){
            steps{
                sh 'scp Dockerfile ec2-user@13.201.117.157:/home/ec2-user/'
                sh 'scp crdb.sql ec2-user@13.201.117.157:/home/ec2-user/'
            }
        }
        
        stage('Create Docker Image'){
            steps{
               sh 'ssh ec2-user@13.201.117.157 "sudo docker build -t mysql-jenkins ."' 
            }
        }
        
        stage('Tag the image'){
            steps{
                sh 'ssh ec2-user@13.201.117.157 "sudo docker image tag mysql-jenkins 6esusigugh/mysql-jenkins:v1"'
		sh 'ls -ltr'
            }
        }
        
         stage('Send image to docker hub'){
            steps{
                sh 'ssh ec2-user@13.201.117.157 "sudo docker login -u "susigugh" -p "Joomla#5647" && sudo docker push 6esusigugh/mysql-jenkins:v1"'
                sh 'ls -ltr'
            }
        } 
    }
}
