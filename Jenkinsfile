pipeline {

    agent any

    stages {

        stage('Build'){
            steps {
                sh "mvn clean"

                sh "mvn compile"
            }
        }

        stage('Test'){
            steps {
                
                sh "mvn test"
            }

            post {
                always {
                    junit '**/target/surefire-reports/Test-*.xml'
                }
            }
        }

        stage('sonar scan'){
            steps {
              sh "mvn sonar:sonar -Dsonar.host.url=http://ec2-3-91-243-131.compute-1.amazonaws.com/ -Dsonar.login=sqa_f0f168940baab039aa6ce3d35f5cdb95dfa33bc0"
            }
        }

        stage('Package'){
            steps {
                
                sh "mvn package"
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/target/*.jar', followSymlinks: false
                }
            }
        }

    }

}
