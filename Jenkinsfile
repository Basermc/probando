pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    env.ENVIRONMENT = input message: 'Select the environment', parameters: [choice(name: 'ENVIRONMENT', choices: ['dev', 'sta', 'pre'], description: 'Select the environment')]
                }
                withCredentials([string(credentialsId: 'jenkins_secret_token_' + env.ENVIRONMENT, variable: 'SECRET_TOKEN')]) {
                    echo "The SECRET_TOKEN for the environment ${env.ENVIRONMENT} is: ${env.SECRET_TOKEN}"
                    sh "echo $SECRET_TOKEN"
                }
            }
        }
    }
}


def load_secret_token(environment) {
    switch (environment) {
        case 'project1':
            return 'dev_secret_token'
        case 'sta':
            return 'sta_secret_token'
        case 'pre':
            return 'pre_secret_token'
        default:
            return 'undefined_secret_token'
    }
}
