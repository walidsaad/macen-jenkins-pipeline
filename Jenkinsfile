
node {
   stage('Git Clone') { 
      // Get some code from a GitHub repository
      git 'https://github.com/walidsaad/maven-jenkins-pipeline.git'
   }
        
   stage('Build') {
      // Run the maven docker build
   echo "Build Docker Maven App"
   }
  
     stage('Deploy') {
      // Run the tomcat deploy
   echo "Run Tomcat with Artifact"
   }

}
