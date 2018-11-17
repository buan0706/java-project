properties([pipelineTriggers([githubPush()])])
node('linux') {
    git credentialsId: 'github-cred', url: 'https://github.com/buan0706/java-project.git', branch: 'master'
    stage ("GetInstances") {

        sh "aws ec2 describe-instances --region us-east-1"
        
    }

    stage ("CreateInstance") {
    
        sh "aws ec2 run-instances --image-id ami-013be31976ca2c322 --count 1 --instance-type t2.micro --key-name mykeypair --security-group-ids sg-35153d79 --subnet-id subnet-eef57389 --region us-east-1"

    }
    
    stage ("TerminateInstance") {
    
        def output = sh returnStdout: true, script: 'aws ec2 describe-instances --region us-east-1 --filters "Name=instance-type,Values=t2.micro" "Name=instance-state-name,Values=pending" | jq -r ".Reservations[].Instances[].InstanceId"'
        sh "aws ec2 wait instance-running --region us-east-1 --instance-ids $output"
        sh "aws ec2 terminate-instances --region us-east-1 --instance-ids $output"
        
    }
}



