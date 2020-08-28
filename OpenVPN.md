# OpenVPN 3

## Install - debian

1. Update & install https transport

        sudo apt update
        sudo apt upgrade -y 
        sudo apt install apt-transport-https

2. Install the OpenVPN repository key used by the OpenVPN 3 Linux packages 

        wget https://swupdate.openvpn.net/repos/openvpn-repo-pkg-key.pub
        sudo apt-key add openvpn-repo-pkg-key.pub

3. Then you need to install the proper repository. Replace $DISTRO with the release name depending on your Debian/Ubuntu distribution.

        sudo wget -O /etc/apt/sources.list.d/openvpn3.list https://swupdate.openvpn.net/community/openvpn3/repos/openvpn3-$DISTRO.list
          
4. Install openvpn3

        sudo apt update
        sudo apt install openvpn3

5. Import config
    - Easiest way to do this is by opening your .ovpn config file and copying it into vim
    - Or you can use scp/winscp. Whatever you fancy.

            vi vpn_profile.ovpn

6. Start the VPN connection

        openvpn3 session-start --config vpn_profile.ovpn

7. And here are some ideas for bash alias' to make life easier
        
        alias vpn='openvpn3'
        alias vpn-ls='openvpn3 sessions-list'
        alias vpn-pause='openvpn3 session-manage --pause --config'
        alias vpn-resume='openvpn3 session-manage --resume --config'
        alias vpn-start='openvpn3 session-start --config'
        alias vpn-dc='openvpn3 session-manage --disconnect --config'
