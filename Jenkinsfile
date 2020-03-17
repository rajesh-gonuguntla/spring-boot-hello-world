podTemplate(
    name: 'default',
    label: 'default',
    containers: [
        containerTemplate(name: 'maven', image: 'maven:3.6.3-amazoncorretto-8', args: 'cat', command: '/bin/sh -c',  livenessProbe: containerLivenessProbe(execArgs: 'cat', failureThreshold: 2, initialDelaySeconds: 30, periodSeconds: 30, successThreshold: 2, timeoutSeconds: 30))
    ],
    {
        //node = the pod label
        node('default'){
            //container = the container label
            stage('Build'){
                container('maven'){
                    sh 'mvn clean install -DskipTests'
                }
            }
        }
    })
