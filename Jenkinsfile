podTemplate(
    name: 'opargo-build-agent',
    label: 'opargo-build-agent',
    containers:[
        // containerTemplate(name: 'docker', image:'trion/jenkins-docker-client'),
        containerTemplate(name: 'maven', image:'maven:3.6.3-amazoncorretto-8', args: 'cat', ttyEnabled: true, command: '/bin/sh -c', workingDir: '/home/jenkins/agent/workspace/spring-boot-hello-world/'),
    ],
    {
        //node = the pod label
        node('opargo-build-agent'){
            //container = the container label
            stage('Build'){
                //container('maven'){
                    sh 'pwd'
                    sh 'ls --all'
               // }
            }
        }
    })
