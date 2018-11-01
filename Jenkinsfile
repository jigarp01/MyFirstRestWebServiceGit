pipeline {
    agent any

    triggers{
        pollSCM('* * * * *')
    }

    stages {
        stage('Build') {
            steps {
                echo "Building .... "
                echo %JAVA_HOME%
                { set "JAVA_HOME=C:/Program Files (x86)/Java/jdk1.8.0_161" }
                echo %JAVA_HOME%
                bat 'mvn clean package'
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
