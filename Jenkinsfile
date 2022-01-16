node
{
    stage('Fetch code from git')
    {
        git branch: 'development', credentialsId: 'a21b5e0b-cf0b-4b9e-a2b2-3c1c30a2dc02', 
        url: 'https://github.com/muragan/maven-web-application-1.git'
    }
    
    stage('Buildpackage')
    {
        sh "${mavenHome}/bin/mvn clean package"
    }
    stage('SonarReport')
    {
    sh "${mavenHome}/bin/mvn clean sonar:sonar"
    }
    stage('NexusRepository'){
        
    sh "${mavenHome}/bin/mvn clean deploy"
    }
   
    stage('DeploytoTomcat')
    {
   /*
        sshagent(['bbc50c77-84f7-41d8-a29f-19a278b2f078']) {
        sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.126.241.213:/opt/apache-tomcat-9.0.56/webapps "
        }
    */
    deploy adapters: [tomcat9(credentialsId: 'ed4ccace-aed9-4752-b99c-50516be3f882', \
    path: '', url: 'http://172.31.41.180:8080/')], contextPath: null, war: '**/maven-web-application.war'
    }
    /*
    stage('EmailNotification')
    {
    emailext body: '''Build success for - Job : ${JOB_NAME}, Build.No:${BUILD_NUMBER}
    Thanks,
    Murlai''', subject: 'Build success for - Job : ${JOB_NAME}, Build.No:${BUILD_NUMBER}', to: 'muralitest.devops@gmail.com'
    }*/
    stage('setBuildNum')
    {
        buildName 'pipe-${BUILD_NUMBER}'
    }
}
