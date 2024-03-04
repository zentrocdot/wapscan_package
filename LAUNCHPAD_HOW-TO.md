# Launchpad How-To

<p align="justify">Building a package for <code>Launchpad</code> is a little bit different form building a DEB package for personal use. There are a few more rules to follow.</p>

<p align="justify">I am using the structure which I presented in the other  <a href="https://github.com/zentrocdot/wapscan_package/blob/main/HOW-TO.md">How-To<a>

# Preparation 

<p align="justify">Delete all package related files in the parent folder.</p>

    ~/USR_DEB

<p align="justify">First re-creating the tree structure from within the package directory e.g.</p>

    ~/USR_DEB/wapscan-0.0.0.2-all

# Prepare Files

<p align="justify">We have to make some modifications in debian/control and debian/changelog:</p>  

    wapscan (0.0.0.2-all) UNRELEASED; urgency=medium    # Results in a rejected package   

    wapscan (0.0.0.2-all) jammy; urgency=medium

 <p align="justify">A package which has UNRELEASED in the changlog file will be rejected.</p>   

 <p align="justify">The file control has also to be changed.</p>  

    Section: unknown    # Results in a rejected package   

    Section: utils

Allowed are:

admin, cli-mono, comm, database, debug, devel, doc, editors, education, electronics, embedded, fonts, games, gnome, gnu-r, gnustep, graphics, hamradio, haskell, httpd, interpreters, introspection, java, javascript, kde, kernel, libdevel, libs, lisp, localization, mail, math, metapackages, misc, net, news, ocaml, oldlibs, otherosfs, perl, php, python, ruby, rust, science, shells, sound, tasks, tex, text, utils, vcs, video, web, x11, xfce, zope

# Create Package for Distribution

<p align="justify">using the command dh_make:</p>  

    dh_make -y --indep --createorig

<p align="justify">Thean use debuild.</p>  

    debuild -S -sa    # New from scratch

    debuild -S -sd    # Difference build

<p align="justify">Ignore the signing error.</p>  

<p align="justify">Change to the parent directory.</p> 

    debsign -k <key-ID> wapscan_0.0.0.1-all-1_source.changes

<p align="justify">Afterwards the package can be uploaded.</p> 

    dput ppa:zentrocdot/wapscan-cli-ppa wapscan_0.0.0.1-all-1_source.changes

<p align="justify">If one makes changes, fore upload.</p> 

    dput --force ppa:zentrocdot/wapscan-cli-ppa wapscan_0.0.0.1-all-1_source.changes

# Passwords & Encryption Keys Application

<p align="justify">The passwords & encryption keys application name is unusually seahorse.</p> 

    sudo apt-get install seahorse

# Getting the KEY ID

    gpg2 --list-keys --keyid-format LONG

# References

[1]   askubuntu.com/questions/1087569/deploying-own-debian-package-to-launchpad

[2]   askubuntu.com/questions/140803/steps-for-creating-a-slightly-modified-package-and-uploading-it-in-a-ppa

[3]    askubuntu.com/questions/1012403/how-to-upload-build-a-custom-kernel-on-launchpad

[4]    help.launchpad.net/YourAccount/CreatingAnSSHKeyPair

[5]    help.launchpad.net/Packaging/PPA/BuildingASourcePackage

[6]    help.launchpad.net/Packaging/PPA/Uploading

[7]    help.launchpad.net/ReadingOpenPgpMail

[8]    help.launchpad.net/Packaging/UploadErrors

[9]    help.ubuntu.com/community/GnuPrivacyGuardHowto

[10]   launchpad.net/~zentrocdot/+archive/ubuntu/wapscan-cli-ppa

[11]    stackoverflow.com/questions/43699845/error-uploading-files-for-distribution-unreleased-to-ppa-not-allowed

[12]    stackoverflow.com/questions/50089033/how-do-i-get-the-changes-file-for-a-debian-package

[13]    stackoverflow.com/questions/46879602/get-fingerprints-of-openpgp-keys

[14]    wiki.ubuntuusers.de/GnuPG/

[15]    www&#8203;.debian.org/doc/debian-policy/ch-controlfields.html

[16]    askubuntu.com/questions/226495/how-to-solve-dpkg-source-source-problem-when-building-a-package