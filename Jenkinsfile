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
            checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'github', url: 'https://github.com/rajesh-gonuguntla/spring-boot-hello-world.git']]])
            stage('Build'){
                container('maven'){
                    sh ' echo in container maven'
                    sh 'pwd'
                    sh 'mvn clean install -DskipTests=true'
                   
                }
            }
        }
    })
