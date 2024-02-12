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
      claimName: 'jenkins-pv-claim', 
      readOnly: false

      )
  ]) 

{
  node(POD_LABEL) {
    stage('Build Petclinic Java App') {
        git 'https://github.com/chhunkim3/simple-java-maven-app.git'
            container('maven') {
                stage('Build a Maven project') {
                    sh '''
                    echo "maven build"
                    mvn -B -ntp clean package -DskipTests
                    '''
                }
            }
        }
  }
}
