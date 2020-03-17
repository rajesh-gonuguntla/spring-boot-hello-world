podTemplate(
    name: 'default',
    label: 'default',
    containers: [
        containerTemplate(name: 'maven', image: '3.6.3-amazoncorretto-8')
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
