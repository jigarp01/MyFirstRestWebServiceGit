pipeline {
    agent any
    
    tools {
        maven 'Maven'
    }
    triggers{
        pollSCM('* * * * *')
    }

    stages {
        stage('Build') {
            steps {
                echo "Building .... "
                sh 'mvn --version'
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
                sh "scp -i /home/ec2-user/MyEC2NewKP.pem **/target/*.war ec2-user@18.215.243.117:/var/lib/tomcat8/webapps"
            }
        }
    }
}
