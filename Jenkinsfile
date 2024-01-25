pipeline {
    agent any
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
            steps {
                script{
                    echo "Compiling in ${params.ENV} environment"
                    sh 'mvn compile'
                }
                }
            }
        stage('UnitTest') {
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
            steps {
                script{
                    echo "Package the Code  ${params.APPVERSION}"
                    sh 'mvn package'
                }
                }
            }
        }
}

