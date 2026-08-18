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
            defaultValue: false,
            description: 'Lancer la collection instagram.json'
        )
    }

    stages {

        stage('Lancer les tests') {
            steps {
                script {

                    if (params.Toolshop) {
                        sh 'newman run Toolshop.json'
                    }

                    if (params.Product) {
                        sh 'newman run instagram.json -e preprod.json'
                    }

                }
            }
        }
    }
}
