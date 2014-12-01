#Assumptions
- Loggregator is deployed and its traffic controller job has the allowAllAccess flag set to true. 
  Currently master of Loggregator supports this flag, but the version in cf-release is behind.  
- Diego-release is deployed
    
#Setup

     go get github.com/pivotal-cf-experimental/whetstone
     go get github.com/pivotal-cf-experimental/diego-edge-cli
     go get -v -t ./...

     go get github.com/onsi/ginkgo/ginkgo
     go get github.com/onsi/gomega


#Running The Whetstone Tests

For example, to Run Tests against Bosh Lite deployed Diego Release and Loggregator with a 30 sec app start timeout:
     
     ginkgo -- -domain="10.244.0.34.xip.io" -timeout=30

To run against [Diego Edge](https://github.com/pivotal-cf-experimental/diego-edge)

    ginkgo -- -domain="192.168.11.11.xip.io" -timeout=30
   

#Notes on Running against Bosh Lite:
  Cloudfoundry reccomends using xip.io with Bosh lite for DNS.
  This has been very flaky for us, resulting in no such host errors.
  The alternative that we have found is to use dnsmasq configured to resolve all xip.io addresses to the ip of the HA proxy.
  This also requires creating a /etc/resolvers/io file that points to 127.0.0.1. See further instructions [here] (http://passingcuriosity.com/2013/dnsmasq-dev-osx/). 
