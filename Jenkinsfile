pipeline {
    agent any

    stages {
        stage('Clonando Repositório Git') {
            steps {
                git branch: 'main', url: 'https://github.com/RAFHAELJ/jk-public-gh.git'
            }
        }
    
        stage('Contruindo imagem') {
            steps {
                sh 'docker build -t webapp:${BUILD_NUMBER} .'
            }
        }
    
        stage('Implantando imagem') {
            steps {
                sh '''
                   docker ps -a --filter "name=webapp_ctr" --format "{{.Names}}" | grep -q "webapp_ctr" && docker stop webapp_ctr || true
                   docker run --rm -d -p 3000:3000 --name webapp_ctr webapp:${BUILD_NUMBER}
                   '''
            }
        }
    }
}
