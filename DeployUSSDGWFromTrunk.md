# Deploy Mobicents USSD Gateway from master #

Below are steps to compile the USSD Gateway from GIT master branch and deploy on latest Mobicents JSLEE Server

  1. Download latest SNAPSHOT JSLEE server from https://hudson.jboss.org/hudson/view/Mobicents/job/Mobicents-Slee-2.x-Release/
  1. GIT clone MAP RA from master branch http://code.google.com/p/jain-slee/source/browse/?repo=ss7#git%2Fresources%2Fmap
  1. GIT clone USSD GW from http://code.google.com/p/ussdgateway/source/checkout
  1. Unzip mobicents-jainslee-2.7.0-SNAPSHOT-jboss-5.1.0.GA.zip
  1. set JBOSS\_HOME environment variable to point to mobicents-jainslee-2.7.0-SNAPSHOT-jboss-5.1.0.GA/jboss-5.1.0.GA
  1. cd to checkedout map ra and call "mvn clean install"
  1. cd to cloned ussdgateway and call "mvn clean install"
  1. copy mobicents-jainslee-2.7.0-SNAPSHOT-jboss-5.1.0.GA/resources/http-client/http-client-ra-DU-2.5.0.FINAL.jar to mobicents-jainslee-2.7.0-SNAPSHOT-jboss-5.1.0.GA/jboss-5.1.0.GA/server/default/deploy
  1. copy mobicents-jainslee-2.7.0-SNAPSHOT-jboss-5.1.0.GA/resources/jdbc/mobicents-slee-ra-jdbc-DU-1.0.0.FINAL.jar to mobicents-jainslee-2.7.0-SNAPSHOT-jboss-5.1.0.GA/jboss-5.1.0.GA/server/default/deploy
  1. cd to mobicents-jainslee-2.7.0-SNAPSHOT-jboss-5.1.0.GA/jboss-5.1.0.GA/bin and start the server "./run.sh -b 127.0.0.1"


## Prepare CLI ##
Above steps will prepare the USSD Gw, however to get the latest Command Line Interface (CLI) working below steps needs to be executed

  1. GIT clone jSS7 from master branch http://code.google.com/p/jss7/source/checkout
  1. set JBOSS\_HOME environment variable to point to mobicents-jainslee-2.7.0-SNAPSHOT-jboss-5.1.0.GA/jboss-5.1.0.GA
  1. cd to checkedout jss7 and call "mvn clean install -Pjboss"
  1. cd to mobicents-jainslee-2.7.0-SNAPSHOT-jboss-5.1.0.GA/jboss-5.1.0.GA/bin and execute ./ss7-cli.sh

Above steps will copy the necessary scripts and jars in jboss-5.1.0.GA for CLI to work