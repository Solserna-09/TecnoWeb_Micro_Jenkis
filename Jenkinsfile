pipeline {
    agent any

    stages {
        stage('Clonar el Repositorio'){
            steps {
                git branch: 'main', url: 'https://github.com/Solserna-09/TecnoWeb_Micro_Jenkis.git'
            }
        }
 
        stage('Desplegar contenedores Docker'){
            steps {
                script {
                    withCredentials([
                            string(credentialsId: 'MONGO_URI', variable: 'MONGO_URI')
                    ]) {
                        sh 'docker-compose up -d'
                    }
                }
            }
        }
    }

    post {
        always {
            emailext (
                subject: "Status del build: ${currentBuild.currentResult}",
                body: "Se ha completado el build. Puede detallar en: ${env.BUILD_URL}",
                to: "sol.serna@est.iudigital.edu.co",
                from: "jenkins@iudigital.edu.co"
            )
        }
    }
}
