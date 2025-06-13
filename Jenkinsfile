pipeline{
    agent {
        label 'agent-1'
    }
    environment{
        appVersion = ''

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
                    echo "Version is: "$packageJson.version"
                }
               
            }
        }
    }
}