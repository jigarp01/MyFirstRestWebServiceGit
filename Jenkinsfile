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
                echo "Deploy to Staging Started.... "
                sh 'ls -ltr /home/ec2-user'
                sh "scp -i /var/lib/jenkins/.ssh/MyEC2NewKP.pem -o StrictHostKeyChecking=no ./target/*.war ec2-user@52.90.215.101:/opt/apache-tomcat-8.5.34/webapps"
            }
        }
    }
}
