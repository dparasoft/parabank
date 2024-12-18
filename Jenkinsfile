pipeline {
    agent any
    environment {
        // Parasoft Jtest Settings
        jtestCWEConfig="builtin://CWE Top 25 2023"
        jtestOWASPConfig="builtin://OWASP Top 10-2021"
        jtestFlowAnalysisConfig="builtin://Flow Analysis Standard"
        jtestPCIConfig="builtin://PCI DSS 4.0"
        jtestUnitTestConfig="builtin://Unit Tests"
    }
    stages {
        stage('Setup') {
            steps {
                deleteDir()                               
                // setup additional environment              
                // setup the workspace
                // Clone this repository & Parabank repository into the workspace
                bat  '''          
                    git clone https://github.com/dparasoft/parabank.git && cd parabank && ls -ll
                    '''
                // Prepare the jtestcli.properties file

                // Setup soatestcli.properties file
            }
        }
        stage('Jtest: Quality Scan - SA') {
            when { equals expected: true, actual: true }
            steps {
                // Execute the scan with Jtest for Static Analysis using Flow based
                bat '''
                    cd parabank && mvn -ntp compile jtest:jtest -Djtest.config="${jtestFlowAnalysisConfig}"
                    '''
            }
        }
        stage('Jtest: Quality Scan - (SAST) OWASP Top 10') {
            when { equals expected: true, actual: true }
            steps {
                // Execute the scan with Jtest for SAST - OWASP 
                bat '''
                    cd parabank && mvn -ntp compile jtest:jtest -Djtest.config="${jtestOWASPConfig}"
                    '''
            }
        }
        stage('Jtest: Quality Scan - (SAST) CWE') {
            when { equals expected: true, actual: true }
            steps {
                // Execute the scan with Jtest for SAST - CWE
                bat '''
                    cd parabank && mvn -ntp compile jtest:jtest -Djtest.config="${jtestCWEConfig}"
                    '''
            }
        }
        stage('Jtest: Quality Scan - (SAST) PCI DSS') {
            when { equals expected: true, actual: true }
            steps {
                // Execute the scan with Jtest for SAST - PCI
                bat '''
                    cd parabank && mvn -ntp compile jtest:jtest -Djtest.config="${jtestPCIConfig}"
                    '''
            }
        }
        stage('Jtest: Unit Test') {
            when { equals expected: true, actual: true }
            steps {
                // Execute the scan with Jtest for SAST - Unit Testing
                bat '''
                    cd parabank && mvn -ntp compile jtest:agent test jtest:jtest -Djtest.config="${jtestUnitTestConfig}" -Dmaven.test.failure.ignore=true
                    '''
            }
        }
    }
}
