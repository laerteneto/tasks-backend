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
    }
}