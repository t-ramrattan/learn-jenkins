// jenkins hello world
pipeline {
    agent { label 'master' }

    environment {
        MSG = 'Hello World!'
    }

    stages {
        stage('build') {
            steps {
                echo ${MSG}
            }
        }
    }
}