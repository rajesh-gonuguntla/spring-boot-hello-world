podTemplate(
    name: 'default',
    label: 'default',
    containers:[
        containerTemplate(name: 'docker', image:'benhall/dind-jenkins-agent:v2'),
        containerTemplate(name: 'maven',  image:'maven:3.6.3-amazoncorretto-8', args: 'cat', ttyEnabled: true, command: '/bin/sh -c'),
    ],
      volumes: [
        hostPathVolume(mountPath: '/var/run/docker.sock',
        hostPath: '/var/run/docker.sock'),
    ],
    {
        GITHUB_PROJECT="https://github.com/rajesh-gonuguntla/spring-boot-hello-world.git"
        GITHUB_CREDENTIALS_ID = 'github' //maps to a Jenkins Credentials Vault ID
        APPLICATION_NAME = "sample-app"
        GITHUB_BRANCH = 'master'
        
        node('default'){
            
            stage ('Locating Branches') {
                echo "${APPLICATION_NAME}"
                git url: GITHUB_PROJECT, credentialsId: GITHUB_CREDENTIALS_ID
                sh 'git branch -r | awk \'{print $1}\' ORS=\'\\n\' >branches.txt'
                sh "cut -d '/' -f 2 branches.txt > branch.txt"
            }
            
            stage('User Input Needed. Select Branch Please.') {
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
                container('maven'){
                  sh 'mvn test'
                }
            }

            stage('Build'){
                container('maven'){
                    sh 'pwd'
                    sh 'mvn clean install -DskipTests=true'
                } 
            } 
            
            stage('Build Docker Image'){
                //app = docker.build("${APPLICATION_NAME")
                container('docker'){
                    sh "docker build -t ${APPLICATION_NAME} ."
                } 
            } 
        } 
       
    })
