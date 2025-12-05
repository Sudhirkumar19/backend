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
                    def packageJSON = readJSON : 'package.json'
                    appVersion = packageJSON.version
                    echo "App Version is ${appVersion}"
                }
            }
        }
        stage('Test') {
            steps {
                sh 'echo This is test'
                sh 'env'
            }
        }
        stage('Deploy') {
            when {
                expression { env.GIT_BRANCH != "origin/main" }
            }
            steps {

                    sh 'echo This is deploy'
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