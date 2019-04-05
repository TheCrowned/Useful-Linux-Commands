# Useful-Linux-Commands
A random selection of useful Linux commands for a variety of tasks.

* To renew certbot Let's Encrypt certificate:

   sudo ./certbot-auto --expand -d domain1.com domain2.com

* To bulk rename files, changing extension case:

   for file in *.jpg; do 
    mv "$file" "(basename "$file".jpg).JPG"; done

* To sync files in two folders:

   rsync --recursive -azPv --delete source/* /path/to/target

   where a is for archive and z to compress

* To mount an SSH resource as local drive:

   sshfs user@host:/remote/path /local/path -p port_number -o IdentityFile=~/.ssh/id_rsa_custom

* To rename (CR2) image files basing on EXIF info:

   exiftool -progress -r -d "%Y-%m-%d %H-%M-%S%%-c -%%f.%%e" "-filename<DateTime Original" -ext CR2 .

   (replace *-filename* with *-testname* for a dry run)

* To run individual PHPUnit tests:

   phpunit --filter methodName className path/to/file.php

   to run all tests, just run *phpunit*

**Imagemagick**
* To resize, compress and rename all jpg files in a folder appending *_tn*:

   convert "source/*.jpg" -quality 50 -monitor -debug cache -resize "150x150>" -set filename:area "%t_tn" "target/%[filename:area].jpg"

* To compress alone:

   mogrify -path "target" -quality 80 -format JPG "source/*.jpg"
