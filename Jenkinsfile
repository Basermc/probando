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
              withCredentials([string(credentialsId: proyect + '-' + params.ENVIRONMENT, variable: 'SECRET_TOKEN')]) {
                    echo "The SECRET_TOKEN for the project ${project_name} and environment ${params.ENVIRONMENT} is: ${SECRET_TOKEN}"
                }
            }
        }
    }
}


