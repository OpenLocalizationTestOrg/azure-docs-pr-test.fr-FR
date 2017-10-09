---
title: tooFreeBSD aaaIntroduction sur Azure | Documents Microsoft
description: "Apprenez à utiliser des machines virtuelles FreeBSD sur Azure"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 32b87a5f-d024-4da0-8bf0-77e233d1422b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: kyliel
ms.openlocfilehash: 43ba7a70ed21e7fb8b331f4a26db0426e098c4aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toofreebsd-on-azure"></a>TooFreeBSD introduction sur Azure
Cette rubrique offre une vue d’ensemble de l’exécution d’une machine virtuelle FreeBSD dans Azure.

## <a name="overview"></a>Vue d'ensemble
FreeBSD pour Microsoft Azure est qu'un système d’exploitation avancé utilisé toopower les serveurs modernes, les ordinateurs de bureau et les plateformes incorporés.

Microsoft Corporation est disposition des images de FreeBSD sur Azure avec hello [Agent invité d’ordinateur virtuel Azure](https://github.com/Azure/WALinuxAgent/) préconfiguré. Actuellement, hello versions FreeBSD suivantes sont proposées en tant qu’images par Microsoft :

- FreeBSD 10.3-RELEASE
- FreeBSD 11.0-RELEASE

Hello est chargé pour la communication entre hello FreeBSD VM et hello tissu Azure pour les opérations telles que l’approvisionnement hello VM sur la première utilisation (nom d’utilisateur, mot de passe ou clé SSH, nom d’hôte, etc.) et l’activation des fonctionnalités pour les extensions de machine virtuelle sélectives.

Comme pour les versions futures de FreeBSD, stratégie de hello est toostay en cours et rendre hello dernières versions disponibles peu de temps après leur publication par l’équipe d’ingénierie hello FreeBSD version.

## <a name="deploying-a-freebsd-virtual-machine"></a>Déploiement d’une machine virtuelle FreeBSD
Déploiement d’un ordinateur virtuel de FreeBSD est un processus simple à l’aide d’une image à partir de Bonjour Azure Marketplace de hello portail Azure :

- [10.3 FreeBSD sur hello Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
- [11.0 FreeBSD sur hello Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/)

### <a name="create-a-freebsd-vm-through-azure-cli-20-on-freebsd"></a>Créer une machine virtuelle FreeBSD via Azure CLI 2.0 sur FreeBSD
Vous devez tout d’abord tooinstall [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) bien que la commande suivante sur un ordinateur de FreeBSD.

```bash 
curl -L https://aka.ms/InstallAzureCli | bash
```

Si l’interpréteur de commandes n’est pas installé sur votre ordinateur FreeBSD, exécutez la commande avant l’installation de hello suivante. 

```bash
sudo pkg install bash
```

Si les python n’est pas installé sur votre ordinateur FreeBSD, exécutez suivant les commandes avant l’installation de hello. 

```bash
sudo pkg install python35
cd /usr/local/bin 
sudo rm /usr/local/bin/python 
sudo ln -s /usr/local/bin/python3.5 /usr/local/bin/python
```

Pendant l’installation de hello, vous êtes invité `Modify profile tooupdate your $PATH and enable shell/tab completion now? (Y/n)`. Si vous répondez `y` et entrez `/etc/rc.conf` en tant que `a path tooan rc file tooupdate`, vous pouvez répondre à problème de hello `ERROR: [Errno 13] Permission denied`. tooresolve ce problème, vous devez accorder hello écriture toocurrent droit sur le fichier de hello `etc/rc.conf`.

Vous pouvez maintenant vous connecter à Azure et créer votre machine virtuelle FreeBSD. Vous trouverez ci-dessous un exemple toocreate une machine virtuelle 11.0 de FreeBSD. Vous pouvez également ajouter le paramètre hello `--public-ip-address-dns-name` avec un nom DNS globalement unique pour une adresse IP publique nouvellement créé. 

```azurecli
az login 
az group create --name myResourceGroup --location eastus
az vm create --name myFreeBSD11 \
    --resource-group myResourceGroup \
    --image MicrosoftOSTC:FreeBSD:11.0:latest \
    --admin-username azureuser \
    --generate-ssh-keys
```

Vous pouvez ensuite vous connecter dans tooyour FreeBSD VM via l’adresse ip hello imprimé dans la sortie de hello d’au-dessus de déploiement. 

```bash
ssh azureuser@xx.xx.xx.xx -i /etc/ssh/ssh_host_rsa_key
```   

## <a name="vm-extensions-for-freebsd"></a>Extension de machine virtuelle pour FreeBSD
Voici les extensions de machines virtuelles prises en charge par FreeBSD.

### <a name="vmaccess"></a>VMAccess
Hello [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) extension peut :

* Réinitialiser le mot de passe hello d’hello d’origine sudo.
* Créer un nouvel utilisateur de sudo avec mot de passe hello spécifié.
* Définissez la clé d’hôte public hello avec clé hello donné.
* Réinitialiser la clé d’hôte public hello fournie pendant l’approvisionnement si la clé d’hôte hello n’est pas fournie d’ordinateur virtuel.
* Ouvrez le port SSH hello (22) et de restauration hello sshd_config si reset_ssh a la valeur tootrue.
* Supprimer un utilisateur existant de hello.
* Vérifier les disques.
* Réparer un disque ajouté.

### <a name="customscript"></a>CustomScript
Hello [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) extension peut :

* Si fourni, télécharger les scripts de hello personnalisé de stockage Azure ou de stockage public externe (par exemple, GitHub).
* Exécutez le script de point d’entrée hello.
* Prendre en charge les commandes inline.
* Convertir automatiquement le saut de ligne Windows dans des scripts Shell et Python.
* Supprimer automatiquement les nomenclatures dans des scripts Shell et Python.
* Protéger les données sensibles dans CommandToExecute.

> [!NOTE]
> La machine virtuelle FreeBSD prend uniquement en charge CustomScript version 1.x à ce stade.  

## <a name="authentication-user-names-passwords-and-ssh-keys"></a>Authentification : noms d’utilisateurs, mots de passe et clés SSH
Lorsque vous créez une machine virtuelle de FreeBSD à l’aide de hello portail Azure, vous devez fournir un nom d’utilisateur, le mot de passe ou la clé publique SSH.
Noms d’utilisateur pour le déploiement d’un ordinateur virtuel de FreeBSD sur Azure ne doivent pas correspondre à des noms des comptes système (UID < 100) déjà présentes dans l’ordinateur virtuel de hello (« root », par exemple).
Actuellement, seuls hello RSA de la clé SSH est pris en charge. Une clé SSH multiligne doit commencer par `---- BEGIN SSH2 PUBLIC KEY ----` et se terminer par `---- END SSH2 PUBLIC KEY ----`.

## <a name="obtaining-superuser-privileges"></a>Obtention de privilèges de superutilisateur
compte d’utilisateur Hello est spécifié lors du déploiement d’instance de machine virtuelle sur Azure est un compte privilégié. package de sudo Hello a été installé dans hello publié FreeBSD image.
Une fois que vous êtes connecté via ce compte d’utilisateur, vous pouvez exécuter des commandes en tant que racine en utilisant la syntaxe de commande hello.

```
$ sudo <COMMAND>
```

Vous pouvez éventuellement obtenir un interpréteur de commandes root avec `sudo -s`.

## <a name="known-issues"></a>Problèmes connus
Hello [Agent invité d’ordinateur virtuel Azure](https://github.com/Azure/WALinuxAgent/) version 2.2.2 a un [problème connu] (https://github.com/Azure/WALinuxAgent/pull/517) qui provoque l’échec de disposition hello pour VM FreeBSD sur Azure. Hello correctif a été capturée par [Agent invité d’ordinateur virtuel Azure](https://github.com/Azure/WALinuxAgent/) version 2.2.3 et versions ultérieures. 

## <a name="next-steps"></a>Étapes suivantes
* Accédez trop[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) toocreate un VM FreeBSD.
* Si vous souhaitez toobring vos propres tooAzure FreeBSD, reportez-vous trop[créer et charger un tooAzure FreeBSD VHD](classic/freebsd-create-upload-vhd.md).
