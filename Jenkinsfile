node('default') {
    stage('Checkout') {
        checkout scm
    }
    stage('Build'){
        container('maven') {
            sh 'echo which mvn'
        }
    }
}
