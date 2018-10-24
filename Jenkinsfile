pipeline {
  agent any
  stages {
    stage ('Unit Testing') {
      steps{
        sh 'ant -f test.xml -v'
      }
    }
    stage ('build') {
      steps{
        sh 'ant -f build.xml -v'
        junit 'reports/result.xml'
      }
    }
  }

	post {
		always {
			archiveArtifacts artifacts:'dist/*.jar', fingerprint:true
			}
		}
	}

	
