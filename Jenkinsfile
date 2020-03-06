pipeline{
    agent any
        tools{
            maven "Maven3"
        }
        stages{
                stage('get SCM'){
                    steps{
                        git credentialsId: 'GITHUB', url: 'https://github.com/suryathejaambati/spring3-mvc-maven-xml-hello-world.git'
                    }
                }
                stage('Validate Build the Code'){
                    steps{
                        sh "mvn validate"
                    }
                }
                stage ('Compile the code'){
                    steps{
                        sh "mvn compile"
                    }
                }
                stage('Test the code'){
                    steps{
                        sh "mvn test"
                    }
                }
                stage('package the code'){
                    steps{
                        sh "mvn packages"
                    }
                }
                stage('archive the artifactory'){
                    steps{
                        archiveArtifacts 'target/*.war'
                    }
                }
        }
        post {
        failure {
            script {
                currentBuild.result = 'FAILURE'
            }
        }

        always {
            step([$class: 'Mailer',
                notifyEveryUnstableBuild: true,
                recipients: "ybmadhuit@gmail.com,ybmadhu404@gmail.com",
                sendToIndividuals: true])
        }
    }
}
