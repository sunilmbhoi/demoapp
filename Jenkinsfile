pipeline {
    agent any
    tools {
    maven 'maven-3.8.6'
    nodejs 'node-12.22.3' 
    }    
   parameters {
    string(name: 'tomcatURL', defaultValue: '', description: 'Tomcat URL')
    string(name: 'tomcatUSER', defaultValue: '', description: 'Tomcat USER')
    string(name: 'tomcatUserPassword', defaultValue: '', description: 'Tomcat PASSWORD')
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
        
        stage('Deploy-to-app-container') {
            steps {
                // Run deployment commands here
                // sh 'mvn deploy'
                script {
                    def tomcatUrl = '${params.tomcatURL}'  // Replace with your Tomcat URL
                    def tomcatUser = '${params.tomcatUSER}'  // Replace with your Tomcat username
                    def tomcatPassword = '${params.tomcatUserPassword}'  // Replace with your Tomcat password
                    //def warFilePath = "path/to/your/project/target/your-app.war"  // Replace with the actual path to your WAR file
                    def warFilePath = "${env.WORKSPACE}/target/demoapp.war" 
                
                    // Construct the URL to deploy the WAR
                    def deployUrl = "${tomcatUrl}/manager/text/deploy?path=/demoapp&update=true"
                
                    // Use curl to deploy the WAR file
                    sh "curl -T ${warFilePath} ${deployUrl} --user ${tomcatUser}:${tomcatPassword}"
                }
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

