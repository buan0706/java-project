properties([pipelineTriggers([githubPush()])])
node('linux') {
    
    git credentialsId: 'github-cred', url: 'https://github.com/buan0706/java-project.git', branch: 'master'
    
    stage ("Unit Tests") {

        sh "ant -f test.xml -v"
        junit "reports/result.xml"
        
    }
    
    stage ("Build") {

        sh "ant -f build.xml -v"
        
    }
    
    stage ("Deploy") {

        sh "aws s3 cp /workspace/java-pipeline/dist/rectangle-${BUILD_NUMBER}.jar s3://buan0706-bucket/rectangle-${BUILD_NUMBER}.jar"
        
    }
    
    stage ("Report") {
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: '8460f80a-8627-453d-b0d0-0218436bae3c', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
        sh "aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins"
}

    }
        
       

}



