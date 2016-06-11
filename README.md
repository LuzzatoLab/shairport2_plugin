shairport2_plugin
================

ShairPort2 Plugin for Squeezebox Server adds airTunes support for each Squeezebox server client.

To install the plugin first - then install the dependancies:

Linux:

    > apt-get install libcrypt-openssl-rsa-perl libio-socket-inet6-perl libwww-perl avahi-utils libio-socket-ssl-perl
    > wget http://www.inf.udec.cl/~diegocaro/rpi/libnet-sdp-perl_0.07-1_all.deb
    > dpkg -i libnet-sdp-perl_0.07-1_all.deb

OSX:

    > sudo /usr/bin/perl -MCPAN -e'install Crypt::OpenSSL::RSA'
    > sudo /usr/bin/perl -MCPAN -e'install IO::Socket::INET6'
    > sudo /usr/bin/perl -MCPAN -e'install Net::SDP'


Now open the LMS GUI; click on Settings, then select the Plugins tab, at the bottom of the page add the repo:

http://raw.github.com/luzzatolab/shairport2_plugin/master/public.xml

Next install the plugin and enable as usual.

This version does not need a helper app in the global fs. It automatically detects the os and uses
the local helper.
  
Ensure avahi-daemon is configured correctly. edit the file /etc/avahi/avahi-daemon.conf:

    [server]
    use-ipv4=yes
    use-ipv6=yes
    
    [wide-area]
    enable-wide-area=yes
    
    [publish]
    publish-aaaa-on-ipv4=no
    publish-a-on-ipv6=no
    
    [reflector]
    
    [rlimits]
    rlimit-core=0
    rlimit-data=4194304
    rlimit-fsize=0
    rlimit-nofile=300
    rlimit-stack=4194304
    rlimit-nproc=3
  
Then restart avahi-daemon and LMS to apply all settings.

== THANKS ==

DMSTK - for doing the intial work and starting this great project
stuartUSA - for bringing it to the masses
chincheta0815 - for the OS autodetect and base work on metadata/covers

== Additional Notes ==

This version has been midified from the Disaster123 version to allow synching of video and audio when using airplay. As such the START_FILL variable in hairtunes.c was changed to 205 (instead of 64).
For quick testing, the executable shairtunes_helper from the src folder can be copied to cp shairport_helper /var/lib/squeezeboxserver/cache/InstalledPlugins/Plugins/ShairTunes2/helperBinaries/shairport_helper-x64-linux after compiles (executable destination name will be different based on sys type)
