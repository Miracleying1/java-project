properties([pipelineTriggers([githubPush()])])
node('linux') {   
    stage('Build'){
        git credentialsId: '52918e40-34ba-4a36-81ae-250806128578', url: 'https://github.com/Miracleying1/java-project.git'  
        sh "ant"        
    }
    stage('Unit Tests') {   
        sh'ant -f test.xml -v'
        junit 'reports/result.xml'
    }   
    stage('Build') {    
        sh'ant -f build.xml -v'
    }   
    stage('Deploy') {    
        sh 'aws s3 cp /workspace/java-pipeline/dist/rectangle-${BUILD_NUMBER}.jar s3://hw10s3'
    } 
	stage ('Report'){  
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'AWS user for Jenkins', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
            sh 'aws cloudformation describe-stack-resources --stack-name jenkins --region us-east-1' 
        }
	}
}
