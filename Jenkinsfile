pipeline {

    agent any

    tools {
        jdk 'JAVA_HOME'
        maven 'M2_HOME'
    }

    stages {

        stage('GIT') {
            steps {
                git branch: 'main', url: 'https://github.com/MedEzzedineBenZbiba/timesheet-devops.git'
            }
        }

        stage('Compile Stage') {
            steps {
                sh 'mvn clean compile package'
            }
        }
        stage('Building image') {
            steps {
                sh 'docker build -t ezzdinbz/timesheet-devops:1.0.0 .'
            }
        }

       stage('Deploy Image') {
           steps {
               sh '''
                   echo "dckr_pat_kjJJgNHGXnSUsdbgj0xk5ywRNb4" | docker login -u "ezzdinbz" --password-stdin
                   docker push ezzdinbz/timesheet-devops:1.0.0
               '''
           }
       }


            stage('Docker compose') {
                              steps {
                                  sh 'docker compose up'
                              }
                          }


         stage('MVN Sonarqube') {
            steps {
                sh 'mvn sonar:sonar -Dsonar.token=sqa_c593b3768524667fc3c4e020f905ddb7a11c8bdb -Dmaven.test.skip=true'
            }
        }

         stage('Deploy to Nexus') {
            steps {
                sh 'mvn deploy -Dmaven.test.skip=true' 

            }
        }
        
    }
}
