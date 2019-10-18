# Parallels Ubuntu UDP Port Forwarding Problem Reproduction

This is a reproduction of a problem where UDP port forwarding is not working on:

* Parallels 15.1.0 (47107)
* Vagrant OSX 2.2.5
* Vagrant Box generic/ubuntu1804 v1.9.36
* vagrant-parallels (2.0.1, global)

### Steps to reproduce

* Install vagrant and the vagrant parallels provider, then run the following.

```
git clone https://github.com/pward123/parallels-udp-forward-repro
cd parallels-udp-forward-repro
vagrant up
```

* Open the parallels desktop preferences and verify that UDP 14550 is forwarded to the VM.
* Run the following command to start listening for udp packets inside the VM

```
vagrant ssh -- -C "ip a && sudo nc -ukl 14550"
```

* Open a second terminal window (using bash) and run the following command replacing ##vagrant_guest_ip## with the ip address of the listed in the `ip a` output from the above command. You should see the first terminal window display "working".

```
echo "working" | nc -w1 -u ##vagrant_guest_ip## 14550
```

* Open a second terminal window (using bash) and run the following command. You should not see "not working" in the first terminal window.

```
echo "not working" | nc -w1 -u 127.0.0.1 14550
```
