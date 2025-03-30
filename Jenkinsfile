pipeline {
    agent any
    
    tools {
        maven 'maven3'
    }
    
    environment{
        SCANNER_HOME = tool 'sonar-scanner'
    }

    stages {
        stage('Git checkout/SCM') {
            steps {
                 git branch: 'main', url: 'https://github.com/venkiaws0306/Boardgame.git'
            }
        }
        
        stage('complile') {
            steps {
                bat "mvn compiler:compile"
            }
        }
        
        stage('test') {
            steps {
                bat "mvn test"
            }
        }
        
        stage('build') {
            steps {
               bat "mvn package"
            }
        }
        
        stage('SonarQube') {
            steps {
               withSonarQubeEnv('sonar') {
                   bat "%SCANNER_HOME%/bin/sonar-scanner -Dsonar.projectName=Boardgame -Dsonar.projectKey=Boardgame \
                 -Dsonar.java.binaries=."
                }
            }
        }
        
        
       
       stage('Deploy to Artifact') {
            steps {
              withMaven(globalMavenSettingsConfig: 'global-settings', jdk: 'jdk', maven: 'maven3', mavenSettingsConfig: '', traceability: true) {
                      bat "mvn deploy"     
              }
            }
        }
       
            
       
        
    }
}
