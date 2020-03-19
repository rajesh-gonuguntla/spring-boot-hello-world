podTemplate(
    name: 'default',
    label: 'default',
    containers:[
        containerTemplate(name: 'maven',  image:'maven:3.6.3-amazoncorretto-8', args: 'cat', ttyEnabled: true, command: '/bin/sh -c'),
    ],
    {
        //node = the pod label
        GITHUB_PROJECT="https://github.com/rajesh-gonuguntla/spring-boot-hello-world.git"
        GITHUB_CREDENTIALS_ID = 'github' //maps to a Jenkins Credentials Vault ID
        APPLICATION_NAME = "Sample-App"
        GITHUB_BRANCH = 'master'
        
        node('default'){
            stage ('Locating Branches') {
                git url: GITHUB_PROJECT, credentialsId: GITHUB_CREDENTIALS_ID
                sh 'git branch -r | awk \'{print $1}\' ORS=\'\\n\' >branches.txt'
                sh "cut -d '/' -f 2 branches.txt > branch.txt"
            }
            stage('User Input Needed. Select Branch Please.') {
                //sh 'echo Please select the branch to build and compile ..'
                liste = readFile 'branch.txt'
                sh "echo Click on the Link  to Select a Branch"
                env.BRANCH_SCOPE = input message: 'Please choose the branch to build ', ok: 'Validate!',
                parameters: [choice(name: 'BRANCH_NAME', choices: "${liste}", description: 'Branch to build?')]
            }
            stage(' Switching to Target Branch') {
                echo "${env.BRANCH_SCOPE}"
                git branch: "${env.BRANCH_SCOPE}",
                credentialsId: GITHUB_CREDENTIALS_ID,
                url: GITHUB_PROJECT
                sh "echo Current Branch is ";
                sh "echo git branch"
                sh "ls -lat"
             }
            
            stage('Test') {
                //steps {
                  sh 'mvn test'
                //}
               // post {
                //  always {
                 //   junit 'target/surefire-reports/*.xml'
                  //}
                //}
              }

            stage('Build'){
                container('maven'){
  
                    sh 'pwd'
                    sh 'mvn clean install -DskipTests=true'
                   
                } // Container ends here
            } // Stage ends here
        } // Stages ends here
        post {
        always {
            echo 'One way or another, I have finished'
            deleteDir() /* clean up our workspace */
        }
        success {
            echo 'I succeeeded!'
        }
        unstable {
            echo 'I am unstable :/'
        }
        failure {
            echo 'I failed :('
        }
        changed {
            echo 'Things were different before...'
        }
    }
    })
