node {
  def MVN_HOME
  stage('Build') {
    git 'https://github.com/Perficient-DevOps/jpetstore-6'
    MVN_HOME = tool 'M3'

    if (isUnix()) {sh "'${MVN_HOME}/bin/mvn' -Dmaven.test.failure.ignore clean package"}
    else {bat(/"${MVN_HOME}\bin\mvn" -Dmaven.test.failure.ignore clean package/)}
    }

  stage('Publish JUnit Results') {
    archive 'target/*.jar'
    }
}