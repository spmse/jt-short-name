pipeline {
    agent any
    stages {
        stage('Prepare') {
          steps {
              sh 'rm -rf artifacts/'
              sh 'mkdir -p artifacts'
              sh 'echo "preparation done" > artifacts/done.txt'
              sh 'ls artifacts'
          }
        }
        stage('Build') {
            steps {
                sh 'echo "In Build stage" > artifacts/test-stage.txt'
            }
        }
        stage('Test') {
            steps {
                sh 'echo "In Test Stage" > artifacts/test-stage.txt'
            }
        }
        stage('Deliver for development') {
            when {
                branch 'development' 
            }
            steps {
                sh 'echo "On Development branch" > artifacts/branch-dev.txt'
            }
        }
        stage('archive main-state') {
            when {
                branch 'main'  
            }
            steps {
                sh ('ls artifacts')
                sh ('tar -czf artifacts/artifacts.tar.gz artifacts/*')
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: 'artifacts/*', fingerprint: true
        }
    }
}
