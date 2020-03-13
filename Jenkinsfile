node('maven-pod') {
    stage('Checkout') {
        checkout scm
    }
    stage('Build'){
        container('maven-container') {
            // This is where we build our code.
        }
    }
}
