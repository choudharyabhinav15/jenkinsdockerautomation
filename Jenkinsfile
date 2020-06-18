node{

   def tomcatWeb = '/opt/apache-tomcat-7.0.104/webapps'
   def tomcatBin = '/opt/apache-tomcat-7.0.104/bin'
   
   def buildNo = BUILD_NUMBER
   
   def tomcatStatus = ''
   stage('SCM Checkout'){
      lock('ABC_PROP') {
        git 'https://github.com/choudharyabhinav15/webapp1.git'
      }
   }
   
   stage('Compile-Package-create-war-file'){
        // Get maven home path
        def mvnHome =  tool name: 'MAVEN_HOME', type: 'maven'   
        sh "${mvnHome}/bin/mvn install"
    }
    
    stage('DOCKER IMAGE BUILD'){
       sh "sudo docker build -t abhinav01503/mywebappdemo:${buildNo} ."
    }
   
    stage ('Docker login & Push') {
       withCredentials([string(credentialsId: 'DOCKER_HUB_PWD', variable: 'DOCKER_HUB_PWD')]) {
          sh "sudo docker login -u abhinav01503 -p ${DOCKER_HUB_PWD}"
      }
       sh "sudo docker push abhinav01503/mywebappdemo:${buildNo}"
    }
}
