node('maven-pod') {
    stage('Checkout') {
        checkout scm
    }
    stage('Build'){
        container('maven-container') {
           sh `mvn clean install -DskipTests`
        }
    }
}
