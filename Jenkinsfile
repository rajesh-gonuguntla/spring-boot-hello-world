podTemplate(
    name: 'default',
    label: 'default',
    {
        //node = the pod label
        node('default'){
            //container = the container label
            stage('Build'){
                //container('maven'){
                    sh 'mvn clean install -DskipTests'
               // }
            }
        }
    })
