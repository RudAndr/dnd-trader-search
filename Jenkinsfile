node {
  stage('Checkout Other Repo') {
      steps {
          dir('new-repo') {
              checkout([$class: 'GitSCM', branches: [[name: '*/master']],
                        userRemoteConfigs: [[url: scm.getUserRemoteConfigs()[0].getUrl()]]])
          }
      }
  }

  stage("Clone the project") {
    git branch: 'main', url: scm.getUserRemoteConfigs()[0].getUrl()
  }

  stage("Compilation") {
    sh "./mvnw clean install -DskipTests"
  }

  stage("Tests and Deployment") {
    stage("Runing unit tests") {
      sh "./mvnw test -Punit"
    }
    stage("Deployment") {
      sh 'nohup ./mvnw spring-boot:run -Dserver.port=8001 &'
    }
  }
}