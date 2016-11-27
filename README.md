Connects to your IMAP server and uses [IMAP IDLE](https://tools.ietf.org/html/rfc2177) as a trigger to run your mail syncing code (ie. [mbsync](http://isync.sourceforge.net)).

# Preflight

    sudo apt-get install expect openssl socat

# mbsync

    MaildirStore local,test
    Path ~/Mail/test/
    
    IMAPAccount test
    User me@example.com
    Pass password
    Tunnel "exec socat - $(readlink /proc/$PPID/fd/0)"
    RequireSSL no
    
    IMAPStore test
    Account test
    MapInbox Inbox
    Trash Trash
    
    Channel test
    Master :test:
    Slave :local,test:
    Create Slave
    CopyArrivalDate yes
    Patterns %
    
    Group test
    Channels test:Inbox,Drafts

# Usage

    ./imapidle {tls,ssl} HOSTNAME CHANNEL
