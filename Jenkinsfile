node {
   stage('git'){
       git 'https://github.com/spring-petclinic/spring-petclinic-angularjs.git'

   }
   stage('build&package'){
       sh 'mvn package'
   }
   stage('archive'){
       archive 'spring-petclinic-server/target/petclinic.jar'
   }
   
}
