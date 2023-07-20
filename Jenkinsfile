pipeline {
    tools {
        jdk 'myjava'
        maven 'mymaven'
    }
    
    agent any
    
    stages {
        stage ('CloneRepo') {
            steps {
                sh 'echo "Clone the repo"'
                git 'https://github.com/ravir1981/DevOpsCodeDemo.git'
            }
        }
        stage ('Compile the code') {
            steps {
                sh 'echo "Compile the code"'
                sh 'mvn compile'
            }
        }
        stage ('CodeReview') {
            steps {
                sh 'echo "Review the code"'
                sh 'mvn pmd:pmd'
            }
            post {
                success {
                    recordIssues(tools: [pmdParser(pattern: '**/pmd.xml')])
                }
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
        stage ('Package') {
            steps {
                sh 'echo "Package the code"'
                sh 'mvn package'
            }
        }
    }
}
