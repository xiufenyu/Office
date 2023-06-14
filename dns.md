1. Temporary Solution
$ nano /run/systemd/resolve/resolv.conf

    ```
    nameserver 132.205.96.93
    nameserver 132.205.96.94
    search encs.concordia.ca
    ```

$ nano /run/systemd/resolve/stub-resolv.conf

    ```
    nameserver 127.0.0.53
    options edns0 trust-ad
    search encs.concordia.ca
    ```

$ sudo rm -f /etc/resolv.conf

$ sudo ln -s /run/resolvconf/resolv.conf /etc/resolv.conf

reference: https://askubuntu.com/questions/1406630/hostnames-cannot-be-resolved-after-upgrading-to-22-04


2. Permanant Solution

Ubuntu 22.04 does not use resolv.conf anymore by default, however it can be installed by

$ sudo apt update

$ sudo apt install resolvconf

check that resolvconf service is started and enabled

$ sudo systemctl status resolvconf.service

If service is not enabled, you can start and enable using the following commands:

$ sudo systemctl start resolvconf.service

$ sudo systemctl enable resolvconf.service

Now edit the resolv.conf.d/head configuration file

$ sudo nano /etc/resolvconf/resolv.conf.d/head

and add your DNS addresses into it (for example I use 8.8.8.8 and 8.8.4.4)

$ nameserver 8.8.8.8 

$ nameserver 8.8.4.4

Now force resolvconf to run update scripts when invoked with -u

$ sudo resolvconf --enable-updates 

Now run updates

$ sudo resolvconf -u

Now if you check the content of resolv.conf file using the following command

$ cat /etc/resolv.conf

you must see your DNS configuration. If not, try the following commands and check again

$ sudo systemctl restart resolvconf.service

$ sudo systemctl restart systemd-resolved.service


reference: https://askubuntu.com/questions/346838/how-do-i-configure-my-dns-settings-in-ubuntu-server