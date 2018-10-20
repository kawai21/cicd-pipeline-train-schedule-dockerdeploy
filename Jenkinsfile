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
        stage('Build Docker Image')
        when {
            branch 'master'
        }
        steps {
            script {
                app = docker.build("kawai21/train-schedle3")
                app.inside {
                    sh 'echo $(curl localhost:8080)'
                }
            }
        }
    }
}
