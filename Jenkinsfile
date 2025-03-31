pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version

                    # Configurer npm pour utiliser un cache local et éviter /var/empty/.npm
                    npm config set cache $(pwd)/.npm-cache --global
                    
                    # Vérifier les permissions des fichiers existants
                    sudo chown -R $(whoami) $(pwd)/.npm-cache || true
                    
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
    }
}
