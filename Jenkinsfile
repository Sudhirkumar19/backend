pipeline {
    agent {
        label 'AGENT-1'
    }
    options{
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
        //retry(1)
    }



    environment {
        DEBUG = 'true'
        appVersion = ' '
    }

    
    
    stages {
        stage('Read the version') {
            steps {
                script {
                    def packageJson = readJSON file : 'package.json'
                    appVersion = packageJson.version
                    echo "App Version : ${appVersion}"
                }
            }
        }
        stage('install dependencies') {
            steps {
                sh 'npm install'
                sh 'env'
            }
        }
        stage('Docker build') {
            
            steps {

                    sh """
                    docker build -t myapp/backend:${appVersion} 
                    docker images                 """
                    //error 'pipeline failed'

            }
        }
        stage('Print Params'){
            steps{
                echo "Hello ${params.PERSON}"
                echo "Biography: ${params.BIOGRAPHY}"
                echo "Toggle: ${params.TOGGLE}"
                echo "Choice: ${params.CHOICE}"
                echo "Password: ${params.PASSWORD}"  
            }
        }
       
    }

    post {
        always{
            echo "This sections runs always"
            deleteDir()
        }
        success{
            echo "This section run when pipeline success"
        }
        failure{
            echo "This section run when pipeline failure"
        }
    }
}