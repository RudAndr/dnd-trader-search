node {
  stage("Compilation") {
    dir('search-service') {
      sh 'chmod +x ./mvnw'
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