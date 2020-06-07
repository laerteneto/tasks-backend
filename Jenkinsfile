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

    }
}