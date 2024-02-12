podTemplate(containers: [
  containerTemplate(
      name: 'maven',
      image: 'maven:3.8.1-jdk-8',
      command: 'sleep',
      args: '30d'
      )
  ], 
  
  volumes: [
  persistentVolumeClaim(
      mountPath: '/root/.m2/repository', 
      claimName: 'jenkins-pv-claim', 
      readOnly: false
      )
  ]) 

{
  node(POD_LABEL) {
    stage('Build Petclinic Java App') {
      git url: 'https://github.com/chhunkim3/simple-java-maven-app.git', branch: 'master'
      container('maven') {
        sh '''
        echo "maven build"
        mvn -B -DskipTests clean package
        '''
      }
    }
  }
}
