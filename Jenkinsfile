SERVERDIRS = [ "DIRsxs-1" , "DIRxssxs-2" ]
cplxStrng = "";
pathA = "/api/one"
stringAAA ="1,2,3,4"
array=[]
arraString = ""

// node {
//   datas = readYaml file: 'deployment.yaml'
// }

pipeline {
    agent any
    environment {
        PROJECT_ID = 'wn-cloud-275704'
		CLUSTER_NAME = 'wn-cloud-portal-test'
		LOCATION = 'us-central1-c'
		CREDENTIALS_ID = 'gke'

        appname = "${appname}"
        namespace = "${namespace}"
        replicas = "${replicas}"
        imagePath = "${imagepath}"
        serviceName = "${servicename}"
        clusterIP = "${clusterip}"
        servicePort = "${serviceport}"
        protocol = "${protocol}"
    }
    stages {
        stage("Checkout code") {
            steps {
                checkout scm
            }
        }
        stage('Make folder for deployments scripts yaml') {
            steps {
                //echo 'Hello World'

                // echo "${datas}"
                // sh "echo ${datas} >> newyyyyml.yaml"

                sh "rm -rf k8s"
                sh "mkdir k8s"
                

                script {
                    print('appName '+env.appname)
                    print('namespace '+env.namespace)
                    print('replicas '+env.replicas)
                    print('imagePath '+env.imagePath)
                    print('serviceName '+env.serviceName)
                    print('clusterIP '+env.clusterIP)
                    print('servicePort '+env.servicePort)
                    print('protocol '+env.protocol)
                }
            }
        }
        stage('generate dynamic deployments') {
            steps {
                script {
                    appname = appname.split(',')
                    namespace = namespace.split(',')
                    replicas = replicas.split(',')
                    imagepath = imagepath.split(',')
                    servicename = servicename.split(',')
                    clusterip = clusterip.split(',')
                    serviceport = serviceport.split(',')
                    protocol = protocol.split(',')

                    for (int j = 0; j < appname.size(); j++) {
                        echo "${appname[j]}"
                        sh "cp deployment.yaml k8s/${appname[j]}.yaml"

                        sh "sed -i 's!-app-name-!${appname[j]}!g' k8s/${appname[j]}.yaml"
                        sh "sed -i 's!-name-space-!${namespace[j]}!g' k8s/${appname[j]}.yaml"
                        sh "sed -i 's!-repli-cas-!${replicas[j]}!g' k8s/${appname[j]}.yaml"
                        sh "sed -i 's!-image-path-!${imagepath[j]}!g' k8s/${appname[j]}.yaml"
                        sh "sed -i 's!-service-name-!${servicename[j]}!g' k8s/${appname[j]}.yaml"
                        sh "sed -i 's!-cluster-ip-!${clusterip[j]}!g' k8s/${appname[j]}.yaml"
                        sh "sed -i 's!-service-port-!${serviceport[j]}!g' k8s/${appname[j]}.yaml"
                        sh "sed -i 's!-proto-col-!${protocol[j]}!g' k8s/${appname[j]}.yaml"

                    }
                }
            }
        }

        // stage('generate dynamic deployments') {
        //     steps {
        //         script {
        //             ingressPathArray = ingressPaths.split(',')

        //             for (int j = 0; j < SERVERDIRS.size(); j++) {
        //                 //echo "${SERVERDIRS[i]}"
        //                 sh "cp ingressDynamic.yaml k8s/${SERVERDIRS[j]}.yaml"

        //                 cplxStrng = ""
        //                 for (int i = 0; i < ingressPathArray.size(); i++) {
        //                     echo "ingressPathArray : ${ingressPathArray[i]}"
        //                     //cplxStrng = cplxStrng + "\t"+ texts[i] + "|END|" //"/\n"

        //                     cplxStrng = cplxStrng + "      - path:" + ingressPathArray[i] + "|END|"
        //                     cplxStrng = cplxStrng + "        backend:" + "|END|"
        //                     cplxStrng = cplxStrng + "          serviceName: wncp-backend-service" + "|END|"
        //                     cplxStrng = cplxStrng + "          servicePort: 8080" + "|END|"
        //                     cplxStrng = cplxStrng + "      -----         " + "|END|"

        //                 }

        //                 sh "sed -i 's!-cplxStrng-!${cplxStrng}!g' k8s/${SERVERDIRS[j]}.yaml"

        //                 sh "sed -i 's/|END|/\\n/g' k8s/${SERVERDIRS[j]}.yaml"
        //             }
        //         }
        //     }
        // }

        stage('Create name space GKE') {
            steps{
                step([$class: 'KubernetesEngineBuilder', projectId: env.PROJECT_ID, clusterName: env.CLUSTER_NAME, location: env.LOCATION, manifestPattern: 'k8s/namespace-test.json', credentialsId: env.CREDENTIALS_ID, verifyDeployments: true])
            }
        } 
        stage('Applying all yaml to GKE') {
            steps{
                step([$class: 'KubernetesEngineBuilder', projectId: env.PROJECT_ID, clusterName: env.CLUSTER_NAME, location: env.LOCATION, manifestPattern: 'k8s/', credentialsId: env.CREDENTIALS_ID, verifyDeployments: true])
                // step([$class: 'KubernetesEngineBuilder', projectId: env.PROJECT_ID, clusterName: env.CLUSTER_NAME, location: env.LOCATION, manifestPattern: 'multi-deployment.yaml', credentialsId: env.CREDENTIALS_ID, verifyDeployments: true])
            }
        }

        // stage ('Looping') {
        //         steps	{
        //             //sh "sed -i 's/-cplxStrng-/hello:${cplxStrng}/g' ingressDynamic.yaml"

        //             script{
        //                 // for (int i = 0; i < SERVERDIRS.size(); i++) {
        //                 //     //echo "${SERVERDIRS[i]}"
        //                 //     // cplxStrng = cplxStrng + "\t"+ SERVERDIRS[i] //+ "\n"
        //                 //     sh "cp ingressDynamic.yaml k8s/${SERVERDIRS[i]}.yaml"
        //                 // }

                        
        //                 // texts = stringAAA.split(',')
        //                 // for (txt in texts) {
        //                 //     sh "echo ${txt}"
        //                 // }

        //                 // texts = param1.split(',')
        //                 // for (int i = 0; i < texts.size(); i++) {
        //                 //     echo "param1 for loop: ${texts[i]}"
        //                 //     cplxStrng = cplxStrng + "\t"+ texts[i] + "|END|" //"/\n"
        //                 // }



        //                 ingressPathArray = ingressPaths.split(',')
        //                 for (int i = 0; i < ingressPathArray.size(); i++) {
        //                     echo "ingressPathArray : ${ingressPathArray[i]}"
        //                     //cplxStrng = cplxStrng + "\t"+ texts[i] + "|END|" //"/\n"

        //                     cplxStrng = cplxStrng + "      - path:" + ingressPathArray[i] + "|END|"
        //                     cplxStrng = cplxStrng + "        backend:" + "|END|"
        //                     cplxStrng = cplxStrng + "          serviceName: wncp-backend-service" + "|END|"
        //                     cplxStrng = cplxStrng + "          servicePort: 8080" + "|END|"
        //                     cplxStrng = cplxStrng + "      -----         " + "|END|"

        //                 }



        //                 // string="QQ,WW,EE,TT"
        //                 // array=(echo $string | sed 's/,/\n/g')

        //                 // for (int i = 0; i < array.size(); i++) {
        //                 //     //echo "${SERVERDIRS[i]}"
        //                 //     arraString = arraString + "\t"+ array[i] //+ "\n"
        //                 // }
        //             }

        //             sh "sed -i 's!-cplxStrng-!${cplxStrng}!g' ingressDynamic.yaml"

        //             // sh "sed -i 's/|END|/\n/g' ingressDynamic.yaml"

        //             sh "sed -i 's/|END|/\\n/g' ingressDynamic.yaml"

        //             // sh "Array Split${arraString} >> ingressDynamic.yaml"

        //             //sh "echo version := 1.0.${cplxStrng} >> ingressDynamic.yaml"
                    

        //             //sh "printf '\t\t\t- path: %s\n' '${pathA}' >> ingressDynamic.yaml"
        //             //sh "printf '\t\t\t- path: %s\n' '${pathA}' >> ingressDynamic.yaml"

        //             //sh "printf '%s\t%s\n' 'Data1' '${cplxStrng}' >> ingressDynamic.yaml"
        //         }
        // }     
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
