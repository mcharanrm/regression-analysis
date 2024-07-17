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

        credentials(
            credentialType: 'org.jenkinsci.plugins.plaincredentials.impl.FileCredentialsImpl',
            name: 'HOST_INVENTORY',
            required: true
        )
    }

    environment{
        HOST_INVENTORY = credentials('${params.HOST_INVENTORY}')
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



                echo "Lets see what is available in KUBE_CONFIG secret file"
                sh(
                    script: """#! /bin/bash
                    echo 'Reading a secret host inventory file'
                    echo -e ${HOST_INVENTORY}
                    
                    echo 'Running a ansible command on host inventory'
                    ansible fake_hosts -i ${HOST_INVENTORY} -m ping
                    """
                )

                /*
                The following builds doesn't track the exit status of the upstream job.
                So we need a way to capture it and handle it in order to control
                the pipeline execution flow.
                */

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

                // Now, lets imagine one of the existing jobs as a remote job and trigger using Parameterized Remote Trigger Plugin
                triggerRemoteJob(
                    job: 'http://localhost:8080/job/regression-analysis/job/topsail',
                    auth: CredentialsAuth(credentials: 'JENKINS_BASIC_AUTH'),
                    pollInterval: 1
                )

                triggerRemoteJob(
                    job: 'http://localhost:8080/job/regression-analysis/job/regression',
                    auth: CredentialsAuth(credentials: 'JENKINS_BASIC_AUTH'),
                    parameters: MapParameters(parameters: [MapParameter(name: 'SLEEP_COMMAND_ARGS', value: "${params.ARGS_SLEEP}")]),
                    pollInterval: 1
                )

            }
            // Multiple `steps` sections are not allowed within one single `stage` block
            /*
            steps {
                sleep time: "${params.ARGS_SLEEP}", unit: 'SECONDS'
            }
            */
        }
    }
}

