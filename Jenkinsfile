pipeline {
  agent any
  stages {
    stage('Test') {
      steps {
        sh 'echo \'test\''
      }
    }
    stage('fortify scan'){
      steps {
        fortifyClean addJVMOptions: '', buildID: '${JOB_NAME}-${BUILD_NUMBER}', debug: true, logFile: '', maxHeap: '1000', verbose: true
        sh 'ls'
        fortifyTranslate addJVMOptions: '', buildID: '${JOB_NAME}-${BUILD_NUMBER}', excludeList: '', logFile: './${JOB_NAME}-${BUILD_NUMBER}-translation.log', maxHeap: '1000', projectScanType: fortifyJava(javaAddOptions: '', javaClasspath: '', javaSrcFiles: '"./WebGoat/*.java"', javaVersion: '1.8')
        fortifyScan addJVMOptions: '-64', addOptions: '', buildID: '${JOB_NAME}-${BUILD_NUMBER}', customRulepacks: '', logFile: './${JOB_NAME}-${BUILD_NUMBER}-scan.log', maxHeap: '1000', resultsFile: '${JOB_NAME}-${BUILD_NUMBER}-results.fpr'
        fortifyUpload appName: 'Demo', appVersion: 'Rel13', failureCriteria: '[fortify priority order]:critical OR high', filterSet: '', pollingInterval: '', resultsFile: ''
        //Generate pdf report from fpr report
        sh 'pwd'
        //sh '/tools/fortify/bin/BIRTReportGenerator -template "Developer Workbook" -source ${JOB_NAME}-${BUILD_NUMBER}-results.fpr -output ${JOB_NAME}-${BUILD_NUMBER}-results.pdf -format PDF -showSuppressed -UseFortifyPriorityOrder'
      }
    }
  }
}
