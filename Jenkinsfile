pipeline {
    agent any

    stages {
        stage("Build DB") {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-cred', passwordVariable: 'password', usernameVariable: 'username')]){
                    sh '''
                        echo "${password} | docker login -u ${username} --password-stdin"
                        docker image build -t my_mysql ./database
                        docker tag my_mysql:latest thien2002nhan/my_mysql:latest
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