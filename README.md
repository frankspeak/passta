# A command-line password manager for OS X #

A few highlights:

1. No additional requirements to run on OS X, other than the ~ 300 line Python script itself.
1. Easy import from comma-separated values (CSV).
1. Completely flexible entry fields; defined by the initially imported CSV headers:
    * By default, the CSV header `Name` is an identifier and `Password` is hidden. 
    * Others can be whatever; no code change required.
1. Passwords are saved to file; better offline than risk a provider [breach](https://blog.lastpass.com/2015/06/lastpass-security-notice.html/).
1. Solid [AES-256](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard) encryption via [OpenSSL](https://www.openssl.org/).
1. CSV data can be dumped to stdout for easy export.
1. Command-line 'magic' to:
    * Perform incremental searches across matches.
    * Rewrite stdout to hide passwords after a keypress (try it out!).


## Getting Started ##

Firstly, download the script, make it executable and easily accessible.  For example:

    #!bash
    ~ $ wget https://bitbucket.org/exemplar/passta/raw/master/passta
    chmod a+x passta
    alias passta="~/passta"

Then, open Terminal and get started.  To see the help...

    #!bash
    usage: passta [-h]
                  [{update,delete,dump,dump-raw,change-password,create-sample}]
                  [name]

Either, get started by generating a sample....

    #!bash
    ~ $ ./passta create-sample  
    Master password for encryption? TopSecretPassword123   
    Confirm Master password for encryption? ********************
    ~/passta.enc encrypted

... or import a raw CSV...

    #!bash
    ~ $ passta
    ~/passta.enc not found.  Path to password CSV? [passta.csv]       
    Master password for encryption? TopSecretPassword123   
    Confirm Master password for encryption? ********************
    ~/passta.enc encrypted

Print an existing record...

    #!bash
    ~ $ ./passta  
    Master password? ********************
    Name? google
    Name=google,URL=https://google.com,User=myaccount@google.com,Password=BigSecret1,Notes=This is a sample google account.
    
Add a new record...

    #!bash
    ~ $ ./passta  
    Master password? ********************
    Name? twitter
    'twitter' not found.  Create it? [yes] y    
    URL? https://www.twitter.com
    User? myaccount@gmail.com
    Password? BigSecret3
    Notes? This is a sample twitter account.
    Save update? [yes] y
    ~/passta.enc encrypted

Print data with hidden fields ('dump-raw' will print all fields for easy export)...

    #!bash
    ~ $ ./passta dump  
    Master password? *******************
    Name=google,URL=https://www.google.com,User=myaccount@gmail.com,Password=**********,Notes=This is a sample google account.
    Name=apple,URL=https://www.apple.com,User=myaccount@gmail,Password=**********,Notes=This is a sample apple account.
    Name=twitter,URL=https://www.twitter.com,User=myaccount@gmail,Password=**********,Notes=This is a sample twitter account.

## Notes ##
* Given that variables in Python loops aren't constrained to that scope, have used the var `tmp` in every case that I don't wish to reuse it later.
