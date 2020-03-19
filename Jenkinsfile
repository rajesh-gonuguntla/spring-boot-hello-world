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
            stage ('Listing Branches') {
                echo "Listing Branches .."
                echo GITHUB_PROJECT
                git url: GITHUB_PROJECT, credentialsId: GITHUB_CREDENTIALS_ID
                sh 'git branch -r | awk \'{print $1}\' ORS=\'\\n\' >branches.txt'
                sh "cut -d '/' -f 2 branches.txt > branch.txt"
            }
            stage('get build branch Parameter User Input') {
                sh 'Please select the branch to build and compile ..'
                liste = readFile 'branch.txt'
                echo "please click on the link here to chose the branch to build"
                env.BRANCH_SCOPE = input message: 'Please choose the branch to build ', ok: 'Validate!',
                parameters: [choice(name: 'BRANCH_NAME', choices: "${liste}", description: 'Branch to build?')]
            }
            stage('Switching to the Selected Branch') {
                echo "${env.BRANCH_SCOPE}"
                git branch: "${env.BRANCH_SCOPE}",
                credentialsId: GITHUB_CREDENTIALS_ID,
                url: GITHUB_PROJECT
                sh "echo Current Branch is ";
                sh "echo git branch"
                sh "ls -lat"
                }

            stage('Build'){
                container('maven'){
  
                    sh 'pwd'
                    sh 'mvn clean install -DskipTests=true'
                   
                }
            }
        }
    })
