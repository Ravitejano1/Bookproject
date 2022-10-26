node{

   def tomcatWeb = 'C:\\apache-tomcat-9.0.68\\webapps'
   def tomcatBin = 'C:\\apache-tomcat-9.0.68\\bin'
   def tomcatStatus = ''
   stage('SCM Checkout'){
     git 'https://github.com/Ravitejano1/Bookproject.git'
   }
   stage('Compile-Package-create-war-file'){
      // Get maven home path
      def mvnHome =  tool name: 'Maven', type: 'maven'   
      bat "${mvnHome}/bin/mvn package"
      }
/*   stage ('Stop Tomcat Server') {
               bat ''' @ECHO OFF
               wmic process list brief | find /i "tomcat" > NUL
               IF ERRORLEVEL 1 (
                    echo  Stopped
               ) ELSE (
               echo running
                  "${tomcatBin}\\shutdown.bat"
                  sleep(time:10,unit:"SECONDS") 
               )
'''
   }*/
   stage('Deploy to Tomcat'){
     bat "copy target\\Bookproject.war \"${tomcatWeb}\\Bookproject.war\""
      deploy adapters: [tomcat9(credentialsId: '70bf7e74-4a07-4349-a42d-893a22866e00', path: '', url: 'http://localhost:8085/manager/html/list')], contextPath: 'Jenkinsfile', war: '**/*.war'
   }
      stage ('Start Tomcat Server') {
         sleep(time:5,unit:"SECONDS") 
         bat "${tomcatBin}\\startup.bat"
         sleep(time:100,unit:"SECONDS")
   }
}
