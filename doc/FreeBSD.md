# Build **gendev** for FreeBSD

## Install Dependencies

*Note: This guide is tested for FreeBSD 11.1-RELEASE*

From the root shell, run the following commands:

    pkg install git gmake texinfo gcc openjdk-jre-7.151.01,1 wget

Type 'y' and hit enter to proceed with installing the packages.

Alternatively if you prefer to install from ports you can run the following [which will also install a much lower number of dependencies]:

    portmaster -d devel/git devel/gmake print/texinfo lang/gcc java/openjdk7-jre ftp/wget

Type 'y' and hit enter to proceed with installing the packages.

## Build the toolchain

Next, clone the repository and build the toolchain. [This may take some time to complete]

    git clone https://github.com/kubilus1/gendev.git
    cd gendev
    export MAKE=gmake [or 'setenv MAKE gmake' for csh]
    gmake

The built toolchain and SGDK can now be installed.

## Install Gendev

Gendev is installed to $GENDEV [/opt/gendev] by default. While generally not 100% in line with FreeBSD's hier policy, it doesn't cause any interference so I would recommend using this to maintain compatability.
Make sure that this directory is writable by the user.

Now install to $GENDEV

    gmake install

## Build some sample code [or your project!]

You can test your new installation by building some sample code. This is also useful as a project template.

    export GENDEV=/opt/gendev [or 'setenv GENDEV /opt/gendev' for csh]
    cd ~/  (or some other directory)
    cp -r gendev/sgdk/SGDK/sample/cube_flat ./
    cd cube_flat
    gmake -f $GENDEV/sgdk/mkfiles/makefile.gen clean all

If everything builds correctly, you should end up with a file out/rom.bin with a size of 131072 bytes. You can run this file in an emulator of choice to confirm your builds are functioning correctly. 
