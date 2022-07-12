pipeline {

    agent {
        docker {
            image "maven:3.8.6-jdk-11"
        }
    }

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
              sh "mvn clean verify sonar:sonar \
  -Dsonar.projectKey=maven-java-project \
  -Dsonar.host.url=http://ec2-3-91-243-131.compute-1.amazonaws.com \
  -Dsonar.login=sqp_a4c121c39873e54ac4bae23a4164328057f3d261"
            }
        }

        stage('Package'){
            steps {
                
                sh "mvn package"
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/target/*.war', followSymlinks: false
                }
            }
        }

    }

}
