// jenkins hello world
pipeline {
    agent { label 'master' }

    environment {
        MSG = 'Hello World!'
    }

    stages {
        stage('build') {
            steps {
                sh 'curl -o vault.zip https://releases.hashicorp.com/vault/1.4.2/vault_1.4.2_linux_amd64.zip ; yes | unzip vault.zip'
                withCredentials([[$class: 'VaultTokenCredentialBinding', credentialsId: 'jenkins-vault-token', vaultAddr: 'https://172.17.0.2:8200']]) {
                    sh 'RESP=$(./vault kv get -format=json secret/hello)'
                    sh 'echo $RESP'
                }
            }
        }
    }
}