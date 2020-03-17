pipeline {
    agent {
        docker {
            image 'qaninja/rubywd'
        }
    }
    
    stages {
        stage('Build') {
            steps {
                echo 'Iniciando estagio de build, compilando ou resolvendo dependências'
                sh 'rm -f Gemfile.lock'
                sh 'bundle install'
            }
        }
        stage('Test') {
            steps {
                echo 'Executando testes de regreção'
                sh 'bundle exec cucumber -p ci'
            }
            post {
                always {
                    cucumber failedFeaturesNumber: -1, failedScenariosNumber: -1, failedStepsNumber: -1, fileIncludePattern: '**/*.json', jsonReportDirectory: 'logs', pendingStepsNumber: -1, skippedStepsNumber: -1, sortingMethod: 'ALPHABETICAL', undefinedStepsNumber: -1
                }
            }
        }
        stage('UAT') {
            steps {
                echo 'Aguardando aceitação do usuário'
                input(message: 'Pode ir para produção?', ok: 'Yes')
            }
        }
        stage('Producion') {
            steps {
                echo 'Subindo para produção :)'
            }
        }
    }
}