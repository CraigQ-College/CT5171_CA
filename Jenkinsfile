pipeline {
    agent any
    tools{
        git 'Default'
    }
    stages {
        stage ('Part 1: GetProject') {
            steps {
                git branch:'master', url:'https://github.com/CraigQ-College/CT5171_CA.git'
            }
        }
        stage ('Part 2: build') {
            steps {
                sh 'mvn clean:clean'
            }
        }
        stage ('Part 3: Package') {
            steps {
                sh 'mvn package'
            }
        }
	stage ('Part 4: Archive') {
            steps {
                archiveArtifacts allowEmptyArchive: true,
             	artifacts:'**/craigspetitions*.war'
            }
        }
	stage ('Part 5: Deploy') {
            steps {
                sh 'docker build -f Dockerfile -t myapp . ' 
                sh 'docker rm -f "myappcontainer" || true'
                sh 'docker run --name "myappcontainer" -p 8081:8080 --detach myapp:latest'
            }
        }
    }
}
