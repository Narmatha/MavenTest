node('master') {

	def MVNHOME = tool 'Maven'
	def ANSIBLE = tool 'ansible'
	
stage ('checkout code'){
	checkout scm
}
	
stage ('build'){
	sh "${MVNHOME}/bin/mvn clean install"
}

stage ('Test Cases Execution'){
	sh "${MVNHOME}/bin/mvn clean org.jacoco:jacoco-maven-plugin:prepare-agent install -Pcoverage-per-test"
}
	
stage ('Integration Test'){
	sh ""
}

stage ('Sonar Analysis'){
	//sh '${MVNHOME}/bin/mvn sonar:sonar -Dsonar.host.url=http://localhost:9000/sonar'
}
	
stage('Code Coverage ') {
    //sh "curl -o coverage.json 'http://35.154.151.174:9000/sonar/api/measures/component?componentKey=com.java.example:java-example&metricKeys=coverage';sonarCoverage=`jq '.component.measures[].value' coverage.json`;if [ 1 -eq '\$(echo '\${sonarCoverage} >= 50'| bc)' ]; then echo 'Failed' ;exit 1;else echo 'Passed'; fi"
   }

stage ('Archive Artifacts'){
	archiveArtifacts artifacts: 'target/*.war'
}

//input message: "QA Team Approval for Production Deployment?"

stage ('Production Deployment'){
    sh 'echo ${MVNHOME}'
    sh 'echo ${ANSIBLE}'
 	sh '/usr/local/bin/ansible-playbook deploy.yml -i inventory.ini'
}
}
