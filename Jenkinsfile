pipeline {
    agent {
        docker {
            image 'postman/newman:latest'
            args '-u root --entrypoint='
        }
    }

    parameters {

        booleanParam(
            name: 'Toolshop',
            defaultValue: true,
            description: 'Lancer la collection Toolshop.json'
        )

        booleanParam(
            name: 'instagram',
            defaultValue: true,
            description: 'Lancer la collection instagram.json'
        )
        booleanParam(
            name: 'Social',
            defaultValue: true,
            description: 'Lancer la collection Social.json'
        )
    }

    stages {
        // stage("installation des dependances"){
        //     steps {
        //         script {
                    
        //             sh 'npm install -g newman-reporter-allure'
                    
        //             sh 'npm install -g allure-commandline'
        //         }
        //     }
        // }

        stage('Lancer les tests') {
            steps {
                script {
                    sh 'mkdir -p allure-results'

                    if (params.Toolshop) {
                        sh 'newman run Toolshop.json -e preprod.json'
                    }

                    if (params.instagram) {
                        sh 'newman run instagram.json -e preprod.json'
                    }

                    if (params.Social) {
                        sh 'newman run Social.json -e preprod.json'
                    }

                }
            }
        }

    }
    

}

