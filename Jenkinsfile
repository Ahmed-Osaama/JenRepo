pipeline {
    agent any

    stages {
        stage('Code') {
            steps {
                echo 'hello from coding'
             git branch: 'main', credentialsId: 'gitUser', url: 'https://github.com/Ahmed-Osaama/JenRepo.git'
            }
            
        }
          stage('Build') {
            steps {
                echo '=====Building====='
                sh 'docker build -t my-app:$BUILD_NUMBER . '
                sh 'docker images'
            }
            
        }
         stage('Test') {
            steps {
                echo '=====Testing====='

            }
            
        }
        stage('Release') {
            steps {
             withCredentials([usernamePassword(credentialsId: 'Docker', passwordVariable: 'DOCKER_PASS', usernameVariable: 'DOCKER_USER')]) {
   
                   sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                   sh 'docker tag my-app:$BUILD_NUMBER ahmedosaama/my-app:$BUILD_NUMBER '
                    sh 'docker push ahmedosaama/my-app:$BUILD_NUMBER'
                   
}
               }
             
            }
            
        }
    }

