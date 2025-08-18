pipeline{
// all code will be written inside this block

agent  any 
// this is mandatory
// which server you want to run the pipeline
// any = current jenkisn server, where the pipeline will be executed

tools{
// it is not mandatory
// write the name of the tool that you are using in the pipeline
// we have configured this tool name in the manage jenkins --> tools section
maven 'mymaven'

}

stages{
    // this is mandatory
    // here we write what jobs pipeline has to execute
    stage('Clone Repo'){
        steps{
            // this is like build steps
            git 'https://github.com/Sonal0409/DevOpsCodeDemo.git'
        }
    }

    stage('Compile Code')
    {
        steps{
            sh 'mvn compile'
        }
    }
   
   stage('Code Review'){
    steps{
        sh 'mvn pmd:pmd'
    }
    post{
        success{
          recordIssues sourceCodeRetention: 'LAST_BUILD', tools: [pmdParser(pattern: '**/pmd.xml')]  
        }
    }
   }
    stage('Test code'){
        steps{
            sh 'mvn test'
        }
        post{
            success{
        
                junit 'target/surefire-reports/*.xml'
            }
        }
    }
    stage('Package Code')
    {
        steps{
            sh 'mvn package'
        }
    }

   }
}





