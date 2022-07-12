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
                    junit '**/target/surefire-reports/TEST-*.xml'
                }
            }
        }

        stage('sonar scan'){
            steps {
              sh "mvn sonar:sonar -Dsonar.host.url=http://ec2-3-91-243-131.compute-1.amazonaws.com/ -Dsonar.login=sqp_a4c121c39873e54ac4bae23a4164328057f3d261"
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
