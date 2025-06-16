pipeline{
    agent {
        label 'agent-1'
    }
    environment{
        appVersion = ''
        project = 'expense'
        environment = 'backend'
        ACC_ID = 435238037339

    }
    options{
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()

    }
    stages{
        stage('read version'){
            steps{
                script{
                    def packageJson = readJSON file: 'package.json'
                    appVersion = packageJson.version
                    echo "Version is: $appVersion"

                }
               
            }
        }
        stage('install dependencies'){
            steps{
                script{
                    sh """
                    npm install
                    """
                }
            }
        }
        stage('build image'){
            steps{
                script{
                    withAWS(region: 'us-east-1', credentials: 'aws'){
                    sh """
                    aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin ${ACC_ID}.dkr.ecr.us-east-1.amazonaws.com
                    docker build -t ${ACC_ID}.dkr.ecr.us-east-1.amazonaws.com/${project}/${environment}:${appVersion} .
                    docker push ${ACC_ID}.dkr.ecr.us-east-1.amazonaws.com/${project}/${environment}:${appVersion}

                    """
                    }
                  
                }
            }
        }
    }
    post{
        always{
            echo "say hello always"
            deleteDir()
        }
        success{
            echo "say hello in success"
        }
        failure{
            echo "say hello in failure"
        }
       
    }
}