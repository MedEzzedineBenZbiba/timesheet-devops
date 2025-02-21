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
                sh 'mvn clean compile'
            }
        }

         stage('MVN Sonarqube') {
            steps {
                sh 'mvn sonar:sonar -Dsonar.token=sqa_c593b3768524667fc3c4e020f905ddb7a11c8bdb -Dmaven.test.skip=true'
            }
        }
        
    }
}
