pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh './mvnw compile'
        catchError(catchInterruptions: true, buildResult: 'Fail', message: 'Failure', stageResult: 'Fail')
      }
    }

    stage('Test') {
      steps {
        sh './mvnw test'
      }
    }

    stage('Package') {
      steps {
        sh './mvnw package'
      }
    }

    stage('Deploy') {
      when {
        expression {
          ${GIT_BRANCH} == 'master'
        }

      }
      steps {
        sh './mvnw deploy'
      }
    }

    stage('Mail result') {
      steps {
        mail(subject: 'Jenkins build ${currentBuild.currentResult}', body: 'Jenkins build has ${currentBuild.currentResult}', from: 'Jenkins <Jenkins@Jenkins>', to: '[$class: \'DevelopersRecipientProvider\']')
      }
    }

  }
}