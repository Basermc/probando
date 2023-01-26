pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    env.ENVIRONMENT = input message: 'Select the environment', parameters: [choice(name: 'ENVIRONMENT', choices: ['dev', 'sta', 'pre'], description: 'Select the environment')]
                    
                    // load the secret token for the environment
                    env.SECRET_TOKEN = load_secret_token(env.ENVIRONMENT)
                }
                echo "The SECRET_TOKEN for the environment ${env.ENVIRONMENT} is: ${env.SECRET_TOKEN}"
                sh "echo $SECRET_TOKEN"
            }
        }
    }
}

def load_secret_token(environment) {
    switch (environment) {
        case 'dev':
            return 'dev_secret_token'
        case 'sta':
            return 'sta_secret_token'
        case 'pre':
            return 'pre_secret_token'
        default:
            return 'undefined_secret_token'
    }
}
