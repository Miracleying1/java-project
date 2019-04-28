properties([pipelineTriggers([githubPush()])])
node('linux') {   
    stage('Unit Tests') {   
        git credentialsId: '52918e40-34ba-4a36-81ae-250806128578', url: 'https://github.com/Miracleying1/java-project.git'   
        sh'ant'  
        ant -f test.xml -v
        junit 'reports/result.xml'

    }   
    stage('Build') {    
        sh'ant'
        ant -f build.xml -v 
    }   
}
