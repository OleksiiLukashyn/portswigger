// Jenkinsfile (Declarative Pipeline) for integration of Dastardly, from Burp Suite.

pipeline {
    agent any
    stages {
        stage ("Docker Pull Dastardly from Burp Suite container image") {
            steps {
                bat 'docker pull public.ecr.aws/portswigger/dastardly:latest'
            }
        }
        stage ("Docker run Dastardly from Burp Suite Scan") {
            steps {
                cleanWs()
                bat '''
                    docker run --user $(id -u) -v 'D:/DockerFiles':'D:/DockerFiles':rw \
                    -e DASTARDLY_TARGET_URL=https://ginandjuice.shop/ \
                    -e DASTARDLY_OUTPUT_FILE='D:/DockerFiles/dastardly-report.xml' \
                    public.ecr.aws/portswigger/dastardly:latest
                '''
            }
        }
    }
    post {
        always {
            junit testResults: 'dastardly-report.xml', skipPublishingChecks: true
        }
    }
}
