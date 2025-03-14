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


         stage('MVN Sonarqube') {
            steps {
                sh 'mvn sonar:sonar -Dsonar.login=squ_03bfe3bbdc402fe989c8c1cec222f95456b6c770 -Dmaven.test.skip=true'
            }
        }

          stage('Deploy to Nexus') {
                    steps {
                        sh 'mvn deploy -Dmaven.test.skip=true'

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




        
    }
}
