pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Running build automation'
                sh './gradlew build --no-daemon'
                archiveArtifacts artifacts: 'dist/trainSchedule.zip'
            }
        }
        stage('Build Docker Image') {
            when {
                branch 'master'
            }
            steps {
                script {
                    app = docker.build("puneetsekhon1986/train-schedule")
                    app.inside {
                        sh 'echo Image built'
                        sh 'echo $(curl localhost:8080)'
                    }
                }
            }
        }
    }
}
