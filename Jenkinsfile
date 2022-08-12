pipeline {
    agent any

    stages {
        stage('SCM') {
            steps {
                git 'https://github.com/saikumarsagar/JavaCalculator.git'
            }
        }

    stage('Junit testing by MVN and build') {
            steps {
             sh 'mvn clean package'
              junit 'target/surefire-reports/*.xml'
            }
        } 
    stage('docker build') {
            steps {
             sh 'sudo docker build -t saidocker2048/java_calculator:2.0 .'
            }
        }
     stage('Pushing code to docker hub') {
            steps {
            withCredentials([string(credentialsId: '6636d3c5-1154-4ac0-8d3d-5f5649a671b7', variable: 'dockerpwd')])
            {
            sh "sudo docker login -u saidocker2048 -p ${dockerpwd}"
            sh 'sudo docker push saidocker2048/java_calculator:2.0'
            }
            }
        }     
    }
}
