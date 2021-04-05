pipeline {
    agent {
        kubernetes {
            yaml """\
                apiVersion: v1
                kind: Pod
                metadata:
                labels:
                    some-label: some-label-value
                spec:
                containers:
                - name: maven
                    image: "maven:alpine"
                    command:
                    - cat
                    tty: true
                - name: busybox
                    image: busybox
                    command:
                    - cat
                    tty: true
            """.stripIndent()
        }
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
