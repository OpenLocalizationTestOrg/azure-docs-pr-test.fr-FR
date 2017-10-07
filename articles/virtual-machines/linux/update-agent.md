---
title: "aaaUpdate hello Azure Linux Agent à partir de GitHub | Documents Microsoft"
description: "Découvrez comment tooupdate Azure Linux Agent pour votre VM Linux dans la version la plus récente à partir de GitHub toohello Azure"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: f1f19300-987d-4f29-9393-9aba866f049c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: mingzhan
ms.openlocfilehash: 4ce7c56efc1e6563e6415f7687573f9fb9e7b4c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-hello-azure-linux-agent-on-a-vm"></a>Comment tooupdate hello Azure Linux Agent sur un ordinateur virtuel

tooupdate votre [Linux Agent Azure](https://github.com/Azure/WALinuxAgent) sur un Linux VM dans Azure, vous devez déjà disposer :

- Une machine virtuelle Linux en cours d'exécution dans Azure.
- Une connexion de toothat Linux VM à l’aide de SSH.

Vous devez toujours vérifier tout d’abord d’un package dans le référentiel de distribution de Linux hello. Il est possible de package hello disponible peut être pas la version la plus récente hello, toutefois, l’activation de mise à jour automatique garantit hello Linux Agent sera toujours obtenir les dernières mises à jour de hello. Si vous avez des problèmes d’installation à partir des gestionnaires de packages hello, vous devez rechercher la prise en charge à partir du fournisseur de distributeur hello.

## <a name="updating-hello-azure-linux-agent"></a>Mise à jour hello Linux Agent Azure

## <a name="ubuntu"></a>Ubuntu

#### <a name="check-your-current-package-version"></a>Vérifier votre version actuelle du package

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a>Mettre à jour le cache du package

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a>Installez la dernière version de package hello

```bash
sudo apt-get install walinuxagent
```

#### <a name="ensure-auto-update-is-enabled"></a>Vérifier que la mise à jour automatique est activée

Vérifiez tout d’abord, toosee s’il est activé :

```bash
cat /etc/waagent.conf
```

Recherchez « AutoUpdate.Enabled ». Si vous voyez cette sortie, cela signifie qu’elle est activée :

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable exécuter :

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Redémarrez le service de waagent hello

#### <a name="restart-agent-for-1404"></a>Redémarrer l’agent pour 14.04

```bash
initctl restart walinuxagent
```

#### <a name="restart-agent-for-1604--1704"></a>Redémarrer l’agent pour 16.04 / 17.04

```bash
systemctl restart walinuxagent.service
```

## <a name="debian"></a>Debian

### <a name="debian-7-wheezy"></a>Debian 7 « Wheezy »

#### <a name="check-your-current-package-version"></a>Vérifier votre version actuelle du package

```bash
dpkg -l | grep waagent
```

#### <a name="update-package-cache"></a>Mettre à jour le cache du package

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a>Installez la dernière version de package hello

```bash
sudo apt-get install waagent
```

#### <a name="enable-agent-auto-update"></a>Activer la mise à jour automatique de l’agent
Cette version de Debian n’a pas de version supérieure ou égale à 2.0.16. Par conséquent, AutoUpdate n’est pas disponible pour elle. sortie de Hello de hello au-dessus de commande vous indiquera si le package de hello est à jour.

### <a name="debian-8-jessie--debian-9-stretch"></a>Debian 8 « Jessie » / Debian 9 « Stretch »

#### <a name="check-your-current-package-version"></a>Vérifier votre version actuelle du package

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a>Mettre à jour le cache du package

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a>Installez la dernière version de package hello

```bash
sudo apt-get install waagent
```
#### <a name="ensure-auto-update-is-enabled"></a>Vérifier que la mise à jour automatique est activée 

Vérifiez tout d’abord, toosee s’il est activé :

```bash
cat /etc/waagent.conf
```

Recherchez « AutoUpdate.Enabled ». Si vous voyez cette sortie, cela signifie qu’elle est activée :

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable exécuter :

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Redémarrez le service de waagent hello

```
sudo systemctl restart walinuxagent.service
```

## <a name="redhat--centos"></a>Redhat / CentOS

### <a name="rhelcentos-6"></a>RHEL/CentOS 6

#### <a name="check-your-current-package-version"></a>Vérifier votre version actuelle du package

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a>Vérifier les mises à jour disponibles

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a>Installez la dernière version de package hello

```bash
sudo yum install WALinuxAgent
```

#### <a name="ensure-auto-update-is-enabled"></a>Vérifier que la mise à jour automatique est activée 

Vérifiez tout d’abord, toosee s’il est activé :

```bash
cat /etc/waagent.conf
```

Recherchez « AutoUpdate.Enabled ». Si vous voyez cette sortie, cela signifie qu’elle est activée :

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable exécuter :

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Redémarrez le service de waagent hello

```
sudo service waagent restart
```

### <a name="rhelcentos-7"></a>RHEL/CentOS 7

#### <a name="check-your-current-package-version"></a>Vérifier votre version actuelle du package

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a>Vérifier les mises à jour disponibles

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a>Installez la dernière version de package hello

```bash
sudo yum install WALinuxAgent  
```

#### <a name="ensure-auto-update-is-enabled"></a>Vérifier que la mise à jour automatique est activée 

Vérifiez tout d’abord, toosee s’il est activé :

```bash
cat /etc/waagent.conf
```

Recherchez « AutoUpdate.Enabled ». Si vous voyez cette sortie, cela signifie qu’elle est activée :

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable exécuter :

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Redémarrez le service de waagent hello

```bash
sudo systemctl restart waagent.service
```

## <a name="suse-sles"></a>SUSE SLES

### <a name="suse-sles-11-sp4"></a>SUSE SLES 11 SP4

#### <a name="check-your-current-package-version"></a>Vérifier votre version actuelle du package

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a>Vérifier les mises à jour disponibles

Hello au-dessus de sortie vous indique si le package de hello est de toodate.

#### <a name="install-hello-latest-package-version"></a>Installez la dernière version de package hello

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a>Vérifier que la mise à jour automatique est activée 

Vérifiez tout d’abord, toosee s’il est activé :

```bash
cat /etc/waagent.conf
```

Recherchez « AutoUpdate.Enabled ». Si vous voyez cette sortie, cela signifie qu’elle est activée :

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable exécuter :

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Redémarrez le service de waagent hello

```bash
sudo /etc/init.d/waagent restart
```

### <a name="suse-sles-12-sp2"></a>SUSE SLES 12 SP2

#### <a name="check-your-current-package-version"></a>Vérifier votre version actuelle du package

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a>Vérifier les mises à jour disponibles

Dans la sortie de hello de hello ci-dessus, cela vous indiquera si le package de hello est à jour.

#### <a name="install-hello-latest-package-version"></a>Installez la dernière version de package hello

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a>Vérifier que la mise à jour automatique est activée 

Vérifiez tout d’abord, toosee s’il est activé :

```bash
cat /etc/waagent.conf
```

Recherchez « AutoUpdate.Enabled ». Si vous voyez cette sortie, cela signifie qu’elle est activée :

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable exécuter :

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Redémarrez le service de waagent hello

```bash
sudo systemctl restart waagent.service
```

## <a name="oracle-6-and-7"></a>Oracle 6 et 7

Pour Oracle Linux, assurez-vous que hello `Addons` référentiel est activé. Choisissez le fichier de hello tooedit `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) ou `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux) et remplacez-la par hello `enabled=0` trop`enabled=1` sous **[ol6_addons]** ou **[ol7_addons]** Dans ce fichier.

