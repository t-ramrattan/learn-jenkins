// jenkins hello world
pipeline {
    agent { label 'master' }
    stages {
        stage('build') {
            steps {
                MSG='Hello World!'
                echo $MSG
            }
        }
    }
}