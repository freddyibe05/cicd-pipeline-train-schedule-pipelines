pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                sh './gradlew build --no-daemon'
            }
        }
    }
    
    post {
        always {
            archiveArtifacts artifacts: 'dist/*.zip', allowEmptyArchive: true
            junit 'build/test-results/**/*.xml'
        }
        failure {
            mail to: 'you@example.com',
                 subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
                 body: "Something is wrong with ${env.BUILD_URL}"
        }
    }
}
