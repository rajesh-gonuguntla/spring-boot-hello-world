node('maven-pod') {
    stage('Checkout') {
        checkout scm
    }
    stage('Build'){
        container('maven-container') {
           mvn clean install -DskipTests
        }
    }
}
