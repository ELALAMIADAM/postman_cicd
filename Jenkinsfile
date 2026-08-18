pipeline {
    agent {
        docker {
            image 'postman/newman' 
            args '--entrypoint='
        }
    } 

    stages {
        stage('Lancement de test') {
            steps{
                sh 'newman run instagram.json -e preprod.json'
            }
        }
    }
}
