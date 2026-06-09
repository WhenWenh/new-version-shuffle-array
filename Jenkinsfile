pipeline {
    agent any

    tools {
        nodejs 'nodejs'
    }

    stages {
        stage('Build') {
            steps {
                sh 'npm ci'
                sh 'npm run build'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test'
            }
        }

        stage('Publish') {
            steps {
                withCredentials([string(
                    credentialsId: 'jenkins_npm',
                    variable: 'NPM_TOKEN'
                )]) {
                    sh 'echo "//registry.npmjs.org/:_authToken=${NPM_TOKEN}" > .npmrc'
                    sh 'npm publish'
                }
            }
        }
    }

    post {
        always {
            sh 'rm -f .npmrc'
        }
    }
}
