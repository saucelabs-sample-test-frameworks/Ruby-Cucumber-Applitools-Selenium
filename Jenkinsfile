node {
    stage 'Checkout'
    git url: 'https://github.com/saucelabs-sample-test-frameworks/Ruby-Cucumber-Applitools-Selenium'

    stage 'Install Dependancies'
    sh 'bundle install --path vendor/bundle'

    stage 'Test'
    docker.image('ruby:2.3.1').inside {
        // Make sure you have a sauce labs credential called 'saucelabs'
        sauce('saucelabs') {
            sauceconnect(useGeneratedTunnelIdentifier: true, verboseLogging: true) {
                // Make sure you have a secret text credential called 'APPLITOOLS_ACCESS_KEY'
                withCredentials([[$class: 'StringBinding', credentialsId: 'APPLITOOLS_ACCESS_KEY', variable: 'APPLITOOLS_ACCESS_KEY']]) {
                    sh 'bundle exec rake test_sauce'
                }
            }
        }
    }

    stage 'Collect Results'
    step([$class: 'SauceOnDemandTestPublisher'])
}
