pipeline {
    agent any
    
    stages {
        stage('GIT') {
            steps {
                git branch: 'main', url: 'https://github.com/medhbib07/med-hbib-twin8.git'
            }
        }

        stage('Compile Stage') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }
        
        stage('SonarQube Analysis') {
            environment {
                SONAR_SCANNER_OPTS = "-Xmx1024m"
            }
            steps {
                withSonarQubeEnv('MySonar') {  
                    sh """
                        mvn sonar:sonar \
                        -Dsonar.projectKey=med-hbib-twin8 \
                        -Dsonar.host.url=http://localhost:9000 \
                        -Dsonar.login=$SONAR_AUTH_TOKEN
                    """
                }
            }
        }

        stage('Build image') {
            steps {
                sh 'docker build -t hbibworld/med-hbib-twin8:latest .'
            }
        }

        stage('Login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-hbibworld',
                    passwordVariable: 'DOCKER_PASSWORD',
                    usernameVariable: 'DOCKER_USERNAME')]) {
                    sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
                }
            }
        }

        stage('Push image') {
            steps {
                sh 'docker push hbibworld/med-hbib-twin8:latest'
            }
        }
    }
}
