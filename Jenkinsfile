pipeline {
    agent {
        kubernetes(k8sagent(name: 'maven:3-jdk-8'))
    }
    
    stages {
        stage('Build') {
            steps {
               sh 'mvn -B -DskipTests clean package'
               archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
}
