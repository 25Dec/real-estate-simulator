pipeline {
    agent any

    stages {
        stage("Build DB") {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-cre', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                    sh '''
                        docker image build -t my_mysql ./database
                        docker image ls
                        docker tag my_mysql:latest thien2002nhan/my_mysql:latest
                        docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD
                        docker push thien2002nhan/my_mysql:latest
                    '''
                }
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