pipeline {
    agent any
    tools {
      maven 'maven3.1'
    }
    stages {
        
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/gargmukku07/simple-java-maven-app.git']])
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
                
            }
        }

        stage('Sonar') {
            steps {
                withSonarQubeEnv(installationName: 'SonarQube', credentialsId: 'sonarQube') {
                    sh 'mvn sonar:sonar'
                }
            }
          post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        
        // stage('Sonar') {
        //     steps {
        //         script {
        //             def scannerHome = tool 'sonarscanner';
        //             withSonarQubeEnv(credentialsId: 'sonarQube') {
        //                 sh "${scannerHome}/bin/sonar-scanner \
        //                         -Dsonar.projectKey=myprjdemo \
        //                         -Dsonar.projectName=DEMO-Project \
        //                         -Dsonar.projectVersion=1.5 \
        //                         -Dsonar.sources=src \
        //                         -Dsonar.java.binaries=."
                    
        //             }
                
        //         }
        //     }

        //     post {
        //         always {
        //             junit 'target/surefire-reports/*.xml'
        //         }
        //     }
        // }
    }
}
