pipeline {
   agent any
   stages{
      stage('Dependency Check') {
      steps {
        dependencyCheck additionalArguments: "--cveValidForHours 48 --prettyPrint --scan scan_dependencies --format ALL ${fileExists('owasp-suppression.xml') ? '--suppression owasp-suppression.xml' : ''} --disableAssembly", odcInstallation: 'dependency-check 6.5.3'
        dependencyCheckPublisher pattern: '', unstableTotalHigh: 1, unstableTotalCritical: 1
        archiveArtifacts allowEmptyArchive: true, artifacts: '**/dependency-check-report.html', onlyIfSuccessful: false
      }
    }
    stage('Build'){
       steps{
     sh 'mvn clean package '
    }
    }   
  }
}
