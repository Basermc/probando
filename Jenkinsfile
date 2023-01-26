def project = ['project1']

pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    env.ENVIRONMENT = input message: 'Select the environment', parameters: [choice(name: 'ENVIRONMENT', choices: ['local', 'global'], description: 'Select the environment')]
                    
                    // load the secret token for the project
                    env.SECRET_TOKEN = load_secret_token(project)
                    
                    sh "echo $SECRET_TOKEN"
                }
            }
        }
    }
}

def load_secret_token(project) {
    switch (project) {
        case 'project1':
            return 'project1_secret_token'
        case 'project2':
            return 'project2_secret_token'
        case 'project3':
            return 'project3_secret_token'
        default:
            return 'undefined_secret_token'
    }
}
