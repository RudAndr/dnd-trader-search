node {
  stage('Checkout Repo') {
    dir('search-service') {
      checkout([$class: 'GitSCM',
                branches: [[name: '*/master']],
                userRemoteConfigs: [[url: 'https://github.com/RudAndr/dnd-trader-search.git']]])
    }
  }

  stage("Compilation") {
    dir('search-service') {
      sh "./mvnw clean install -DskipTests"
    }
  }

  stage("Tests and Deployment") {
    stage("Running unit tests") {
      dir('search-service') {
        sh "./mvnw test -Punit"
      }
    }
    stage("Deployment") {
      dir('search-service') {
        sh 'nohup ./mvnw spring-boot:run -Dserver.port=8001 &'
      }
    }
  }
}