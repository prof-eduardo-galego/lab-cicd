pipeline {
    agent any

    tools {
        maven 'maven-3.6.3'
        jdk 'jdk-11'
    }

    stages {
        stage('Build') {
            steps {
               sh 'mvn -B -DskipTests clean package'
               archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }

        stage ('Deploy to DEV using SSH') {
//             when {
//                 branch 'master'
//             }
            sshagent(credentials : ['dev']) {
                sh 'ssh ubuntu:ec2-54-82-245-41.compute-1.amazonaws.com rm -rf ~/*.jar'
                sh 'scp ./target/*.jar ubuntu@ec2-54-82-245-41.compute-1.amazonaws.com:~/app.jar'
                sh 'ssh ubuntu:ec2-54-82-245-41.compute-1.amazonaws.com java -jar ~/app.jar'
            }
        }
    }
}