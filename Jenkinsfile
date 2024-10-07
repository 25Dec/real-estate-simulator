pipeline {
    agent any

    stages {
        stage("Build DB") {
            steps {
                sh '''
                    docker image build -t my_mysql ./database
                    docker tag my_mysql:latest thien2002nhan/my_mysql:latest
                    docker login
                    docker push thien2002nhan/my_mysql:latest
                '''
            }
        }

        stage("Deploy to Server") {
            steps {
                sh'''
                    ansible-playbook -i ./ansible/hosts ./playbook.yml
                '''
            }
        }
    }
}