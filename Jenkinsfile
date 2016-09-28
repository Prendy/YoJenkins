stage('Build') {

  parallel() {

      "app" : {

          node('andrew') {

            git 'https://github.com/Prendy/WhatTheDevOps'
            sh 'curl -L https://www.opscode.com/chef/install.sh | sudo bash'
            sh 'curl https://omnitruck.chef.io/install.sh | sudo bash -s -- -P chefdk -c stable -v 0.16.28'
            //sh 'chef-apply cookbooks/webserver/recipes/default.rb'
            sh 'sudo hostname andrew.dev'
            sh 'sudo chef-client --local-mode --runlist \'recipe[webserver]\''
            sh 'git clone https://github.com/cleahy3/poker-front /var/www/html'
            sh 'cat /var/www/html/index.html'
          }

      },
      "api" : {

          node('andrew') {

            git 'https://github.com/Prendy/WhatTheDevOps'
            sh 'curl -L https://www.opscode.com/chef/install.sh | sudo bash'
            sh 'curl https://omnitruck.chef.io/install.sh | sudo bash -s -- -P chefdk -c stable -v 0.16.28'
            //sh 'chef-apply cookbooks/webserver/recipes/default.rb'
            sh 'sudo hostname andrew.dev'
            sh 'sudo chef-client --local-mode --runlist \'recipe[webserver]\''
            sh 'git clone https://github.com/cleahy3/poker-front /var/www/html'
            sh 'cat /var/www/html/index.html'
          }

      }


  }

}
