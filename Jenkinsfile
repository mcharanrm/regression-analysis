// A poor attempt to create a Jenkinsfile
pipeline {
    agent {
        label 'built-in'
    }

    parameters {
        string(
            name: 'SLEEP_COMMAND_ARGS',
            description: 'arguments to sleep command'
        )
    }

    stages {
        stage('testing') {
            steps {
                // Use one of the pipeline basic steps to get started
                echo "Hello World !"

                // Run an another pipeline step using sleep
                sleep time: "${SLEEP_COMMAND_ARGS}", unit: 'SECONDS'
            }
        }
    }
}
