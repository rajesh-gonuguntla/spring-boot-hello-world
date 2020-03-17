podTemplate(
    name: 'default',
    label: 'default'
    {
        //node = the pod label
        node('default'){
            //container = the container label
            stage('Build'){
                //container('maven'){
                    sh 'cd /home/jenkins/workspace/spring-boot-hello-world_master';
                    sh 'mvn clean install -DskipTests';
               // }
            }
        }
    })
