pipeline{
    agent any
    environment {
        KEY = credentials('Muthur')
    }
    stages{
        stage('docker-build'){
            steps{
                dir('codebase') {
                    script{
                        def imagename = "muthuinc/webapp:latest"
                        def dockerimage = docker.build("${imagename}", ".")
                    }
                }
            }
        }

        stage('docker-push'){
            steps{
                script{
                    def appname = "muthuinc/webapp:latest"
                    withDockerRegistry(credentialsId: 'dockerid') {
                        docker.image(appname).push()
                    }
                }
            }
        }

        stage('deploy'){
            steps{
                dir('ansible'){
                    sh ' ansible-playbook -i inventory --private-key=$KEY deployment.yaml '
                }
            }
        }
    }

    post {
        success {
            sh 'docker rmi muthuinc/webapp:latest '
        }
    }
}