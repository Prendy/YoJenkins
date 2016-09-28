stage('Build') {

  parallel (

      "app" : {

          node('standard') {
            slackSend channel: '#pokerladz', color: 'blue', message: 'PrendyPipe building app on test', teamDomain: 'spartaglobal'
            git 'https://github.com/Prendy/WhatTheDevOps'
            sh 'curl -L https://www.opscode.com/chef/install.sh | sudo bash'
            sh 'curl https://omnitruck.chef.io/install.sh | sudo bash -s -- -P chefdk -c stable -v 0.16.28'
            sh 'sudo hostname andrew.dev'
            sh 'sudo chef-client --local-mode --runlist \'recipe[webserver]\''
            sh 'rm -rf /var/www/html'
            sh 'git clone https://github.com/cleahy3/poker-front /var/www/html'
            slackSend channel: '#pokerladz', color: 'good', message: 'PrendyPipe successfully built app on test', teamDomain: 'spartaglobal'
          }

      },

      "api" : {

          node('standard') {
            slackSend channel: '#pokerladz', color: 'blue', message: 'PrendyPipe building API on test', teamDomain: 'spartaglobal'
            git 'https://github.com/Prendy/WhatTheDevOps'
            sh 'curl -L https://www.opscode.com/chef/install.sh | sudo bash'
            sh 'curl https://omnitruck.chef.io/install.sh | sudo bash -s -- -P chefdk -c stable -v 0.16.28'
            sh 'sudo hostname andrew.dev'
            sh 'sudo chef-client --local-mode --runlist \'recipe[webserver::api]\''
            sh 'rm -rf /var/www/html'
            sh 'git clone -b dev https://github.com/farrakhb/pokerMVC /var/www/html'
            sh 'pm2 start /var/www/html/app.js'
            slackSend channel: '#pokerladz', color: 'good', message: 'PrendyPipe successfully built API on test', teamDomain: 'spartaglobal'
          }

      },

      "db" : {

          node('standard') {
            slackSend channel: '#pokerladz', color: 'blue', message: 'PrendyPipe building DB on test', teamDomain: 'spartaglobal'
            git 'https://github.com/Prendy/WhatTheDevOps'
            sh 'curl -L https://www.opscode.com/chef/install.sh | sudo bash'
            sh 'curl https://omnitruck.chef.io/install.sh | sudo bash -s -- -P chefdk -c stable -v 0.16.28'
            sh 'sudo hostname andrew.dev'
            sh 'sudo chef-client --local-mode --runlist \'recipe[db]\''
            slackSend channel: '#pokerladz', color: 'good', message: 'PrendyPipe successfully built DB on test', teamDomain: 'spartaglobal'
          }

      }


  )

}

stage('Deploy') {

  parallel (

      "app" : {

          node('prendy-app-prod') {

            git 'https://github.com/Prendy/WhatTheDevOps'
            sh 'curl -L https://www.opscode.com/chef/install.sh | sudo bash'
            sh 'curl https://omnitruck.chef.io/install.sh | sudo bash -s -- -P chefdk -c stable -v 0.16.28'
            sh 'sudo hostname andrew.dev'
            sh 'sudo chef-client --local-mode --runlist \'recipe[webserver]\''
            sh 'rm -rf /var/www/html'
            sh 'git clone https://github.com/cleahy3/poker-front /var/www/html'
          }

      },

      "api" : {

          node('prendy-api-prod') {

            git 'https://github.com/Prendy/WhatTheDevOps'
            sh 'curl -L https://www.opscode.com/chef/install.sh | sudo bash'
            sh 'curl https://omnitruck.chef.io/install.sh | sudo bash -s -- -P chefdk -c stable -v 0.16.28'
            sh 'sudo hostname andrew.dev'
            sh 'sudo chef-client --local-mode --runlist \'recipe[webserver::api]\''
            sh 'rm -rf /var/www/html'
            sh 'git clone -b dev https://github.com/farrakhb/pokerMVC /var/www/html'
            sh 'pm2 kill'
            sh 'pm2 start /var/www/html/app.js'

          }

      },

      "db" : {

          node('prendy-db-prod') {

            git 'https://github.com/Prendy/WhatTheDevOps'
            sh 'curl -L https://www.opscode.com/chef/install.sh | sudo bash'
            sh 'curl https://omnitruck.chef.io/install.sh | sudo bash -s -- -P chefdk -c stable -v 0.16.28'
            sh 'sudo hostname andrew.dev'
            sh 'sudo chef-client --local-mode --runlist \'recipe[db]\''
          }

      }


  )

}
