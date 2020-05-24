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
                dir('api-test') {
                    git credentialsId: 'github_login', url: 'https://github.com/igoritosousa/tasks-api-test'
                    bat 'mvn test'       
                }
            }
        }
        stage('Deploy Frontend'){
            steps{
                dir('frontend') {
                    git credentialsId: 'github_login', url: 'https://github.com/igoritosousa/tasks-frontend'
                    bat 'mvn clean package'
                    deploy adapters: [tomcat8(credentialsId: 'TomcatID', path: '', url: 'http://localhost:8001/')], contextPath: 'tasks', war: 'target/tasks.war'       
                }
            }
        }
        stage('Veracode Analisys'){
            steps{
                veracode applicationName: 'Application Tasks - Demo', criticality: 'VeryHigh', fileNamePattern: '', replacementPattern: '', sandboxName: 'sb-application-tasks', scanExcludesPattern: '', scanIncludesPattern: '', scanName: '$buildnumber', teams: '', uploadExcludesPattern: '', uploadIncludesPattern: '**/**.war', vid: '9e58155a16086227d811ed1dd9d520a3', vkey: '697e8b3b1a7e64b1b96ddd7a5c9db95bbc61a5ac07ae93be99d18aef42d6973d9faaae07d0a1fa60902d6045d556198a0095789136a1820ac94bb7d02d20da72', waitForScan: true
            }
        }
    }
}





