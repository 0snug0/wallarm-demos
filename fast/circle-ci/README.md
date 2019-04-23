[![CircleCI](https://circleci.com/gh/0snug0/wallarm-demos/tree/master.svg?style=svg)](https://circleci.com/gh/0snug0/wallarm-demos/tree/master)

# Wallarm FAST Demo for Circle-CI
A Circle CI demo with a Wallarm FAST proxy running 1000's of security test

## Demo Components
### DVWA
[Damn Vulnerable Web App](https://hub.docker.com/r/vulnerables/web-dvwa/)

Damn Vulnerable Web Application (DVWA) is a PHP/MySQL web application that is damn vulnerable. Its main goal is to be an aid for security professionals to test their skills and tools in a legal environment, help web developers better understand the processes of securing web applications and to aid both students & teachers to learn about web application security in a controlled class room environment. Read more [here](https://hub.docker.com/r/vulnerables/web-dvwa/).

### Wallarm FAST 
[Framework for Automated Security Testing](https://hub.docker.com/r/wallarm/fast/)
Wallarm Framework for Application Security Testing (FAST) - get a huge increase in security test coverage without spending a lot of time. FAST uses fuzzer and known security payload library to automatically create and run 1000X security tests for every functional test. Read more [here](https://hub.docker.com/r/wallarm/fast/)

### Selenium
#### Selenium Hub
[Selenium Hub](https://github.com/SeleniumHQ/docker-selenium)
The Hub receives a test to be executed along with information on which browser and 'platform' where the test should be run. The hub will use this information and delegate to a node that can service those needs. Read more [here](https://github.com/SeleniumHQ/docker-selenium/tree/master/Hub)

#### Selenium Nodes
[Selenium Node](https://github.com/SeleniumHQ/docker-selenium/tree/master/NodeBase)
Selenium automates browsers. That's it! What you do with that power is entirely up to you. Primarily, it is for automating web applications for testing purposes, but is certainly not limited to just that. Boring web-based administration tasks can (and should!) also be automated as well. Read more [here](https://github.com/SeleniumHQ/docker-selenium/tree/master/NodeBase)
```
kubectl run selenium-hub --image selenium/hub:3.10.0 --port 4444
kubectl run selenium-node-chrome --image selenium/node-chrome:3.10.0 --env="HUB_PORT_4444_TCP_ADDR=selenium-hub" --env="HUB_PORT_4444_TCP_PORT=4444"
kubectl run selenium-node-firefox --image selenium/node-firefox:3.10.0 --env="HUB_PORT_4444_TCP_ADDR=selenium-hub" --env="HUB_PORT_4444_TCP_PORT=4444"
kubectl expose deployment selenium-hub --type=NodePort
kubectl port-forward deploy/selenium-hub 4444:4444
kubectl expose deployment selenium-hub --type=LoadBalancer --name selenium-hub-external
```