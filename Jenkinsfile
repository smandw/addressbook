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

       stages {
        stage('Compile') {
             agent any
            sshagent(['build_server']) {
                steps {
                script{
                    echo "Compiling in ${params.ENV} envgit push ironment"
                    sh "scp ec2-user@172.31.36.175 server-config.sh ec2-user@172.31.36.175:/home/ec2-user"
                    sh "ssh ec2-user@172.31.36.175 'bash ~/server-config.sh'"
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

