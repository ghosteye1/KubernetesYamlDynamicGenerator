SERVERDIRS = [ "DIR -1" , "DIR -2" ]

pipeline {
    agent any
    environment {
        param1 = "${param1}"
    }
    stages {
        stage("Checkout code") {
            steps {
                checkout scm
            }
        }
        stage('Hello') {
            steps {
                echo 'Hello World'
                script {
                    print('param '+env.param1)
                }
            }
        }
        stages	{
            stage ('Looping') {
                steps	{
                    script{
                        for (int i = 0; i < SERVERDIRS.size(); i++) {
                            echo "${SERVERDIRS[i]}"
                        }
                    }
                }
        }     
        // stage('Create name space GKE') {
        //     steps{
        //         //sh "sed -i 's/hello:latest/hello:${env.BUILD_ID}/g' deployment.yaml"
        //         step([$class: 'KubernetesEngineBuilder', projectId: env.PROJECT_ID, clusterName: env.CLUSTER_NAME, location: env.LOCATION, manifestPattern: 'k8s/namespace-test.json', credentialsId: env.CREDENTIALS_ID, verifyDeployments: true])
        //     }
        // } 
        // stage('Applying all yaml to GKE') {
        //     steps{
        //         //sh "sed -i 's/hello:latest/hello:${env.BUILD_ID}/g' deployment.yaml"
        //         //step([$class: 'KubernetesEngineBuilder', projectId: env.PROJECT_ID, clusterName: env.CLUSTER_NAME, location: env.LOCATION, manifestPattern: 'k8s/', credentialsId: env.CREDENTIALS_ID, verifyDeployments: true])
        //         step([$class: 'KubernetesEngineBuilder', projectId: env.PROJECT_ID, clusterName: env.CLUSTER_NAME, location: env.LOCATION, manifestPattern: 'multi-deployment.yaml', credentialsId: env.CREDENTIALS_ID, verifyDeployments: true])
        //     }
        // }
        // stage('Sending success response to portal') {
        //     steps{
        //         echo 'Sending success response to portal------>'

        //         script {
        //             def response = httpRequest "http://dummy.restapiexample.com/api/v1/employees"
        //             println('Status: '+response.status)
        //             println('Response: '+response.content)
        //         }
        //     }
        // }

    }    
}
