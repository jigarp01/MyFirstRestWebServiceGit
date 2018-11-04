pipeline {
    agent any

    triggers{
        pollSCM('* * * * *')
    }

    stages {
        stage('Build') {
            steps {
                echo "Building .... "
                echo $PATH
                sh 'mvn clean package'
            }
            post {
                success {
                    echo "Now Archiving ... "
                    archiveArtifacts artifacts: '**/target/*.war'

                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Deploy to Staging Started... "
            }
        }
    }
}
