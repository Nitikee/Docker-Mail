# Docker-Mail

Nitinan Keel </br>
Containerization of application and services </br>
Docker-Mail

## Table of contents
* [Concept]
  * [Requierements]
  * [Networkdiagramm]
  * [IP-Table]
  * [DNS]
* [Installation]
  * [Setup folders and required files]
  * [Vagrantfiles]
* [Testing]
* [Project review]

## Concept

### Requirements:
* [Vagrant](https://www.vagrantup.com/downloads.html)
* [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
* [Git](https://git-scm.com/download/win)
* [Vagrant plugin](https://github.com/leighmcculloch/vagrant-docker-compose)

### Networkdiagramm
```
                                     +------------------------+
                                     | SVMB1                  |
                   SMTP --> 25  +----+ 192.168.1.10/24        |
                   IMAP --> 143 |    | tandem2.nitinankeel.ch |
+----------------+              |    +------------------------+
| Windows Client +--------------+
| 192.168.1.2/24 |              |    +------------------------+
+----------------+              |    | SVMB2                  |
                                +----+ 192.168.1.20/24        |
                                     | tandem1.nitinankeel.ch |
                                     +------------------------+
```
### DNS Records
```
 +-------------------------------------------------------------+
 | DNS Server                                                  |
 | ns1.hostserv.eu                                             |
 |                                                             |
 | A Record                                                    |
 | mail.tandem1.nitinankeel.ch ==> 192.168.1.10/24             |
 | mail.tandem2.nitinankeel.ch ==> 192.168.1.20/24             |
 | tandem1.nitinankeel.ch      ==> 192.168.1.10/24             |
 | tandem2.nitinankeel.ch      ==> 192.168.1.20/24             |
 |                                                             |
 | MX Record                                                   |
 | tandem1.nitinankeel.ch      ==> mail.tandem1.nitinankeel.ch |
 | tandem2.nitinankeel.ch      ==> mail.tandem2.nitinankeel.ch |
 +-------------------------------------------------------------+
```

### Setup folders and required files
```
. 
├── tandem1         
|   ├── docker-compose.yml
│   └── user.sh
├── tandem2
|   ├── docker-compose.yml
│   └── user.sh         
├── LICENSE (GPLv2)
└── Vagrantfile               # Vagrant file
```
### Vagrantfile


## Testing

## Project review