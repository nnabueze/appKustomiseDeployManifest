pipeline{
    agent{
        label "master"
    }
    stages{
        stage("Update Image Tag"){
            steps{
                if(params.DOCKERTAG != null){
                    echo "======== Updating image tag in dev ========"

                    withCredentials([usernamePassword(credentialsId: 'jenkins-app', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USER')]) {
                        // some block
                        sh "git config user.email villa@gmail.com"
                        sh "git config user.name villa"
                        sh "cat dev/deployment.yaml"
                        sh "sed -i 's+villavelle101/maths.*+villavelle101/maths:${params.DOCKERTAG}+g' dev/deployment.yaml"
                        sh "cat dev/deployment.yaml"
                        sh "git add ."
                        sh "git commit -am 'Triggered Build: ${env.BUILD_NUMBER}'"
                        sh 'git push https://${GIT_USER}:${GIT_PASSWORD}@github.com/${GIT_USER}/testAppTemplate.git HEAD:master'
                    }
                }
            }
        }

        stage("Update Prod Image Tag"){
            when {
                branch 'prod'
            }
            
            steps{
                echo "======== Updating image tag in prod ========"

                withCredentials([usernamePassword(credentialsId: 'jenkins-app', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USER')]) {
                    // some block
                    sh "git config user.email villa@gmail.com"
                    sh "git config user.name villa"
                    sh "cat dev/deployment.yaml"
                    sh "sed -i 's+villavelle101/maths.*+villavelle101/maths:${params.DOCKERTAG}+g' dev/deployment.yaml"
                    sh "cat dev/deployment.yaml"
                    sh "git add ."
                    sh "git commit -am 'Triggered Build: ${env.BUILD_NUMBER}'"
                    sh 'git push https://${GIT_USER}:${GIT_PASSWORD}@github.com/${GIT_USER}/testAppTemplate.git HEAD:master'
                }
            }

                
        }
    }
}