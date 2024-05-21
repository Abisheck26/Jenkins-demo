pipeline {
    agent any

    environment {
        GO_VERSION = '1.21.5' 
        GOPATH = "${env.WORKSPACE}/go"
        PATH = "${env.GOPATH}/bin:${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Abisheck26/Jenkins-demo.git', branch: 'main'
            }
        }

        stage('Set up Go') {
            steps {
                sh 'wget https://golang.org/dl/go${GO_VERSION}.linux-amd64.tar.gz'
                sh 'sudo tar -C /usr/local -xzf go${GO_VERSION}.linux-amd64.tar.gz'
                sh 'export PATH=$PATH:/usr/local/go/bin'
                sh 'go version'
            }
        }

        stage('Build') {
            steps {
                sh 'go build -o demo main.go'
            }
        }

        stage('Test') {
            steps {
                sh 'go test ./...'
            }
        }
        
        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'demo', fingerprint: true
            }
        }
    }
}
