String credentialsId = 'id-cred-aws-20220204'

pipeline {
    agent {
        kubernetes {
            yaml '''
              apiVersion: v1
              kind: Pod
              spec:
                containers:
                - name: terraform
                  image: hashicorp/terraform
                  command:
                  - cat 
                  tty: true
            '''
        }
    }
    stages {
        stage('terraform init'){
            steps{
                container('terraform'){
                    withCredentials([[
                        $class: 'AmazonWebServicesCredentialsBinding',
                        credentialsId: credentialsId,
                        accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                        secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'
                        ]]) {
                            ansiColor('xterm') {
                              sh 'terraform init'
                            }
                    }
                }
            }
        }
        stage('terraform plan'){
            steps{
                container('terraform'){
                    withCredentials([[
                        $class: 'AmazonWebServicesCredentialsBinding',
                        credentialsId: credentialsId,
                        accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                        secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'
                        ]]) {
                            ansiColor('xterm') {
                              sh 'terraform plan'
                            }
                    }
                }
            }
        }
        stage('terraform show'){
            steps{
                container('terraform'){
                    withCredentials([[
                        $class: 'AmazonWebServicesCredentialsBinding',
                        credentialsId: credentialsId,
                        accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                        secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'
                        ]]) {
                            ansiColor('xterm') {
                              sh 'terraform show'
                            }
                    }
                }
            }
        }
    }
}