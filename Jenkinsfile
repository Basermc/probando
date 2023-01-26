def secret_token = load_secret_token(params.ENVIRONMENT)

properties([parameters([
  choice(name: 'ENVIRONMENT', choices: ['dev', 'sta', 'pre'], description: 'Select the environment')
])])

pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo "The SECRET_TOKEN for the environment ${params.ENVIRONMENT} is: ${secret_token}"
                sh "echo $secret_token"
            }
        }
    }
}

def load_secret_token(environment) {
    switch (environment) {
        case 'dev':
            return 'jenkins_secret_token_dev'
        case 'sta':
            return 'sta_secret_token'
        case 'pre':
            return 'pre_secret_token'
        default:
            return 'undefined_secret_token'
    }
}

