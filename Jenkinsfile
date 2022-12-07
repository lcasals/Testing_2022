def textFiles = " "
pipeline {
    agent {
        kubernetes {
        yaml '''
        apiVersion: v1
        kind: Pod
        spec:
          containers:
          - name: maven
            image: maven:alpine
            command:
            - cat
            tty: true
        '''
        }
    }
    stages {
        stage('Build') {
            steps {
                echo "Building.."

                script {
                    echo "doing build stuff.."
                    textFiles= sh(returnStdout: true, script: 'find ./documents -iname *.txt')
                    echo "$textFiles"
                 }
            }
        }
        stage('Test') {
            steps {
                echo "Testing.."
                echo "Test Step - Value of textFiles = $textFiles"
                def texts = textFiles.split(' ')
                for (txt in texts) {
                    sh "echo ${txt}"
                    sh "cat ${txt}"    
                }
        }
        stage('Deliver') {
            steps {
                echo 'Deliver....'
                sh '''
                echo "doing delivery stuff.."
                '''
            }
        }
    }
}
