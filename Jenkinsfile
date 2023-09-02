pipeline {
    agent any
    environment {
        MY_IMAGE = "my-web-app"
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    dockerBuild = docker.build(MY_IMAGE, '-f Dockerfile .')
                }
            }
        }
        stage('Deploy image') {
            steps {
                script {
                    def containers = sh(script: "docker ps -q -f ancestor=${MY_IMAGE}", returnStatus: true, returnStdout: true)

                    if (containers) {
                        sh "docker stop -f ${containers}"
                        sleep time: 10, unit: 'SECONDS'
                    }

                    sh "docker run -dp 8080:8080 ${MY_IMAGE}"
                }
            }
        }
    }
}
