podTemplate(
    name: 'default',
    label: 'default',
    containers:[
        // containerTemplate(name: 'docker', image:'trion/jenkins-docker-client'),
        containerTemplate(name: 'maven',  image:'maven:3.6.3-amazoncorretto-8', args: 'cat', ttyEnabled: true, command: '/bin/sh -c'),
    ],
    {
        //node = the pod label
        node('default'){
            //container = the container label
            stage('Build'){
                container('maven'){
                    sh ' echo in container maven'
                    sh 'pwd'
                    sh 'mvn clean install -DskipTests=true'
                   
                }
            }
        }
    })
