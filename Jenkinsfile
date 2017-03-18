node {
  def MVN_HOME
  stage('Build') {
    git 'https://github.com/Perficient-DevOps/jpetstore-6'
    MVN_HOME = tool 'M3'

    if (isUnix()) {sh "'${MVN_HOME}/bin/mvn' -Dmaven.test.failure.ignore clean package"}
    else {bat(/"${MVN_HOME}\bin\mvn" -Dmaven.test.failure.ignore clean package/)}
    }

  stage('Publish JUnit Results') {
    junit '**/target/surefire-reports/TEST-*.xml'
    archive 'target/*.jar'
    }

  stage('Publish to Nexus') {
    nexusArtifactUploader artifacts: [[artifactId: 'jpetstore', classifier: '', file: 'target/jpetstore.war', type: 'war']], credentialsId: 'f874c3a9-2332-4efa-9b8c-09b98d8164e2', groupId: 'com.perficient', nexusUrl: '158.85.63.189:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'jenkins-preprod', version: '${BUILD_NUMBER}'
    }

  stage('UrbanCode Deploy Import from Nexus') {
    step([$class: 'UCDeployPublisher',
      siteName: '158.85.63.187',
      component: [
        $class: 'com.urbancode.jenkins.plugins.ucdeploy.VersionHelper$VersionBlock',
        componentName: 'JPetStore-J2EE',
        delivery: [
          $class: 'com.urbancode.jenkins.plugins.ucdeploy.DeliveryHelper$Pull',
          pullSourceType: 'Maven',
          pullProperties: 'MavenImportProperties/name=${BUILD_NUMBER}\nMavenImportProperties/description=Triggered import from Jenkins'
          ]]
      ])
    }
  }
