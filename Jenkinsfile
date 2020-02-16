
node {
   parameters {
        string (name: 'GIT_BRANCH',           defaultValue: 'master',  description: 'Git branch to build')
        booleanParam (name: 'DEPLOY_TO_PROD', defaultValue: false,     description: 'If build and tests are good, proceed and deploy to production without manual approval')


        // The commented out parameters are for optionally using them in the pipeline.
        // In this example, the parameters are loaded from file ${JENKINS_HOME}/parameters.groovy later in the pipeline.
        // The ${JENKINS_HOME}/parameters.groovy can be a mounted secrets file in your Jenkins container.
/*
        string (name: 'DOCKER_REG',       defaultValue: 'docker-artifactory.my',                   description: 'Docker registry')
        string (name: 'DOCKER_TAG',       defaultValue: 'dev',                                     description: 'Docker tag')
        string (name: 'DOCKER_USR',       defaultValue: 'admin',                                   description: 'Your helm repository user')
        string (name: 'DOCKER_PSW',       defaultValue: 'password',                                description: 'Your helm repository password')
*/
    }
   stage('Git Clone') { 
      // Get some code from a GitHub repository
      git 'https://github.com/walidsaad/maven-jenkins-pipeline.git'
   }
        
   stage('Build Docker Maven Image') {
      // Run the maven docker build
   echo "Build Docker Maven Image With Sample WebApp"
   sh "docker build -t=\"mymaven:v2.0\" ./maven/"
   }
   stage('Generate Maven Artifact') {
   echo "Run Docker Container and Generate Artifcat"
   sh "docker run --rm -d -v /home/stagiaire/.m2:/root/.m2 -w /app/training-webapp/ --name test-maven  mymaven:v2.0 mvn clean install"
   
   }
    stage('Deploy Artifcat') {
      // Run the tomcat deploy
   echo "Build Tomcat Image with Artifact"
   sh "docker build -t=\"mytomcat:v2.0\" ./tomcat/"
   echo "Run Tomcat Container"
   sh "docker run --rm -d -v /home/stagiaire/.m2/repository/com/mycompany/app/training-webapp/1.0-SNAPSHOT/:/usr/local/tomcat/webapps/ -p 8888:8080 --name maven-webapp mytomcat:v2.0"
   }

}
