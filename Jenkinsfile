pipeline {
    agent any
    
    tools {
        // Node.js kurulumunu belirt
        nodejs "nodejs"
    }
    
    stages {
        stage('Build') {
            steps {
                // Node.js ile ilgili işlemleri buraya ekle
                sh 'npm install'
                sh 'npm run build'
            }
        }
    }
}