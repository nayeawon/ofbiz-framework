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

    stage('Build with CodeBuild') {
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

    stage('Deploy with CodeDeploy') {
        steps {
            withAWS(credentials: 'codebuild') {
                script {
                    def deployCommand = "aws deploy create-deployment " +
                        "--application-name nyw-mod-cd " +
                        "--deployment-config-name CodeDeployDefault.ECSAllAtOnce " +
                        "--deployment-group-name nyw-mod-cd-dg " +
                        "--s3-location bucket=nyw-mod-s3/nyw-mod-cb/"
                    sh deployCommand
                }
            }
        }
        post {
            success {
                echo 'Deploy with CodeDeploy stage succeeded'
            }
            failure {
                echo 'Deploy with CodeDeploy stage failed'
            }
        }
    }
  }
}
