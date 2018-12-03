node {
  def MVN_HOME
  stage('Build') {
    git 'https://github.com/nick363501/Perficient-JPetstore.git'

    if (isUnix()) {sh "'${MVN_HOME}/bin/mvn' -Dmaven.test.failure.ignore clean package"}
    else {bat(/"${MVN_HOME}\bin\mvn" -Dmaven.test.failure.ignore clean package/)}
    }

  stage('Publish JUnit Results') {
    archive 'target/*.jar'
    }
}
