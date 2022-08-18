pipeline{
  agent any
 
  stages {    

   stage("Opening"){
         steps{
            //Welcome message
            script{
               sh "echo 'Welcome to Calsoft'"
}
}
}

  stage("Workspace_cleanup"){
        //Cleaning WorkSpace
        steps{
            step([$class: 'WsCleanup'])

}
}

   stage("Repo_clone"){
       //Clone repo from GitHub
      steps {
         checkout ([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[credentialsId: 'mykey', url: 'https://github.com/shubh9975/cto-demo.git']]])


}
}

  stage("linting and formatiing"){
    //fmt and lint
     steps{
      script{

       sh '''
           echo "Formatting the Java Code"
           echo "Linting the Java Code"
      '''

}
}
}
  stage("Image Building"){
     steps{
      script{
       sh '''
           docker build -t cto .
           docker tag bfctech:v1 artifactory.bfctech.io:8087/adapt:v1
           docker tag  cto shubh9975/simple-app:v3.3.3
       '''
}
}
}
  stage("Image scanning"){
     steps{
      script{
       sh '''
            trivy image artifactory.bfctech.io:8087/adapt:v1
       '''
        
   stage("Docker Login & Image Push"){
     steps{
      script{
       sh '''
            docker login --username shubh9975 --password c65b19fc-7e5c-4553-bf79-1e878a505365
            docker push shubh9975/simple-app:v3.3.3
       '''      
}
}
}
  

}
}
