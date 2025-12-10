pipeline {
    agent { label 'dev' }

    stages {
        stage('Pull SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/andifathulms/financial-record-go-mysql.git'
            }
        }
        
        stage('Build') {
            steps {
                sh'''
                cd app
                go mod tidy
                '''
            }
        }
        
        stage('Code Review') {
            steps {
                sh'''
                cd app
                sonar-scanner   -Dsonar.projectKey=app-fathul   -Dsonar.sources=.   -Dsonar.host.url=http://172.23.10.14:9000   -Dsonar.token=sqp_364446af1227834d0b5c1f101c69a40dfd87287e
                '''
            }
        }
        
        stage('Deploy') {
            steps {
                sh'''
                docker compose up --build -d
                '''
            }
        }
        
        stage('Backup') {
            steps {
                 sh 'docker compose push' 
            }
        }
    }
}
