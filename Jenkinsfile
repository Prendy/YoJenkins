stage('Build') {

  parallel (

      "app" : {

          node('standard') {
            print "this should print = ${Perform_build_phase}"
            if('${Perform_build_phase}' == 'true')
            print "its true"
            else
            print "its false!!"


            slackSend channel: '#pokerladz', color: 'blue', message: 'PrendyPipe building app on test', teamDomain: 'spartaglobal'
            git 'https://github.com/Prendy/WhatTheDevOps'
            sh 'sudo hostname andrew.dev'
            sh 'sudo chef-client --local-mode --runlist \'recipe[webserver]\''
            sh 'rm -rf /var/www/html'
            sh 'git clone -b master https://github.com/cleahy3/poker-front /var/www/html'
            slackSend channel: '#pokerladz', color: 'good', message: 'PrendyPipe successfully built app on test', teamDomain: 'spartaglobal'
            sh 'rm -rf Poker-Automation-Tests'
            sh 'git clone https://github.com/johnmetcalfe/Poker-Automation-Tests'

            dir ('/root/Poker-Automation-Tests') {

            sh 'sudo apt-get update'
            sh 'sudo apt-get -f -y install'
            sh 'sudo apt-get install -y libxss1 libappindicator1 libindicator7 libasound2 libgconf-2-4 libpango1.0-0 fonts-liberation libcurl3 xdg-utils'
            sh 'wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb'
            sh 'set +e && sudo dpkg -i google-chrome*.deb && set -e'
            sh 'sudo apt-get install -f'
            sh 'sudo apt-get install -y xvfb'
            sh 'sudo apt-get install -y unzip'
            sh 'wget -N http://chromedriver.storage.googleapis.com/2.20/chromedriver_linux64.zip'
            sh 'unzip chromedriver_linux64.zip'
            sh 'chmod +x chromedriver'
            sh 'sudo mv -f chromedriver /usr/local/share/chromedriver'
            // sh 'sudo ln -s /usr/local/share/chromedriver /usr/local/bin/chromedriver'
            // sh 'sudo ln -s /usr/local/share/chromedriver /usr/bin/chromedriver'
            sh 'sudo apt-get install -y python-pip'
            sh 'pip install pyvirtualdisplay selenium'
            }
            sh 'rspec ./Poker-Automation-Tests/'

          }

      },

      "api" : {

          node('standard') {
            slackSend channel: '#pokerladz', color: 'blue', message: 'PrendyPipe building API on test', teamDomain: 'spartaglobal'
            git 'https://github.com/Prendy/WhatTheDevOps'
            sh 'sudo hostname andrew.dev'
            sh 'sudo chef-client --local-mode --runlist \'recipe[webserver::api]\''
            sh 'rm -rf /var/www/html'
            sh 'git clone https://github.com/farrakhb/pokerMVC /var/www/html'
            sh 'pm2 kill'
            sh 'npm install --prefix /var/www/html/'
            sh 'pm2 start /var/www/html/app.js'
            slackSend channel: '#pokerladz', color: 'good', message: 'PrendyPipe successfully built API on test', teamDomain: 'spartaglobal'
          }

      },

      "db" : {

          node('standard') {
            slackSend channel: '#pokerladz', color: 'blue', message: 'PrendyPipe building DB on test', teamDomain: 'spartaglobal'
            git 'https://github.com/Prendy/WhatTheDevOps'
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
            slackSend channel: '#pokerladz', color: 'blue', message: 'PrendyPipe deploying app', teamDomain: 'spartaglobal'
            git 'https://github.com/Prendy/WhatTheDevOps'
            sh 'sudo hostname andrew.dev'
            sh 'sudo chef-client --local-mode --runlist \'recipe[webserver]\''
            sh 'rm -rf /var/www/html'
            sh 'git clone -b master https://github.com/cleahy3/poker-front /var/www/html'
            sh 'pm2 kill'
            sh 'npm install --prefix /var/www/html/'
            sh 'pm2 start /var/www/html/index.js'
            slackSend channel: '#pokerladz', color: 'good', message: 'PrendyPipe successfully deployed app', teamDomain: 'spartaglobal'
          }

      },

      "api" : {

          node('prendy-api-prod') {
            slackSend channel: '#pokerladz', color: 'blue', message: 'PrendyPipe deploying API', teamDomain: 'spartaglobal'
            git 'https://github.com/Prendy/WhatTheDevOps'
            sh 'sudo hostname andrew.dev'
            sh 'sudo chef-client --local-mode --runlist \'recipe[webserver::api]\''
            sh 'rm -rf /var/www/html'
            sh 'git clone https://github.com/farrakhb/pokerMVC /var/www/html'
            sh 'pm2 kill'
            sh 'npm install --prefix /var/www/html/'
            sh 'pm2 start /var/www/html/app.js'
            slackSend channel: '#pokerladz', color: 'good', message: 'PrendyPipe successfully deployed API', teamDomain: 'spartaglobal'
          }

      },

      "db" : {

          node('prendy-db-prod') {
            slackSend channel: '#pokerladz', color: 'blue', message: 'PrendyPipe deploying DB', teamDomain: 'spartaglobal'
            git 'https://github.com/Prendy/WhatTheDevOps'
            sh 'sudo hostname andrew.dev'
            sh 'sudo chef-client --local-mode --runlist \'recipe[db]\''
            slackSend channel: '#pokerladz', color: 'good', message: 'PrendyPipe successfully deployed DB', teamDomain: 'spartaglobal'
          }

      }


  )

}
