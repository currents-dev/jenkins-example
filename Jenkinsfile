pipeline {
  agent {
    docker {
      image 'cypress/base:14'
    }
  }

  stages {
    stage('build') {
      steps {
        echo "Running build ${env.BUILD_ID} on ${env.JENKINS_URL}"
        sh 'npm ci'
      }
    }

    

    
    stage('cypress parallel tests') {
      environment {
        CURRENTS_RECORD_KEY = credentials('currents-record-key')
        CYPRESS_trashAssetsBeforeRuns = 'false'
      }

      // https://jenkins.io/doc/book/pipeline/syntax/#parallel
      parallel {
        // start several nodes in parallel
        stage('node A') {
          steps {
            echo "Running build ${env.BUILD_ID}"
            // sh "npm run e2e:record:parallel"
          }
        }

        // second tester runs the same command
        stage('node B') {
          steps {
            echo "Running build ${env.BUILD_ID}"
            // sh "npm run e2e:record:parallel"
          }
        }
      }

    }
  }
}
