podTemplate(
    name: 'default',
    label: 'default',
    containers:[
        // containerTemplate(name: 'docker', image:'trion/jenkins-docker-client'),
        containerTemplate(name: 'maven',  image:'maven:3.6.3-amazoncorretto-8', args: 'cat', ttyEnabled: true, command: '/bin/sh -c'),
    ],
    {
        //node = the pod label
        GITHUB_PROJECT="https://github.com/rajesh-gonuguntla/spring-boot-hello-world.git"
        GITHUB_CREDENTIALS_ID = 'github' //maps to a Jenkins Credentials Vault ID
        APPLICATION_NAME = "Sample-App"
        GITHUB_BRANCH = 'master'
        
        node('default'){
            stage ('Listing Branches') {
                echo "Initializing workflow"
                //checkout code
                echo GITHUB_PROJECT
                git url: GITHUB_PROJECT, credentialsId: GITHUB_CREDENTIALS_ID
                sh 'git branch -r | awk \'{print $1}\' ORS=\'\\n\' >branches.txt'
                sh "cut -d '/' -f 2 branches.txt > branch.txt"
                sh "cat ./branch.txt"
                //sh “sed s’/origin”\’///g branches.txt > branch.tx”
                //sed ‘s/$/from S0 to S1/’
            }
            stage('get build branch Parameter User Input') {
                sh 'echo hello world'
                liste = readFile 'branch.txt'
                echo "please click on the link here to chose the branch to build"
                env.BRANCH_SCOPE = input message: 'Please choose the branch to build ', ok: 'Validate!',
                parameters: [choice(name: 'BRANCH_NAME', choices: "${liste}", description: 'Branch to build?')]
            }
            stage('Checkout external proj') {
                echo "${env.BRANCH_SCOPE}"
                git branch: "${env.BRANCH_SCOPE}",
                credentialsId: GITHUB_CREDENTIALS_ID,
                url: GITHUB_PROJECT

                sh "ls -lat"
                }
            
            //stage('checkout'){
            //checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'github', url: 'https://github.com/rajesh-gonuguntla/spring-boot-hello-world.git']]])
            
           // }

            stage('Build'){
                container('maven'){
                    sh ' echo in container maven'
                    sh 'pwd'
                    sh 'mvn clean install -DskipTests=true'
                   
                }
            }
        }
    })
