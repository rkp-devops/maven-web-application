
node{

def mavenHome = tool name: 'maven-3.8.6'

stage('CheckOutCode'){
git branch: 'development', credentialsId: 'c678bd0d-9fd5-42e3-88c2-ca3d4e398c6a', url: 'https://github.com/rkp-devops/maven-web-application.git'
}//CheckOutCode closing

stage('Build'){
sh "$mavenHome/bin/mvn  package"
}

/* stage('ExeSonarQubeGenerator'){
sh "$mavenHome/bin/mvn clean sonar:sonar"
} */

stage('UploadArtifactsIntoNexus'){
sh "$mavenHome/bin/mvn  clean deploy"
}

stage('DeployAppIntoTomcatServer'){
sshagent(['b2654455-2926-4255-b28c-3f8e39c15055']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@172.31.13.12:/opt/tomcat/webapps"
}
}
 
}//Node Closing
