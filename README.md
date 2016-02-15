# A Geek's Password Manager for OS X #

## Highlights ##

1. **No additional requirements**, other than the ~ 300 line Python script itself and a command line.
2. **Simple:**
     * **Import** from comma-separated values (CSV).
     * **Export**, as CSV, to stdout.
3. **Completely flexible CSV 'schema'**; fields are defined by the initially imported CSV headers:
    * By default, the CSV header `Name` is an identifier and `Password` is hidden. 
    * Others can be whatever you choose; no code change required.
4. **Passwords are saved to a local file**.  Better offline than risk a provider [breach](https://blog.lastpass.com/2015/06/lastpass-security-notice.html/).
5. **Solid [AES-256](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard) encryption** via [OpenSSL](https://www.openssl.org/).
6. **Command-line enhancements** to:
    * Perform incremental searches across matches.
    * Rewrite stdout to hide passwords after a keypress (try it out!).

## Getting Started ##

1. Download the script, make it executable and easily accessible:

    ```
    $ wget https://github.com/frankspeak/passta/blob/master/passta
    $ chmod a+x passta
    $ alias passta="~/passta"
    ```
    
    _Optional:_ Set the location for the encrypted password file and a default email in your `~/.profile`:
    
    ```
    export PASSTA_ENC_DIR="~/backed-up"
    export PASSTA_EMAIL="me@mail.com"
    ```
2. Either try out the 'sample.csv' or create a new password CSV (remember the fields themselves are flexible):

    ```
    $ passta -h
    usage: passta [-h]
              [{update,delete,dump,raw,change-password}]
              [name]

    $ passta
    ~/passta.enc not found.  Path to password CSV? [sample.csv]       
    Master password for encryption? TopSecretPassword123   
    Confirm Master password for encryption? ********************
    ~/passta.enc encrypted
    ```
3. Show existing records or add a new one:

    ```
    $ ./passta  
    Master password? ********************
    Name? google
    Name=google,URL=https://google.com,User=myaccount@google.com,Password=BigSecret1,Notes=This is a sample google account.

    $ ./passta edit google  
    Master password? ***
    Edit? [yes] yes
    Name? [google] 
    URL? [https://www.google.com] 
    User? [myaccount@gmail.com] 
    Password? [**********] 
    Notes? [This is a sample google account.] 
    Save update? [yes] 
    ./passta.enc encrypted

    $ ./passta  
    Master password? ********************
    Name? twitter
    'twitter' not found.  Create it? [yes] y    
    URL? https://www.twitter.com
    ...
    ```
4. Export the data; 'dump' will mask hidden fields, 'raw' will print them out for for easy export:

    ```
    $ ./passta dump  
    Master password? *******************
    Name=google,URL=https://www.google.com,User=myaccount@gmail.com,Password=**********,Notes=This is a sample google account.
    Name=apple,URL=https://www.apple.com,User=myaccount@gmail,Password=**********,Notes=This is a sample apple account.
    Name=twitter,URL=https://www.twitter.com,User=myaccount@gmail,Password=**********,Notes=This is a sample twitter account.
    ```
