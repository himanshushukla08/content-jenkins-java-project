pipeline {
  agent none

  stages {
    stage ('Unit Tests') {
      agent {
        label 'apache'
      }
      steps{
        sh 'ant -f test.xml -v'
      }
    }
    stage ('build') {
      agent {
        label 'apache'
      }
      steps{
        sh 'ant -f build.xml -v'
        junit 'reports/result.xml'
      }
    }
    stage('Deploy'){
      agent {
        label 'apache'
      }
      steps{
        sh "cp dist/rectangle_${env.BUILD_NUMBER}.jar /var/www/html/rectangles/all/"
      }
    }
    stage('Running on centOS'){
      agent {
        label 'CentOS'
      }
      steps {
        sh "wget http://54.173.130.65/rectangles/all/rectangle_${env.BUILD_NUMBER}.jar"
        sh "java -jar rectangle_${env.BUILD_NUMBER}.jar 3 4"
      }
    }
  }
	post {
    agent {
      label 'apache'
    }
		always {
			archiveArtifacts artifacts:'dist/*.jar', fingerprint:true
			}
		}
}
	
