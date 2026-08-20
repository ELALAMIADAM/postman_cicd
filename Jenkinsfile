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
        stage('Vérifier les fichiers') {
            steps {
                sh 'echo "Fichiers dans le workspace:"'
                sh 'ls -la *.json || echo "Aucun fichier JSON trouvé"'
            }
        }

        stage('Lancer les tests') {
            steps {
                script {
                    def testResults = []
                    
                    if (params.Toolshop) {
                        echo "Exécution de Toolshop..."
                        sh 'newman run Toolshop.json -e preprod.json --reporters cli'
                        testResults.add('Toolshop: PASSED')
                    }

                    if (params.instagram) {
                        echo "Exécution de instagram..."
                        sh 'newman run instagram.json -e preprod.json --reporters cli'
                        testResults.add('instagram: PASSED')
                    }

                    if (params.Social) {
                        echo "Exécution de Social..."
                        sh 'newman run Social.json -e preprod.json --reporters cli'
                        testResults.add('Social: PASSED')
                    }

                    // Afficher le résumé
                    echo "=== RÉSUMÉ DES TESTS ==="
                    testResults.each { result ->
                        echo result
                    }
                }
            }
        }
    }

    post {
        always {
            echo "Pipeline terminé"
        }
        failure {
            echo "Des tests ont échoué"
        }
        success {
            echo "Tous les tests ont réussi !"
        }
    }
}