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
                withCredentials([string(credentialsId: 'jenkins-vault', variable: 'ROLE_ID'),string(credentialsId: 'jenkins-vault-token', variable: 'VAULT_TOKEN')]) {
                    sh '''
                        set +x
                        export VAULT_ADDR=http://172.17.0.2:8200
                        export SECRET_ID=$(./vault write -field=secret_id -f auth/approle/role/jenkins/secret-id)
                        export VAULT_TOKEN=$(./vault write -field=token auth/approle/login role_id=${ROLE_ID} secret_id=${SECRET_ID})
                        echo ${VAULT_TOKEN}
                        '''
                }
            }
        }
    }
}