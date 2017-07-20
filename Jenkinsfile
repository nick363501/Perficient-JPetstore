node {
  def MVN_HOME
  stage('Build') {
    git 'https://github.com/nick363501/jpetstore-6.git'
    MVN_HOME = tool 'maven3'

    if (isUnix()) {sh "'${MVN_HOME}/bin/mvn' -Dmaven.test.failure.ignore clean package"}
    else {bat(/"${MVN_HOME}\bin\mvn" -Dmaven.test.failure.ignore clean package/)}
    } 
  	stage('Publish JUnit Results') {
		junit 'var/lib/jenkins/jobs/JPetstore/workspace/target/surefire-reports/TEST-*.xml'
		}
	}
	