pipeline {
    agent any
    parameters{
        choice(choices:['Build_all','Build_backend','Build_frontend'], description: 'Build parameter choices', name: 'build')
    }
    stages {
        stage('Checkout'){
            steps {
                sh "git --version"
                sh "docker -v"
                sh "echo Branch name: ${GIT_BRANCH}"
            }
        }
        stage('Build_stage'){
            environment{
                ENV_FILE = credentials("three-tier-env-file")
            }
            parallel{
                stage('Build_backend'){
                    environment {
                        ENV_FILE = credentials("three-tier-env-file")
                    }
                    when{
                        expression{params.build == 'Build_backend' || params.build == 'Build_all'}
                    }
                    steps{
                        sh "docker-compose -f docker-compose.yml build backend"
                    }
                }
                stage('build_frontend'){
                    environment{
                     ENV_FILE = credentials("three-tier-env-file")
                    }
                    when{
                        expression{params.build == 'Build_frontend' || params.build == 'Build_all'}
                    }
                    steps{
                        sh "docker-compose -f docker-compose.yml build frontend"
                    }
                }

            }
        }
        stage("stop Existing Containers"){
            steps{
                sh "docker-compose -f docker-compose.yml down"
            }
        }
        stage("Deploy"){
            environment{
                ENV_FILE = credentials("three-tier-env-file")
            }
            steps{
                sh "docker-compose -f docker-compose.yml up -d"
            }
        }
    }
}