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
<<<<<<< HEAD
            sshagent(['build_server']) {
                steps {
=======
            steps {
>>>>>>> e0d8f901029587f069d6dc3890d4f64309959524
                script{
                    echo "Compiling in ${params.ENV} envgit push ironment"
                    sh "scp ec2-user@172.31.36.175 server-config.sh ec2-user@172.31.36.175:/home/ec2-user"
                    sh "ssh ec2-user@172.31.36.175 'bash ~/server-config.sh'"
                }
                }
            }
            }
        stage('UnitTest') {
<<<<<<< HEAD
            agent any
=======
            agent {label  'linux_slave'}
>>>>>>> e0d8f901029587f069d6dc3890d4f64309959524
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
<<<<<<< HEAD
             agent any
=======
            agent any
>>>>>>> e0d8f901029587f069d6dc3890d4f64309959524
            steps {
                script{
                    echo "Package the Code  ${params.APPVERSION}"
                    sh 'mvn package'
                }
                }
            }
        }
}

