node {
    stage('Clone repository') {     
        checkout scm
    }

    stage('Update GIT') {
        script {
		    // 앞선 단계에서 설정한 github credential 값으로 변수 설정
            withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                sh "git config user.email cmlee@zenithn.com"
                sh "git config user.name cmlee"
                sh "cat deployment.yaml"
                sh "sed -i 's+webinarzenacr.azurecr.io/petclinic.*+webinarzenacr.azurecr.io/petclinic:${IMAGETAG}+g' deployment.yaml"
                sh "cat deployment.yaml"
                sh "git add ."
                sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/webinar1220-argocd.git HEAD:main"
            }                
        }
    }
}
