podTemplate(containers: [
  containerTemplate(
      name: 'maven', 
      image: 'maven:latest', 
      command: 'sleep', 
      args: '99d'
      )
  ], 
  
  volumes: [
  persistentVolumeClaim(
      mountPath: '/root/.m2/repository', 
      claimName: 'maven-repo-storage', 
      readOnly: false
      )
  ]) 

{
  node(POD_LABEL) {
    stage('Build Petclinic Java App') {
      git url: 'https://github.com/chhunkim3/simple-java-maven-app', branch: 'master'
      container('maven') {
        sh 'mvn -B -ntp clean package -DskipTests'
      }
    }
  }
}
