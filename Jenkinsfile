pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh './mvnw compile'
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
        expression {${GIT_BRANCH} == 'master'}
      }
                    steps {
                      sh './mvnw deploy'
                    }
    }

  }

}
