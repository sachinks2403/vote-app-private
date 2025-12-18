pipeline{
    agent {label 'worker'}
    stages{
        stage("Docker image build and push"){
            steps{
                sh "docker login -u sachinaws90 -p Suja2403@"
                sh '''
                 cd vote
                 docker build -t yogesh010/vote:v${BUILD_NUMBER} .
                 '''
                sh "docker push yogesh010/vote:v${BUILD_NUMBER}"
            }
        }
        stage("Parallel Tests") {
            parallel{
                stage("Unit Tests") {
                    agent { label 'windows' }
                    steps {
                            sh "echo Running Unit Tests"
                }
            }
                stage("Integration Tests") {
                    agent { label 'linux' }
                    steps {
                            sh "echo Running Integration Tests"
                }
            }

        }
    }
        stage("deploy"){
            agent {label 'worker'}
            steps{ sh "echo starting deployment"
            }
        }
    }
    
}
