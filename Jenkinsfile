pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code from repository'
                checkout scm
            }
        }

        stage('Update Helm Chart') {  
            steps {
                script {
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[credentialsId: 'github-ATOKEN', url: 'git@github.com:tomerschwartz24/mock-app-infra.git', refspec: '+refs/heads/*:refs/remotes/origin/*']]])
                    sh """
                    git checkout main
                    yq eval   '.image.tag = "${env.BUILD_NUMBER}"' -i counter-app-helm/values.yaml
                    git add counter-app-helm/values.yaml
                    git commit counter-app-helm/values.yaml -m " Updated counter-app Helm chart image tag to \${BUILD_NUMBER} "
                    git pull --rebase
                    git push --set-upstream origin main
                       """
                }
            }
        }
    }
}
