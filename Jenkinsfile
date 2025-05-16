pipeline {
    agent any
  
    tools {
        maven 'Maven' 
    }
 
    stages {
        stage('Install Chrome') {
            steps {
                sh '''
                    wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
                    sudo apt install -y ./google-chrome-stable_current_amd64.deb
                '''
            }
        }
      
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/humhainpiyush/Java-TestNG-Selelnium.git' 
            }
        }
 
        stage('Build & Test') {
            steps {
                sh 'chmod +x driver/chromedriver'
                sh 'mvn clean test -Dsuite=single.xml'
            }
 
            post {
                success {
                    publishHTML ([
                        allowMissing: false,
                        alwaysLinkToLastBuild: false,
                        keepAll: true,
                        reportDir: 'target/surefire-reports',
                        reportFiles: 'emailable-report.html', 
                        reportName: 'Maven Test Report'
                    ])
                }
            }
        }
    }
}
