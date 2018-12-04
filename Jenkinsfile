node {
   def mvnHome
   def jdkHome
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/Sanjiban2332/SanjibanLearning.git'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration. 
      jdkHome = tool 'JDK1.8'
      mvnHome = tool 'MAVEN'
	  env.JAVA_HOME = "C:\\Program Files\\Java\\jdk1.8.0_191"
   }
   
   stage('build & SonarQube') {
      // Run the maven build
         bat(/"${mvnHome}\bin\mvn" clean install sonar:sonar/)
   }
   
   stage('Nexus') {
      configFileProvider([configFile(fileId: 'f64a4d2b-dd6c-4ce9-a3f5-ff4ee13c8273', targetLocation: 'settings.xml')]) {
      // Run the maven build
		 bat(/"${mvnHome}\bin\mvn" clean deploy -s settings.xml/)
	  }
   }   
   stage('Results') {
      junit 'target/surefire-reports/*.xml'  
   }
}
