pipeline {
    agent {
        // Use a Java-capable agent
        docker {
            image 'openjdk:11'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout code from SCM
                checkout scm
                
                // Display information about the checked out code
                echo "Checked out repository"
                sh 'ls -la'
            }
        }
        
        stage('Compile') {
            steps {
                // Compile the Java file
                sh 'javac Sum.java'
                echo "Compilation completed"
            }
            post {
                success {
                    echo "Successfully compiled Sum.java"
                }
                failure {
                    echo "Failed to compile Sum.java"
                }
            }
        }
        
        stage('Execute') {
            steps {
                // Run the compiled Java program and capture its output
                script {
                    def output = sh(script: 'java Sum', returnStdout: true).trim()
                    echo "Program output: ${output}"
                }
            }
            post {
                success {
                    echo "Successfully executed Sum program"
                }
                failure {
                    echo "Failed to execute Sum program"
                }
            }
        }
    }
    
    post {
        always {
            echo "Pipeline execution completed"
        }
        success {
            echo "Pipeline executed successfully"
        }
        failure {
            echo "Pipeline execution failed"
        }
    }
}

