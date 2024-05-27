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
            // steps section refers to individual pipeline steps/plugins
            // https://www.jenkins.io/doc/pipeline/steps/
            steps {
                // Use one of the pipeline basic steps to get started
                echo "Hello World !"

                // Lets try an another simple pipeline step
                sleep time: "${params.ARGS_SLEEP}", unit: 'SECONDS'

                // How about this ?
                sleep(
                    time: "${params.ARGS_SLEEP}",
                    unit: 'SECONDS'
                )

                // Build a job
                build(
                    job: 'topsail',
                    waitForStart: 'true'
                )

                // Now build a parameterized job
                build(
                    job: 'regression',
                    waitForStart: 'true',
                    parameters: [string(name: 'SLEEP_COMMAND_ARGS', value: "${params.ARGS_SLEEP}")]
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

