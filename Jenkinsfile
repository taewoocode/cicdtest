pipeline {
    agent any
    stages {
        stage('git scm update') {
            steps {
                git url: 'https://github.com/taewoocode/cicdtest.git', branch: 'main'
            }
        }
        stage('docker build and push') {
            steps {
                sh '''
                sudo docker build -t taewoocode/cicdtest:green .
                sudo docker push taewoocode/cicdtest
                '''
            }
        }
        stage('deploy kubernetes') {
            steps {
                sh '''
                kubectl create deployment pl-bulk-prod --image=taewoocode/cicdtest:green
                kubectl expose deployment pl-bulk-prod --type=LoadBalancer --port=80 \
                                                       --target-port=80 --name=pl-bulk-prod
                '''
            }
        }
    }
}
