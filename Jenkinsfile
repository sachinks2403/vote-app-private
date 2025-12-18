pipeline{
    agent {label 'worker'}
    stages{
	
		stage("Parallel Tests") {
            parallel{
                stage("Unit Tests") {
                    agent { label 'windows' }
                    steps {
                            sh "echo Running Unit Tests"
							sh "sleep 180"
                }
            }
                stage("Integration Tests") {
                    agent { label 'linux' }
                    steps {
                            sh "echo Running Integration Tests"
							sh "sleep 180"
                }
            }

        }
    }

        stage("Docker image build and push"){
            steps{
                sh "docker login -u sachinaws90 -p Suja2403@"
                sh '''
                 cd vote
                 docker build -t sachinaws90/vote:v${BUILD_NUMBER} .
                 '''
                sh "docker push sachinaws90/vote:v${BUILD_NUMBER}"
            }
        }
                stage("deploy"){
            agent {label 'worker'}
            steps{ sh "echo starting deployment"
            }
        }
    }
    
}
