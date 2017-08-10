node {
   stage ('Preparation'){
       git credentialsId: '26a4bb4a-2b9c-4e52-9178-827dbe6991b2', url: 'git@github.com:ConsiliumB/gildedrose.git'
   }
   stage ('Build'){
       sh 'docker run -i --rm --name my-maven-project -v "$PWD":/usr/src/mymaven -w /usr/src/mymaven maven:3-jdk-8 mvn clean install'
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
   }
   stage('Javadoc') {
      sh 'docker run -i --rm --name my-maven-project -v "$PWD":/usr/src/mymaven -w /usr/src/mymaven maven:3-jdk-8 mvn site'
   }
   stage('Archive') {
      archive 'target/gildedrose-*.jar'
      archive 'target/javadoc'
   }
}
