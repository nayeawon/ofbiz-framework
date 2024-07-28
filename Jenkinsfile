pipeline {

  agent any

  stages {
    stage('project-clone'){
        git (
            branch: "master“,
            credentialsId: "${codeCommitCredentialsId}",
            url: "https://git-codecommit.ap-northeast-2.amazonaws.com/v1/repos/demo"
        )
    }

    stage('project-build') {
      agent {
        label 'master'
      }
      steps {
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
