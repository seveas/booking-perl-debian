Booking-perl for Debian
-----------------------
This is a port of our internal rpm packaging to Debian, but only for perl
itself, not any CPAN packages. After building and installing this package,
you have a working perl and cpanm in /usr/local/booking-perl/ and symlinks to
perl and cpanm in /usr/local/bin.

It differs from the normal version of Perl shipped by Debian in a few ways:

- No local patches, this is vanilla perl
- No split package, all is contained in the booking-perl5241 package
- Our own ./Configure` arguments
- Installed into /usr/local/booking-perl/5.24.1 instead of /usr
- You can have multiple perl versions installed at the same time, the default
  (the one that symlinks in /usr/local/bin point to) can be set with
  update-alternatives

How to build this package
-------------------------
This will build booking-perl5241, which corresponds to a vanilla Perl 5.24.1

- Get perl itself and extract it

    ```
    wget http://www.cpan.org/src/5.0/perl-5.24.1.tar.gz \
        -O booking-perl5241_5.24.1.orig.tar.gz
    tar xf booking-perl5241_5.24.1.orig.tar.gz
    ```

- Get the packaging

    ```
    cd perl-5.24.1
    wget -O- https://github.com/seveas/booking-perl-debian/archive/perl-5.24.1.tar.gz \
        | tar --xform 's!.*/!debian/!' -xz
    ```

- Build a source package, don't try to sign it

    `debuild -S -us -uc`

- Set up pbuilder if you have not done so yet

    ```
    sudo apt-get install pbuilder
    sudo pbuilder create
    ```

- Build a binary package.

    `sudo pbuilder build ../booking-perl5241_5.24.1-1.dsc`

- The binary package can now be found in /var/cache/pbuilder/result
