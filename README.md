# Useful-Linux-Commands
A random selection of useful Linux commands for a variety of tasks.

* Recursive sed search replace:

  find . -type f -exec sed -i 's/foo/bar/g' {} +

* To renew certbot Let's Encrypt certificate:

   sudo ./certbot-auto --expand -d domain1.com domain2.com

* To bulk rename files, changing extension case:

   for file in *.jpg; do 
    mv "$file" "$(basename "$file" jpg)JPG"; done

* Bulk svg to png conversion

   for file in *.svg; do
   inkscape -w 2000 "$file" -e "$(basename "$file" svg)png"; done

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

* To see fail2ban status for a given set (such as sshd)
   
   sudo fail2ban-client status sshd

* To handle torrents
   service transmission-deamon stop
   transmission-deamon --noauth
   transmission-deamon -a "MAGNETURI"
   transmission-daemon -l   #shows status
   transmission-daemon -t 1 -r   #removes torrent N.1

* To rip a CD
   cdparanoia -B
   for t in track{01..18}*.wav; do lame -b 320 $t; done
   use puddletag to add ID3 tags

* To loop microphone to speakers
   package name is pavucontrol
   pactl load-module module-loopback latency_msec=1
   pactl unload-module $(pactl list short modules | awk '$2 =="module-loopback" { print $1 }' - ) # to disable

* Batch convert HEIC files to jpg (imagemagick)
   mogrify -format jpg *.HEIC

* Copy from a samba resource 
   rsync --recursive -azPv --delete --dry-run --ignore-existing /run/user/1000/gvfs/smb-share\:server\=olimpodisk.local\,share\=public/Stefano/Foto/* /media/stefano/Secrets/Foto/

* Sync two dirs
  rsync --progress --delete -i -t -r  -e 'ssh -p 22 -o IdentityFile=~/.ssh/id -o IdentitiesOnly=yes' 'user@192.x.x.x:/dir/' '/dir'

* To mount an LVE full disk encrypted volume
  sudo vgchange -a y  # activates volume group
  sudo mount /dev/mapper/vgmint2-root /mnt/test/  # mounts, fetch vgname with lsblk
  # cryptsetup luksOpen /dev/sdb3 luks-d3921fcb-3103-4666-aa35-a2c6e2414756  # optional, to decrypt if OS doesn't ask; fetch ID with lsblk

**Imagemagick**
* To resize, compress and rename all jpg files in a folder appending *_tn*:

   convert "source/*.jpg" -quality 50 -monitor -debug cache -resize "150x150>" -set filename:area "%t_tn" "target/%[filename:area].jpg"

* To compress alone:

   mogrify -path "target" -quality 80 -format JPG "source/*.jpg"
