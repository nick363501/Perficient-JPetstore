node {
  def MVN_HOME
  stage('Build') {
    git 'https://github.com/nick363501/Perficient-JPetstore.git'
    MVN_HOME="/usr"

    if (isUnix()) {sh "'${MVN_HOME}/bin/mvn' clean package"}
    else {bat(/"${MVN_HOME}\bin\mvn" clean package/)}
    }

  stage('Publish JUnit Results') {
    archive 'target/*.jar'
    }
}
