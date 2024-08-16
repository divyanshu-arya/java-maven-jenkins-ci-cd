pipeline {
    agent any

    stages {
        stage('Application Deployment') {
            agent {
                label 'application'
            }
            steps {
                sh '''
				sudo rm -rf *
    				git clone https://github.com/divyanshu-arya/java-maven-jenkins-ci-cd/
				cd java-maven-jenkins-ci-cd/
				docker build -t tomcat .
				docker run -d -p 8080:8080 --name tomcat-server tomcat
    				cp /home/ubuntu/Mumbai.pem .
				scp -i "Mumbai.pem" -r init-scripts docker-compose.yml ubuntu@10.0.140.175:/home/ubuntu
				'''
            }
        }
        stage('Database Deployment') {
			agent {
                label 'database'
            }
            steps {
                sh '''
				cd /home/ubuntu/
				docker-compose up --build
				'''
            }
        }
    }
}
