pipeline {
    agent any

    stages {
        stage('Clonar código') {
            steps {
                git 'https://github.com/reporaff/calculadora.git'
            }
        }
        
        stage('Ejecutar pruebas') {
            steps {
                sh 'python -m unittest test_calculator.py'
            }
        }
    }

    post {
        success {
            echo 'Pipeline ejecutado correctamente'
        }
        failure {
            echo 'Error en la ejecución de la pipeline'
        }
    }
}
