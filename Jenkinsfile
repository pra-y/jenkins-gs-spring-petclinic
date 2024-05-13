pipeline {
  agent any
  
  stages {
    
    stage("checkout") {
      steps {
        git branch: 'main', url: 'https://github.com/pra-y/jenkins-gs-spring-petclinic.git'
      }
    }
    
    stage("build") {
      steps {
        sh "./mvnw package"
      }
    }
    
    stage("capture") {
      steps {
        archiveArtifacts '**/target/*jar'
        jacoco()
        junit '**/target/surefire-reports/TEST*.xml'
      }
    }
  }
  post {
    always {
      emailext body: '${env.BUILD_URL}\n${CurrentBuild.absoluteUrl}', 
        to: 'always@foo.bar',
        recipientProviders: [previous()], 
        subject: "${currentBuild.currentResult}: Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]"
    }
  }
}
