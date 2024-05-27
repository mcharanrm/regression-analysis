// A poor attempt to create a Jenkinsfile
pipeline {
    agent {
        label 'built-in'
    }
    parameters {
        string(
            name: 'ARGS_SLEEP',
            description: 'Provide an argument to the sleep command'
        )
    }
    stages {
        stage('testing') {
            steps {
                // Use one of the pipeline basic steps to get started
                echo "Hello World !"
                sleep time: "${params.ARGS_SLEEP}", unit: 'SECONDS'

                // How about this
                sleep(
                    time: "${params.ARGS_SLEEP}",
                    unit: 'SECONDS'
                )
            }
            // Multuple steps sections are not allowed in one single stage block
            /*
            steps {
                sleep time: "${params.ARGS_SLEEP}", unit: 'SECONDS'
            }
            */
        }
    }
}
