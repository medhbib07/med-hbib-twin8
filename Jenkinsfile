pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: ='https://github.com/medhbib07/med-hbib-twin8.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn compile'
            }
        }
    }
}