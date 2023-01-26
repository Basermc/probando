def secret_token = load_secret_token(params.ENVIRONMENT)
def proyect

properties([parameters([
  choice(name: 'ENVIRONMENT', choices: ['dev', 'sta', 'pre'], description: 'Select the environment'),
  choice(name: 'PROJECT_TYPE', choices: ['local', 'global'], description: 'Select the project')
])])

pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
              script {
                if (params.PROJECT_TYPE == 'local') {
                    proyect = "sgt-onehrlocal"
                }else if (params.PROJECT_TYPE == 'global') {
                    proyect = "sgt-onehr"
                }
              }
                withCredentials([string(credentialsId: proyect + '_secret_token_' + params.ENVIRONMENT, variable: 'SECRET_TOKEN')]) {
                    echo "The SECRET_TOKEN for the project ${project_name} and environment ${params.ENVIRONMENT} is: ${SECRET_TOKEN}"
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

