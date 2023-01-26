def secret_token = load_secret_token(params.ENVIRONMENT)

properties([parameters([
  choice(name: 'ENVIRONMENT', choices: ['dev', 'sta', 'pre'], description: 'Select the environment')
])])

pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                withCredentials([string(credentialsId: 'jenkins_secret_token_' + params.ENVIRONMENT, variable: 'SECRET_TOKEN')]) {
                    echo "The SECRET_TOKEN for the environment ${params.ENVIRONMENT} is: ${SECRET_TOKEN}"
                }
            }
        }
    }
}

def load_secret_token(environment) {
    switch (environment) {
        case 'dev':
            return 'jenkins_secret_token_dev'
        case 'sta':
            return 'jenkins_secret_token_sta'
        case 'pre':
            return 'jenkins_secret_token_pre'
        default:
            return 'undefined_secret_token'
    }
}

