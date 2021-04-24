pipeline {
    agent any

    tools {
        maven 'maven-3.6.3'
        jdk 'jdk-8'
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
        stage('Deploy') {
            steps {
                echo '> Deploying the application ...'
                ansiblePlaybook(
                    credentialsId: 'dev1',
                    inventory: 'hosts.ini',
                    playbook: 'playbook-install.yaml',
                    disableHostKeyChecking: true
                )
            }
        }
    }
}
