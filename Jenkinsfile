pipeline{
    agent any
    stages{
        stage('Build Backend'){
            steps{
                bat 'mvn clean package -DskipTests=true'
            }
        }
        stage('Testes unitarios'){
            steps{
                bat 'mvn test'
            }
        }

        stage('Deploy BackEnd'){
            steps{
                deploy adapters: [tomcat8(credentialsId: 'TomcatID', path: '', url: 'http://localhost:8001/')], contextPath: 'tasks-backend', war: 'target/tasks-backend.war'
            }
        }

        stage('Teste de API'){
            steps{
                git credentialsId: 'github_login', url: 'https://github.com/igoritosousa/tasks-api-test'
                bat 'mvn test'
            }
        }
    }
}


