pipeline {
    agent {
        docker {
            image 'postman/newman:latest'
            args '-u root --entrypoint=/bin/sh'
        }
    }

    parameters {
        booleanParam(name:'ALLURE', defaultValue: false, description: 'generation de rapport allure')
    }
    tools {
        allure 'allure'
    }

    stages {
        stage('install deps'){
                    steps{
                        sh 'npm ci || true'
                    }
                }
        stage('clean allure results'){
                    
                    steps{
                        sh '''
                            echo "Suppression du cache Allure..."
                            rm -rf allure-results
                            mkdir -p allure-results
                            echo "Dossier allure-results nettoyé avec succès"
                        '''
                    }
                }

        stage('Lancer les tests') {
            steps {
                script {
                    sh 'mkdir -p allure-results'
                    if(params.ALLURE){
                        sh 'newman run instagram.json -e preprod.json -r allure'
                        stash name: 'allure-results', includes: 'allure-results/*'
                    }

                    else{
                        sh 'newman run instagram.json -e preprod.json'
                        }
                    }

                }
            }
        }
    post{
        always{
            script{
                if(params.ALLURE){
                    unstash 'allure-results'
                    archiveArtifacts 'allure-results/*'
                    allure includeProperties: false,
                           jdk: '',
                           results: [[path: 'allure-results/']]
                }
            }
        }
    }
    }
    


