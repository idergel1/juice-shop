pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Juice Shop build adımı
                sh 'npm install' // Örnek: Gerekli paketleri yükleme
                sh 'npm run build' // Örnek: Uygulama yapısını oluşturma
            }
        }
    }
}