# Envelope - Publish web apps based on your PostgreSQL database fast!

## Dependencies

#### LIBEV
Different versions of libev may not work with every version of Envelope. To avoid problems, the Envelope compile process is set up to statically compile libev. This way we control what version you use. If you need a different version, start with the dependencies/update.sh file.

#### LIBRESSL
Envelope uses the new TLS API found in LibreSSL. It can take some time to compile LibreSSL. If LibreSSL is already installed on your machine, then the compile process dynamically loads that one. This way you can avoid the wait. If not, it's compiled in statically.

#### LIBPQ
In order for Envelope to talk to PostgreSQL you need to have the libpq library installed.

Mac OS X ships with a PostgreSQL install with no libpq header files. If you then install PostgreSQL but don't add it to your PATH (in .profile) then the Envelope configure process will error saying that it found pg_config (but it will be the wrong one) and fail to find the libpq header files. To fix this situation, make sure you add the proper pgsql/bin folder in the beginning of your path.

Usually, if you have psql then you'll have the libpq library files and be fine. Rarely, you may encounter issues by using the wrong version of libpq. In these cases, or in the case where you want to run envelope on a computer that doesn't have libpq installed, you can consult the file INSTALL_LIBPQ for some OS specific advice on how to get libpq.

####DOWNLOADING THE LATEST VERSION OF ENVELOPE

If you prefer wget:

    wget https://www.workflowproducts.com/downloads/envelope.zip
    unzip envelope.zip

OR if you prefer curl:

    curl -L https://www.workflowproducts.com/downloads/envelope.zip > envelope.zip
    unzip envelope.zip

####INSTALLING ENVELOPE

If you'd like to test Envelope before you install, see the section "Testing Envelope Before Installing" further down.

*`make` will take a while as it builds libressl.*

    cd envelope
    ./configure
    make
    sudo make install

If you are on OpenBSD or FreeBSD, use gmake instead.
Envelope will be installed in `/usr/local/sbin`. All other files such as the html, javascript and configuration files will be installed to `/usr/local/etc/envelope`.

####RUNNING ENVELOPE

To run Envelope:

    /usr/local/sbin/envelope

Long version:

    /usr/local/sbin/envelope \
    -c /usr/local/etc/envelope/envelope.conf \
    -d /usr/local/etc/envelope/envelope-connections.conf

####Configuring ENVELOPE

Before running Envelope for the first time you may want to configure some options. All the options are explained in the Envelope man file:

    man envelope

Current configuration options allow you to set various paths, various access restrictions, web port and log level. Note that in order to make Envelope publish to HTTPS, you need to add paths for a TLS cert and key.

You'll also need to set up a connection string to tell Envelope where your PostgreSQL database is published. The default connection string config file located in /usr/local/etc/envelope/. There are examples in the provided envelope-connections.conf file and further info is available in the man file.

####TESTING ENVELOPE BEFORE INSTALLING

    cd envelope
    ./configure
    make
    nano config/envelope-connections.conf
    make test

If you want to test Envelope before you install, edit the `config/envelope-connections.conf` file to add a connection string for your Postgres database. Instructions for adding a connection string are included in the Envelope man page. To look at the Envelope man page before installing Envelope:

    ./configure
    man -M man envelope

By default Envelope runs on port 8080, so if you need to change that you do it in the `envelope.conf` file. You can also set other options like whether to use TLS to connect.

Once you've added a connection string to the envelope-connections.conf file, start the Envelope server with:

    make test

Envelope will push a message like:

    Open http(s)://<this computer's ip>:8080/ in your web browser

Once you see that message that means Envelope is running, open your web browser to the link shown.

####UNINSTALLING ENVELOPE

If you still have your original build directory then:

    cd envelope
    ./configure
    make uninstall

If you don't have your original build directory check the following locations:

*Warning*
    
    The /usr/local/etc/envelope folder contains app/, role/, web_root/ and your config files. Make sure you have backups before you remove these folders. If you've made apps or altered your website then back up these folders before removing envelope. 
    
    rm -r /usr/local/etc/envelope
    rm /usr/local/sbin/envelope             # this removes the binary
    rm /usr/local/man/man1/envelope.1       # this removes the man page
    
####FEEDBACK AND BUG REPORTS

Please contact us with your feedback! Please report any issues you have for FREE support. More information is available at the project home page: https://www.workflowproducts.com/envelope.html

####Licensing

If you like some or all of Envelope's functionality and the current license won't suit your needs, commercial licensing is available starting at $99. Please call Justin at Workflow Products, 817-503-9545 for details.

Copyright 2016 Workflow Products LLC
