pipeline {
    agent {
        node {
            label 'AGENT-1' // Specifies the node with label 'AGENT-1' to run the pipeline on
        }
    }
    // environment { 
    //     packageVersion = '' // Placeholder for the package version extracted from the package.json file
    //     nexusURL = '172.31.21.186:8081' // URL for Nexus repository
    // }
    options {
        timeout(time: 1, unit: 'HOURS') // Set timeout of 1 hour for the entire pipeline
        disableConcurrentBuilds() // Prevents concurrent builds of the same job
    }

    // Uncomment the parameters block if you need to pass parameters
     parameters {
        string(name: 'version', defaultValue: '1.2.0', description: 'What is the artifact version?')
        string(name: 'environment', defaultValue: 'dev', description: 'Which environment is this?')
        // booleanParam(name: 'Destroy', defaultValue: 'false', description: 'What is Destroy?')
        // booleanParam(name: 'Create', defaultValue: 'false', description: 'What is Create?')
    }

    stages {
        stage('Deploy') {
            steps {
                sh """
                echo "version: ${params.version}"
                echo "environment: ${params.environment}"
                """
            }
        }
    }

    post {
        always {
            echo 'I will always say Hello again!..' // This will always run, regardless of the build result
            deleteDir() // Clean up workspace after the build
        }
        failure {
            echo 'This block of scripts runs only when the pipeline has failed, used generally to send some alerts' // Execute only on failure
        }
        success {
            echo 'I will say Hello when the pipeline is executed successfully' // Execute only on successful execution
        }
    }
}