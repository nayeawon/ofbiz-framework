pipeline {

  agent any

  stages {
    stage('project-clone'){
        steps {
            git (
                branch: "trunk",
                url: "https://github.com/nayeawon/ofbiz-framework"
            )
        }
    }

    stage('project-build') {
      steps {
        withAWS(credentials: 'aws-credentials') {
          awsCodeBuild(
            credentialsType: 'keys',
            projectName: 'nyw-mod-cb',
            region: 'ap-northeast-1',
            sourceControlType: 'jenkins',
            sseAlgorithm: 'AES256'
            // buildspec 위치 없어도 되는지 확인
        )
        }
        
      }
    }
  }
}
