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
            credentialsId: '797ce515-f9f8-4c25-a35b-cea16242feed',
            projectName: 'nyw-mod-cb',
            region: 'ap-northeast-1',
            sourceControlType: 'jenkins',
            sseAlgorithm: 'AES256'
        )
      }
    }
  }
}
