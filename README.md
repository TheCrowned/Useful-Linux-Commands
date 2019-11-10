# Useful-Linux-Commands
A random selection of useful Linux commands for a variety of tasks.

* To renew certbot Let's Encrypt certificate:

   sudo ./certbot-auto --expand -d domain1.com domain2.com

* To bulk rename files, changing extension case:

   for file in *.jpg; do 
    mv "$file" "(basename "$file".jpg).JPG"; done

* To sync files in two folders:

   rsync --recursive -azPv --delete source/* /path/to/target

   where a is for archive, z to compress, P for progress and v for verbose. Include --dry-run for dry run; --ignore-existing to only copy new files (on remote shares permissions may be different and all already present files may be copied over every time because seen as different).

* To mount an SSH resource as local drive:

   sshfs user@host:/remote/path /local/path -p port_number -o IdentityFile=~/.ssh/id_rsa_custom

* To rename (CR2) image files basing on EXIF info:

   exiftool -progress -r -d "%Y-%m-%d %H-%M-%S%%-c - %%f.%%e" "-filename<DateTimeOriginal" -ext CR2 .

   (replace *-filename* with *-testname* for a dry run)

* To run individual PHPUnit tests:

   phpunit --filter methodName className path/to/file.php

   to run all tests, just run *phpunit*

* To enable/disable/see status startup of service

   sudo systemctl enable btsync.service
   sudo systemctl disable btsync.service
   sudo systemctl status btsync.service

* To handle torrents
   service transmission-deamon stop
   transmission-deamon --noauth
   transmission-deamon -a "MAGNETURI"
   transmission-daemon -l   #shows status
   transmission-daemon -t 1 -r   #removes torrent N.1

**Imagemagick**
* To resize, compress and rename all jpg files in a folder appending *_tn*:

   convert "source/*.jpg" -quality 50 -monitor -debug cache -resize "150x150>" -set filename:area "%t_tn" "target/%[filename:area].jpg"

* To compress alone:

   mogrify -path "target" -quality 80 -format JPG "source/*.jpg"
