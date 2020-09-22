node{
     
    stage('SCM Checkout'){
        git credentialsId: 'GIT_CREDENTIALS', url: 'https://github.com/arjun1128/spring-boot-mongo-docker.git',branch: 'master'
    }
    
    stage(" Maven Clean Package"){
      def mavenHome =  tool name: "Maven-3.6.3", type: "maven"
      def mavenCMD = "${mavenHome}/bin/mvn"
      sh "${mavenCMD} clean package"
      
    } 
    
    
    stage('Build Docker Image'){
        sh 'docker build -t arjunps/spring-boot-mongo .'
    }
    
    stage('Push Docker Image'){
        withCredentials([string(credentialsId: 'DOCKER_HUB_CREDENTIALS', variable: 'DOCKER_HUB_CREDENTIAL')])
         {
          sh "docker login -u arjunps -p ${DOKCER_HUB_CREDENTIAL}"
        }
        sh 'docker push arjunps/spring-boot-mongo'
     }
     
}
