pipeline {
    agent any
    
    tools {
        // Node.js kurulumunu belirt
        nodejs "nodejs"
    }
    
    environment {
        PRISMA_API_URL="https://api.eu.prismacloud.io"
    }
    
    stages {
        stage('Build') {
            steps {
                // Node.js ile ilgili işlemleri buraya ekle
                sh 'npm install'
                sh 'npm run postinstall'
            }
        }

        stage('Checkout') {
          steps {
              git branch: 'master', url: 'https://github.com/idergel1/juice-shop.git'
              stash includes: '**/*', name: 'source'
          }
        }
        stage('Checkov') {
            steps {
                withCredentials([string(credentialsId: 'PC_USER', variable: 'c78b7eb1-907c-47e7-bf1d-7f9644ae1521'),string(credentialsId: 'PC_PASSWORD', variable: '991ScVUyvPdZI9AjOVrlI3v7JAc=')]) {
                    script {
                        docker.image('bridgecrew/checkov:latest').inside("--entrypoint=''") {
                          unstash 'source'
                          try {
                              sh 'checkov -d . --use-enforcement-rules -o cli -o junitxml --output-file-path console,results.xml --bc-api-key ${pc_user}::${pc_password} --repo-id  idergel1/juice-shop --branch main'
                              junit skipPublishingChecks: true, testResults: 'results.xml'
                          } catch (err) {
                              junit skipPublishingChecks: true, testResults: 'results.xml'
                              throw err
                          }
                        }
                    }
                }
            }
        }
    }
     options {
        preserveStashes()
        timestamps()
    }
}