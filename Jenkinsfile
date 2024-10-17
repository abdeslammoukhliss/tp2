pipeline{
    agent any

    stages{
        stage("Cloning"){
            steps {
              git branch: 'main', url: 'https://github.com/abdeslammoukhliss/tp2.git'

            }
        }
           stage('Build') {
            steps {
                script {
                    // Construire l'image Docker sans cache
                    sh 'docker build --no-cache -t abdomokh/tp2:latest .'
                }
            }
        }
         stage('Login to Docker Hub') {
            steps {
                script {
                    // Utiliser les identifiants de Docker Hub
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        // Se connecter à Docker Hub
                        sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
                    }
                }
            }
        }
          stage('test Container') {
                    steps {
                        script {
                            // Arrêter et supprimer un conteneur existant
                            sh 'echo "test"'
                        }
                    }
                }

        stage('Push Image') {
            steps {
                script {
                    // Pousser l'image sur Docker Hub
                    sh 'docker push abdomokh/tp2:latest'
                }
            }
        }
        stage('Run Container') {
            steps {
                script {
                    // Arrêter et supprimer un conteneur existant
                    sh 'docker stop my_nginx || true'
                    sh 'docker rm my_nginx || true'

                    // Lancer un nouveau conteneur
                    sh 'docker run -p 80:80 -d --name my_nginx abdomokh/tp2:latest'
                }
            }
        }
    }



}