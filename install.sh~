#!/bin/bash

# Tested on Debian Squeeze only

FORCERVM="" # force rvm reinstallation if it's not null

DEBPKG_LIST="ruby curl git subversion build-essential libreadline6-dev git-core zlib1g-dev libssl-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt-dev autoconf automake libtool bison"

function rvm_installer() {

bash < <(curl -s https://raw.github.com/wayneeseguin/rvm/master/binscripts/rvm-installer)

}

apt-get install -y $DEBPKG_LIST

if [ ! -d /usr/local/rvm ]
then 
    rvm_installer
else
    [ $FORCERVM ] && rvm_installer
fi

# set rvm for login shells
echo '[[ -s "/usr/local/rvm/scripts/rvm" ]] && . "/usr/local/rvm/scripts/rvm" # Load RVM function' >> /etc/profile.d/source_rvm.sh
chmod +x /etc/profile.d/source_rvm.sh

# set rvm for non login shells
if ! grep -q 'Load RVM function' /etc/bash.bashrc
then
  echo '[[ -s "/usr/local/rvm/scripts/rvm" ]] && . "/usr/local/rvm/scripts/rvm" # Load RVM function' >> /etc/bash.bashrc
fi

# set rvm for this script now wile running 
. /etc/profile.d/source_rvm.sh

rvm requirements 
rvm install 1.9.3
rvm use 1.9.3 --default
ruby -v 

