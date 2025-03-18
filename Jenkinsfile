pipeline {
    agent any

    environment {
        GIT_URL = 'https://github.com/reporaff/calculadora.git'
        BRANCH = 'main'  // Asegúrate de que sea la rama correcta
        PYTHON_VERSION = '3.8'  // Cambia según la versión de Python que necesites
    }

    stages {
        stage('Clonar código') {
            steps {
                script {
                    checkout([$class: 'GitSCM',
                        branches: [[name: env.BRANCH]],
                        userRemoteConfigs: [[url: env.GIT_URL, credentialsId: '9c6a12a6-bde9-4195-9b16-8f48171a1353']]
                    ])
                }
            }
        }

        stage('Instalar dependencias') {
            steps {
                script {
                    sh 'python -m venv venv'
                    sh '. venv/bin/activate && pip install -r requirements.txt'
                }
            }
        }

        stage('Ejecutar pruebas') {
            steps {
                script {
                    sh '. venv/bin/activate && pytest'
                }
            }
        }

        stage('Desplegar') {
            when {
                branch 'main'  // Solo se ejecuta en la rama principal
            }
            steps {
                echo 'Desplegando aplicación...'
                // Aquí puedes agregar comandos de despliegue (Docker, Kubernetes, etc.)
            }
        }
    }

    post {
        always {
            echo 'Pipeline finalizada.'
        }
        failure {
            echo '❌ Error en la ejecución de la pipeline.'
        }
        success {
            echo '✅ Ejecución exitosa.'
        }
    }
}
