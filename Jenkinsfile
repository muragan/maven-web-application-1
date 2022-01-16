node{
   
    stage('Fetch code from git')
    {
        git branch: 'development', credentialsId: 'a21b5e0b-cf0b-4b9e-a2b2-3c1c30a2dc02', 
        url: 'https://github.com/muragan/maven-web-application-1.git'
    }
    stage('Buildpackage'){
     sh "${mavenHome}/bin/mvn clean package"
    }
}
