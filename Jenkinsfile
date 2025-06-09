#!/usr/bin/env groovy
import hudson.model.*
import hudson.EnvVars
import groovy.json.JsonSlurper
import groovy.json.JsonBuilder
import groovy.json.JsonOutput
import jenkins.plugins.http_request.*
import java.net.URL


node {
  stage ('Checkout') 
  {
    // Get the code from the Git repository
    checkout scm
  }

  stage('Git to ISPW Synchronization')
  { 
    gitToIspwIntegration app: 'GPLAY', 
    branchMapping: '''*DEV* => DEV1, per-branch,
    *STG1* => STG1, per-branch,
    *QA* => QA, per-branch, 
    *STAG* => STAG, per-branch, 
    *master* => PRD, per-branch''', 
    connectionId: '925c5699-8617-42b8-b43d-409dcc77e122', 
    credentialsId: 'dfb1f0d7-38e2-4b57-a8d7-82df70a7eee7', 
    gitCredentialsId: '1d016276-c36c-414f-95c5-22fa43515542', 
    gitRepoUrl: 'https://github.com/pharvey666/GIT_GPLAY', 
    runtimeConfig: 'ISPP', 
    stream: 'PLAY', 
    subAppl: 'GPLAY'
  }

  stage('Build ISPW assignment')
  {
    ispwOperation connectionId: '925c5699-8617-42b8-b43d-409dcc77e122', 
    credentialsId: 'dfb1f0d7-38e2-4b57-a8d7-82df70a7eee7', 
    ispwAction: 'BuildAssignment', 
    ispwRequestBody: '''buildautomatically=true 
'''
  }
}