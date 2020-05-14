SERVERDIRS = [ "DIRsxs -1" , "DIRxssxs -2" ]
cplxStrng = "A";
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

                sh "sed -i 's/-cus-content-/hello:${env.param1}/g' ingressDynamic.yaml"

                script {
                    print('param '+env.param1)
                }
            }
        }
        stage ('Looping') {
                steps	{
                    sh "sed -i 's/-cplxStrng-/hello:${cplxStrng}/g' ingressDynamic.yaml"

                    script{
                        for (int i = 0; i < SERVERDIRS.size(); i++) {
                            //echo "${SERVERDIRS[i]}"
                            cplxStrng = cplxStrng + "\t"+ SERVERDIRS[i] //+ "\n"
                        }
                    }

                    //sh "echo version := 1.0.${cplxStrng} >> ingressDynamic.yaml"
                    pathA = "/api/one"

                    sh "printf '\t\t\t- path: %s\n' '${pathA}' >> ingressDynamic.yaml"
                    sh "printf '\t\t\t- path: %s\n' '${pathA}' >> ingressDynamic.yaml"

                    //sh "printf '%s\t%s\n' 'Data1' '${cplxStrng}' >> ingressDynamic.yaml"
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
