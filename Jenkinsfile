pipeline{
    agent any

    stages{
        stage('Build Backend'){
            steps{
                echo 'Building project'
                sh 'mvn clean package -DskipTests=true'
            }
        }
        
        stage('Unit Tests'){
            steps{
                echo 'Unit tests'
                sh 'mvn test'
            }
        }

        stage('Sonar Analysis'){
            environment{
                scannerHome = tool 'SONAR_SCANNER'
            }
            steps{
                withSonarQubeEnv('SONAR_LOCAL'){
                    sh "${scannerHome}/bin/sonar-scanner -e -Dsonar.projectKey=DeployBack -Dsonar.host.url=http://localhost:9000 -Dsonar.login=e2f4f19844b1583e0e73d38c1cc6d15e40000fb2 -Dsonar.java.binaries=target -Dsonar.coverage.exclusions=**/mvn/**,**/src/test/**,**/model/**,**Application.java"
                }
            }
        }

        stage('Quality Gate'){
            steps{
                sleep(6)
                timeout(time: 1, unit: 'MINUTES'){
                    waitForQualityGate abortPipeline: true
                }
            }
        }

        stage('Deploy BackEnd'){
            steps{
                deploy adapters: [tomcat8(credentialsId: 'LoginTomcat', path: '', url: 'http://localhost:8001/')], contextPath: 'tasks-backend', war: 'target/tasks-backend.war'
            }
        }

        stage('API Test'){
            steps{
                dir('api-test') {
                    git credentialsId: 'github_login', url: 'https://github.com/laerteneto/tasks-api-test.git'
                    sh 'mvn test'
                }
            }
        }

    }
}


