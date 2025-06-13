pipeline{
    agent {
        label 'agent-1'
    }
    environment{
        appVersion = ''

    }
    options{

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
    }
}