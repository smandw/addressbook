pipeline {
    agent none
    tools{
        maven 'mymaven'
        jdk 'myjava'
    }
 
    parameters{
         string(name: 'ENV', defaultValue: 'DEV', description: 'env to compile')
         booleanParam(name: 'executeTest', defaultValue: true, description: 'decide to run tc')
         choice(name: 'APPVERSION', choices: ['1.1', '1.2', '1.3'], description: 'Pick app version')
    }
 environment{
        BUILD_SERVER='ec2-user@1172.31.36.175'
    }
       stages {
        stage('Compile') {
            agent any
             steps {
                script{
                    sshagent(['build_server']) {
                    echo "Compiling in ${params.ENV} envgit push ironment"
                   sh "scp -o StrictHostKeyChecking=no server-config.sh ${BUILD_SERVER}:/home/ec2-user"
                   sh "ssh -o StrictHostKeyChecking=no ${BUILD_SERVER} 'bash ~/server-config.sh'"
        
                }
                }
            }
            }
        stage('UnitTest') {
            agent any
            when{
                expression{
                    params.executeTest == true
                }
            }
            steps {
                script{
                    echo "Run the Unit test cases"
                    sh 'mvn test' 
                }
                }
            }
        stage('Package') {
             agent any
            steps {
                script{
                    echo "Package the Code  ${params.APPVERSION}"
                    sh 'mvn package'
                }
                }
            }
        }
}
