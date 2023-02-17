pipeline {
    agent none // agent is defined per stage

    stages {
        stage ('BTC Unit Test') {
            // make sure that this stage runs on an agent with the required software
            // - BTC EmbeddedPlatform incl. JenkinsAutomation plugin
            agent { label 'my_btc_agent' }

            steps {
                // Tests with BTC EmbeddedPlatform
                script {
                    // start BTC EmbeddedPlatform on Agent
                    btc.startup {}
                    
                    // BTC: load & update test project (*.epp)
                    // - relative paths from workspace / pwd to files
                    btc.profileLoad {
                        profilePath = "tst/TestProject.epp"
                        compilerShortName = "MinGW64"
                        updateRequired = true
                    }

                    // Run tests
                    btc.rbtExecution {}
                
                    // BTC: close EmbeddedPlatform and store reports
                    btc.wrapUp {}
                }
            }
        }
    }

}   
