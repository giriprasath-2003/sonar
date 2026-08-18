pipeline {
    agent any
 
    stages {
        stage('SCM Checkout') {
            steps {
                echo 'Git Clone'
                git branch: 'main', 
                credentialsId: 'Github-ID', 
                url: 'https://github.com/giriprasath-2003/sonar.git'
            }
        }
        stage('Code Coverage') {
            steps {
                bat 'echo This is sonarqube task perfect'
            }
        }
        stage('Sonarqube Analysis') {
            steps {
                script {
                    def scannerhome = tool name: 'sonarqube', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
                    
                withCredentials([string(credentialsId: 'sonarqube', variable: 'SONAR_TOKEN')]) {
                    bat """
                            ${scannerhome}/bin/sonar-scanner \
                            -Dsonar.projectKey=sonarqube \
                            -Dsonar.sources=app.js \
                            -Dsonar.host.url=http://65.0.177.159:9000 \
                            -Dsonar.login=${SONAR_TOKEN}
                       """
                    }
                
                } 
            }
        }
          
    }
}