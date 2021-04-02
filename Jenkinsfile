#!/usr/bin/env groovy
import hudson.model.*
import hudson.EnvVars
import groovy.json.JsonSlurper
import groovy.json.JsonBuilder
import groovy.json.JsonOutput
import java.net.URL

String ISPW_Application     = "JERY"        // Change to your assigned application
String HCI_Token            = "ee59da9e-49c1-47ec-85c3-9460ae490023"     // Change to your assigned ID

node {
  stage ('Checkout')
  {
    // Get the code from the Git repository
    checkout scm
  }

  stage('Git to ISPW Synchronization')
  {
    gitToIspwIntegration app: "${ISPW_Application}",
    branchMapping: '''*master* => QA, per-branch'
    bug* => HLD, per-branch
    feature1* => STG1, per-branch
    feature2* => STG2, per-branch''',
    //connectionId: '38e854b0-f7d3-4a8f-bf31-2d8bfac3dbd4', // CWC2
    connectionId: 'f0ede0d7-9b8d-497a-a20b-b9a2d7f08469', // TD-CW13
    credentialsId: "${HCI_Token}",
    gitCredentialsId: '8308db3f-3bed-453f-b569-05db1cde895c', // ispw-fts
    gitRepoUrl: 'https://github.com/ispw-fts/GitFTS.git',
    //runtimeConfig: 'isp8', // CWC2
    runtimeConfig: 'tpzp', // CW13
    stream: 'TOPAZ'
  }

 

  stage('Deploy to Testing')
  {
    sleep(7)
    println "Deploy successfull!"
  }

  stage('Run TTT Tests')
  {
    sleep(10)
    println "TTT Tests successfull!"
  }

  stage('Retrieve Code Coverage')
  {
    sleep(5)
    println "Retrieve code successfull!"
  }

  stage('Run Sonar Analysis')
  {
    sleep(12)
    println "Sonar analysis successfull!"
  }


}
