pipeline {
    agent any

    stages {
        stage("Build DB") {
            steps {
                sh'''
                    cat test.txt
                    docker image build -t my_mysql ./database
                    docker image ls
                    docker tag my_mysql:latest thien2002nhan/my_mysql:latest
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