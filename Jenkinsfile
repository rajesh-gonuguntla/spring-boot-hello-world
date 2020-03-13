
     node('maven') {
    stage('Checkout') {
        checkout scm
    }
    stage('Build'){
        container('maven') {
           sh 'which maven'
        }
    }
}

