pipeline {
    agent any
    tools {
    maven 'maven-3.8.6'
    nodejs 'node-12.22.3' 
  }    
    stages {
        stage('Build') {
            steps {
                // Run build commands here
                sh 'mvn clean install'
            }
        }
        
        stage('Test') {
            steps {
                // Run test commands here
                sh 'mvn test'
            }
        }
        
        stage('Deploy') {
            steps {
                // Run deployment commands here
                sh 'mvn deploy'
            }
        }
    }
    
    post {
        success {
            // Actions to perform on successful build
            echo 'Build successful!'
        }
        
        failure {
            // Actions to perform on failed build
            echo 'Build failed!'
        }
    }
}

