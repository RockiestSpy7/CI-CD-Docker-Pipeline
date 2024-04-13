pipeline {
    agent {
        label "Dev"
    }
    
    tools {
        jdk 'jdk17'
        maven 'maven3'
    }
    
    environment {
        SCANNER_HOME= tool 'sonar-scanner'
    }

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', credentialsId: 'git-cred', url: 'https://github.com/RockiestSpy7/Boardgame.git'
            }
        }
        stage('Compile') {
            steps {
                sh "mvn compile"
            }
        }
        stage('Test') {
            steps {
                sh "mvn test"
            }
        }
        stage('SonarQube Analsyis') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=BoardGame -Dsonar.projectKey=BoardGame \
                    -Dsonar.java.binaries=. '''
                }
            }
        }
        stage('OWASP Scan') {
            steps {
                dependencyCheck additionalArguments: '', odcInstallation: 'dp-check'
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }
        stage('Build') {
            steps {
               sh "mvn package"
            }
        }
        stage('Publish To Nexus') {
            steps {
               withMaven(globalMavenSettingsConfig: 'global-settings', jdk: 'jdk17', maven: 'maven3', mavenSettingsConfig: '', traceability: true) {
                    sh "mvn deploy"
                }
            }
        }
        stage('Build & Tag Docker Image') {
            steps {
                sh "docker build -t rockiestspy7/boardshack:latest ."
            }
        }
        stage('Docker Image Scan') {
            steps {
                sh "trivy image --format table -o trivy-image-report.html rockiestspy7/boardshack:latest "
            }
        }
        stage('Push Docker Image') {
            steps {
                sh "docker push rockiestspy7/boardshack:latest"
            }
        }
    }
}