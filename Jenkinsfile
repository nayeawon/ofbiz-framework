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
        awsCodeBuild(
            credentialsType: 'jenkins',
            credentialsId: 'codebuild',
            projectName: 'nyw-mod-cb',
            region: 'ap-northeast-1',
            sourceControlType: 'jenkins',
            sseAlgorithm: 'AES256'
        )
      }
    }
  }
}
