pipeline {
    tools {
        jdk 'myjava'
        maven 'mymaven'
    }
    
    agent any
    
    stages {
        stage ('CloneRepo') {
            steps {
		sh 'echo "Cloning the repo"'
                git 'https://github.com/ravir1981/DevOpsCodeDemo.git'
            }
        }
        stage ('Compile the code') {
            steps {
                sh 'echo "Compiling the code"'
                sh 'mvn compile'
            }
        }
        stage ('Code Review') {
            steps {
		sh 'echo "Review the code"'
                sh 'mvn pmd:pmd'
            }
        }
        stage ('Unit Test') {
            steps {
		sh 'echo "Test the code"'
                sh 'mvn test'
            }
            post {
                success {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage ('Package the Code') {
            steps {
		sh 'echo "Package the code"'
                sh 'mvn package'
            }
        }
    }
}
