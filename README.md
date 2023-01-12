Docker-Container of php8 and apache
========================================================================



Required variables in .env:
------------------------------------------------------------------------

    :::text
    HOSTNAME=localhost.direct
    UID=1234
    GID=1234

- The hostname should work fine. This is a public DNS with a root
  certificate that points back to 127.0.0.1 .
- The UID and GID are your user- and group-id.
    - Get your user-id like this: `id -u` and your group-id like that: `id -g`.
- Adjust the data!



Example docker-compose.yml
------------------------------------------------------------------------

    :::yaml
    version: "3"
    services:
        application:
            build: .../php7
            env_file: .env
            ports:
                - "80:80"
                - "443:443"
            volumes:
                - ./html:/srv
                - ./etc/custom-php.ini:/etc/php8/conf.d/custom-php.ini
                - ./etc/custom-apache.conf:/etc/apache2/conf.d/custom-apache.conf
                - ./etc/vhosts.d/:/etc/apache2/conf.d/vhosts.d/

- Update the path to the build directory.
- Copy and edit the content of the etc/ directory.



SSL-Certificates
------------------------------------------------------------------------

Copy the content of the html directory (a shell file and a certificate)
to your html directory. Restart the container.



Virtual Hosts
------------------------------------------------------------------------

See the etc/vhosts.d/ directory for examples on how to create virtual hosts.
You may also use the tools/new-vhost script to create a new one.

