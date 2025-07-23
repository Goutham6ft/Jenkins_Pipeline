pipeline {
  agent any
  stages {
    stage('Build plus testing stage') {
      parallel {
        stage('Build') {
          steps {
            echo 'Build is Completed'
          }
        }

        stage('Test') {
          steps {
            echo 'E2E testing is completed'
            echo "Get the Driver path ${Chromepath}"
          }
        }

        stage('Test log') {
          steps {
            writeFile(file: 'Test_Results_log.txt', text: 'All testcases are passed')
          }
        }

      }
    }

    stage('Deployment plus Archive Artifacts stage') {
      parallel {
        stage('Deployment stage') {
          steps {
            input(message: 'Only If Accept then go for deployment', id: 'ok', cancel: 'Cancel')
            echo 'Deploying our application to Azure Server'
          }
        }

        stage('Archive Artifacts') {
          steps {
            archiveArtifacts 'Test_Results_log.txt'
          }
        }

      }
    }

  }
  environment {
    Chromepath = 'C:\\Job\\Jenkins'
  }
}