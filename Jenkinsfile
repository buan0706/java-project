properties([pipelineTriggers([githubPush()])])
node('linux') {
    
    git credentialsId: 'github-cred', url: 'https://github.com/buan0706/java-project.git', branch: 'master'
    
    stage ("Unit Tests") {

        sh "ant -f test.xml -v"
        junit "reports/result.xml"
        
    }
    
    stage ("Build") {

        //sh "aws ec2 describe-instances --region us-east-1"
        
    }
    
    stage ("Deploy") {

        //sh "aws ec2 describe-instances --region us-east-1"
        
    }
    
    stage ("Report") {

        //sh "aws ec2 describe-instances --region us-east-1"
        
    }    

}



