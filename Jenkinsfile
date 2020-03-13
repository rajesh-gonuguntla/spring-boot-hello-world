podTemplate(cloud: 'opargo', containers: [containerTemplate(alwaysPullImage: true, args: 'cat', command: '/bin/sh -c', image: 'maven:3.6.3-jdk-11-openj9', livenessProbe: containerLivenessProbe(execArgs: '', failureThreshold: 0, initialDelaySeconds: 0, periodSeconds: 0, successThreshold: 0, timeoutSeconds: 0), name: 'maven', resourceLimitCpu: '', resourceLimitMemory: '', resourceRequestCpu: '', resourceRequestMemory: '', ttyEnabled: true, workingDir: '/home/jenkins/agent')], inheritFrom: '', instanceCap: 0, label: 'maven', name: 'maven', namespace: 'tools', nodeSelector: '', podRetention: always(), serviceAccount: '', supplementalGroups: '', workspaceVolume: dynamicPVC(accessModes: 'ReadWriteOnce', requestsSize: '', storageClassName: ''), yaml: '') {
    // some block
     node {
    stage('Checkout') {
        checkout scm
    }
    stage('Build'){
        container('maven') {
           sh 'which maven'
        }
    }
}
}
