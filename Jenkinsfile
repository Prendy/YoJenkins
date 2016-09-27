stage('Build') {

  node('andrew') {

    git 'https://github.com/Prendy/WhatTheDevOps'
    sh 'curl https://omnitruck.chef.io/install.sh | sudo bash -s -- -P chefdk -c stable -v 0.16.28'
    sh 'pwd'
    sh 'ls -aRl'
    sh 'sudo chef-client --local-mode --runlist \'recipe[webserver]\''
  }
}
