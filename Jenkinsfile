node {
    def mvnHome 
    
    // Mark the code checkout 'stage'....
    stage 'Checkout'
    // Get some code from a GitHub repository
    git url: 'https://github.com/saucelabs-sample-test-frameworks/Java-Junit-Selenium.git'
    mvnHome = tool 'M3'
    stage 'Compile'
    bat "${mvnHome}/bin/mvn compile"
    stage 'Test'
    sauce('sauce-labs') {
        sauceconnect(useGeneratedTunnelIdentifier: true, verboseLogging: true) {
            bat "${mvnHome}/bin/mvn test"
        }
    }
    stage 'Collect Results'
    step([$class: 'JUnitResultArchiver', testResults: '**/target/surefire-reports/TEST-*.xml'])
    step([$class: 'SauceOnDemandTestPublisher'])
}
post {
    always {
        junit '**/surefire-reports/*.xml'
    }
}
