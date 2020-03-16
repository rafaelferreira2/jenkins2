pipeline{
    agent {
        docker {
            image 'ruby'
        }
    }
    
    stages{
        stage('Build'){
            steps{
                echo 'Iniciando estagio de build, compilando ou resolvendo dependências'
                sh 'bundle install'
            }
        }
        stage('Test'){
            steps{
                echo 'Executando testes de regreção'
                sh 'bundle exec cucumber -p ci'
            }
        }
        stage('UAT'){
            steps{
                echo 'Aguardando aceitação do usuário'
                input(message: 'Pode ir para produção?', ok: 'Yes')
            }
        }
        stage('Producion'){
            steps{
                echo 'Subindo para produção :)'
            }
        }
    }
}