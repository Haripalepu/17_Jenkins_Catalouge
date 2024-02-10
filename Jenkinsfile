#!groovy
@Library('roboshop-shared-library') _  //Name of the library. Mange jenkins - system configuration

// responsibility to pass what type of application and component/component is this to pipeline deicssion

def configMap = [
    application: "nodejsVM",
    component: "catalogue"
]
if( ! env.BRANCH_NAME.equalsIgnoreCase('main')){   //If the branch name is not main then run pipeline.
    pipelineDecission.decidePipeline(configMap)   //pipelineDecission is a file name in 17_shared_library
}
else{
    echo "This is PRODUCTION, deal with CR process"
}