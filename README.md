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
+--------------------------------------------------------------------------+
|                                                                          |
|  +-------------+            Vagrant VM's           +-------------+       |
|  | SVMB1       |                                   | SVMB2       |       |
|  | 192.168.1.2 |                                   | 192.168.2.2 |       |
|  +------+------+                                   +------+------+       |
|         |                                                 |              |
|         |                                                 |              |
|         | Private Network +-------------+ Private Network |              |
|         +-----192.168.1.1-+ PFSense     +-192.168.2.1-----+              |
|                           +------+------+                                |
|                                  |                                       |
|                             192.168.3.x                                  |
|                                  |                                       |
|                                  +----NAT-Network----+----------------+  |
|                                                      |  Windows HOST  |  |
+------------------------------------------------------+                +--+
                                                       +----------------+

```
### IP-Table

### DNS

## Installation

### Setup folders and required files

### Vagrantfiles

## Testing

## Project review