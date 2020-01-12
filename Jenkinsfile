pipeline{
    agent any
    options {
        timestamps()
    }
    environment {
        IMAGE='rsxyz123/hello-docker-java'
        DOCKERHUB='DockerHub'
    }
    stages{
        stage('prep') {
            steps {
                script {
                    env.GIT_HASH = sh(
                        returnStdout: true, 
                        script: 'git rev-parse HEAD'
                        ).trim().take(7)
                    env.BUILD_TAG="${env.BUILD_ID}-${env.GIT_HASH}"
                }
            }
        }     
        stage("java build"){
            steps{
                sh "mvn clean package"
            }
        }
        stage("docker build"){
            steps{
                 
               script {
                    dockerImage=docker.build("${IMAGE}")
                    dockerImage.tag("${env.BUILD_TAG}")
                    println "Newly generated image, " + dockerImage.id
                }
            }
        }
        stage('Deploy Image') {
            steps{
                 script {
                     withDockerRegistry([ credentialsId: "${DOCKERHUB}", url: "" ]) {
                       dockerImage.push()
                     }
                }
            }
        }
        stage('Remove Unused docker image') {
            steps{
                sh "docker rmi $IMAGE:$BUILD_TAG"
            }
        }
    }
}
