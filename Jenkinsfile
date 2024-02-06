//Angent should have Java,Terrafrom,Aws cli,node js,& Sonar scanner. VPN sg group should be attached to Agent to connect to the catalogue because Agent has to connect to the catalogue server but cataloufe is accepting connection from VPN.
//The below stages are for Continues Integration process
//Stage-01 Get the version of the aplication.While doing the developments the application version will change (package.json file line no 3)
//Stage-02 Install Dependencies 
//Stage-03 Sonar Scanning
//Stage-04 Build i.e Zip all files(16_Jenkins_Catalogues) and create artifact
//Stage-05 Push Artifact to Nexus Repo
//Stage-06 Deploy. To pass the version & environmnet to the downstreat server.

pipeline {
    agent {
        node {
            label 'Agent' //Name of the Agent label 
        }
    }

    environment { 
        packageVersion = ''
        nexusURL = '172.31.81.162:8081' //Mention your Nexus Url
    }

    options {
        timeout(time: 1, unit: 'HOURS')
        disableConcurrentBuilds()  //It won't allow us to run two builds at a time.
    }

    parameters {
        booleanParam(name: 'Deploy', defaultValue: false, description: 'Toggle this value')
    }

    // build
    stages {
        stage('Get the version') { 
            steps {
                script { //Groovy scripting. def command is used declare a variable in pipeline.
                    def packageJson = readJSON file: 'package.json' //Now we will get all data from the package.json file and stores in packageJson by using Pipeline Utility Steps plugin.
                    packageVersion = packageJson.version //Now from that file we can take the version id. 
                    echo "application version: $packageVersion" //Calling from line no 12
                }
            }
        }
     }
     
    // post build
    post { 
        always { 
            echo 'Deleting the workspace folder...!'
            deleteDir() //Once we create the zip file and store it nexus we have to delete the workspace folder.If not we face issue while running second time.
        }
        failure { 
            echo 'This runs when pipeline is failed, used generally to send some alerts'
        }
        success{
            echo 'I will say Hello when pipeline is success'
        }
    }
}