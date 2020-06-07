pipeline{
    agent any

    stages{
        stage('Build Backend'){
            steps{
                echo 'Backend Downloaded'
                echo 'Building project'
                sh 'mvn clean package -DskipTests=true'
            }
        }
    }
}