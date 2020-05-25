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
                withCredentials([[$class: 'VaultTokenCredentialBinding', credentialsId: 'jenkins-vault-token', vaultAddr: 'http://172.17.0.2:8200']]) {
                    sh '''
                        set +x
                        export VALUE=$(echo $(./vault kv get --format=json secret/hello | python -c "import sys, json; print json.load(sys.stdin)['data']['data']['foo']")
                        echo "id: ${VALUE}"
                    '''
                }
            }
        }
    }
}