Ensuite, tooinstall hello version la plus récente de hello Azure Linux Agent, type :

```bash
sudo yum install WALinuxAgent
```

Si vous ne trouvez pas référentiel de module complémentaire hello vous pouvez simplement ajouter ces lignes à fin hello de votre fichier .repo selon la version d’Oracle Linux tooyour :

Pour les machines virtuelles Oracle Linux 6 :

```sh
[ol6_addons]
name=Add-Ons for Oracle Linux $releasever ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL6/addons/x86_64
gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-ol6
gpgcheck=1
enabled=1
```

Pour les machines virtuelles Oracle Linux 7 :

```sh
[ol7_addons]
name=Oracle Linux $releasever Add ons ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL7/addons/$basearch/
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle
gpgcheck=1
enabled=0
```

Tapez ensuite :

```bash
sudo yum update WALinuxAgent
```

En général, cela est que nécessaire, mais si pour une raison quelconque vous devez tooinstall à partir de https://github.com directement, hello utilisation suivant les étapes.


## <a name="update-hello-linux-agent-when-no-agent-package-exists-for-distribution"></a>Mettre à jour hello Linux Agent lorsque aucun package de l’agent n’existe pour la distribution

Installez wget (il existe des versions qui ne l’installation par défaut, tels que des versions Redhat, CentOS et Oracle Linux 6.4 et 6.5) en tapant `sudo yum install wget` sur la ligne de commande hello.

### <a name="1-download-hello-latest-version"></a>1. Télécharger la version la plus récente hello
Ouvrez [hello version de l’Agent de Linux Azure dans GitHub](https://github.com/Azure/WALinuxAgent/releases) dans une page web et découvrez le numéro de version plus récente hello. (Vous pouvez rechercher votre version actuelle en tapant `waagent --version`.)

#### <a name="for-version-22x-or-later-type"></a>Pour la version 2.2.x ou ultérieure, tapez :
```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.x.zip
unzip v2.2.x.zip.zip
cd WALinuxAgent-2.2.x
```

Hello ligne suivante utilise version2.2.0 comme exemple :

```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.14.zip
unzip v2.2.14.zip  
cd WALinuxAgent-2.2.14
```

### <a name="2-install-hello-azure-linux-agent"></a>2. Installer hello Linux Agent Azure

#### <a name="for-version-22x-use"></a>Pour la version 2.2.x, tapez :
Vous devrez peut-être le package de hello tooinstall `setuptools` premier--se [ici](https://pypi.python.org/pypi/setuptools). Exécutez ensuite la commande suivante :

```bash
sudo python setup.py install
```

#### <a name="ensure-auto-update-is-enabled"></a>Vérifier que la mise à jour automatique est activée

Vérifiez tout d’abord, toosee s’il est activé :

```bash
cat /etc/waagent.conf
```

Recherchez « AutoUpdate.Enabled ». Si vous voyez cette sortie, cela signifie qu’elle est activée :

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable exécuter :

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="3-restart-hello-waagent-service"></a>3. Redémarrez le service de waagent hello
Pour la plupart des versions de linux :

```bash
sudo service waagent restart
```

Pour Ubuntu, procédez comme suit :

```bash
sudo service walinuxagent restart
```

Pour CoreOS, procédez comme suit :

```bash
sudo systemctl restart waagent
```

### <a name="4-confirm-hello-azure-linux-agent-version"></a>4. Confirmer la version de le Linux Agent Azure hello
    
```bash
waagent -version
```

Pour CoreOS, hello au-dessus de commande peuvent ne pas fonctionne.

Vous verrez que hello Azure Linux Agent version a été mis à jour toohello nouvelle version.

Pour plus d’informations sur hello Linux Agent Azure, consultez [Lisezmoi de l’Agent Linux Azure](https://github.com/Azure/WALinuxAgent).
