---
title: aaaUsing hello Extension de machine virtuelle Docker pour Linux sur Azure
description: "Décrit les Docker et les extensions de Machines virtuelles Azure hello et montre comment tooprogrammatically créer des Machines virtuelles sur Azure qui sont des hôtes de docker à partir de la ligne de commande hello à l’aide de hello CLI d’Azure."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: eaff75e3-d929-4931-a4a1-8c377a8e7302
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/29/2016
ms.author: rasquill
ms.openlocfilehash: 1e192ad7c273aa9c997ea7bfa53b7de0b41a43c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-docker-vm-extension-from-hello-azure-command-line-interface-azure-cli"></a>À l’aide de hello Extension de machine virtuelle Docker à partir de hello Azure Interface de ligne (Azure)
> [!IMPORTANT] 
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. Pour plus d’informations sur l’utilisation d’extension de machine virtuelle de Docker hello avec modèle de gestionnaire de ressources hello, consultez [ici](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Cette rubrique décrit comment toocreate une machine virtuelle avec hello Extension de machine virtuelle Docker à partir de hello service en mode de gestion (asm) dans Azure CLI sur n’importe quelle plateforme. [Docker](https://www.docker.com/) d'entre hello est la virtualisation qui utilise les plus populaires [les conteneurs Linux](http://en.wikipedia.org/wiki/LXC) plutôt que des machines virtuelles comme un moyen d’isoler les données et le calcul sur des ressources partagées. Vous pouvez utiliser l’extension de machine virtuelle de Docker hello et de hello [Linux Agent Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate une machine virtuelle Docker qui héberge un nombre quelconque de conteneurs pour vos applications sur Azure. toosee une description détaillée des conteneurs et leurs avantages, consultez hello [tableau blanc de niveau élevé Docker](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).

## <a name="how-toouse-hello-docker-vm-extension-with-azure"></a>Comment toouse hello Extension de machine virtuelle Docker avec Azure
extension de machine virtuelle de Docker toouse hello avec Azure, vous devez installer une version de hello [Interface de ligne de commande Azure](https://github.com/Azure/azure-sdk-tools-xplat) (CLI d’Azure) supérieur 0.8.6 (comme ce Hello écrit la version actuelle est 0.10.0). Vous pouvez installer hello CLI d’Azure sur le Mac, Linux et Windows.

Terminer le processus de Hello toouse Docker sur Azure est simple :

* Installer hello CLI d’Azure et ses dépendances sur ordinateur hello à partir desquels vous souhaitez toocontrol Azure (sous Windows, ce sera une distribution Linux en cours d’exécution comme une machine virtuelle)
* Utiliser hello Azure CLI Docker commandes toocreate un hôte Docker de machine virtuelle dans Azure
* Utilisez hello local Docker commandes toomanage vos conteneurs Docker dans votre machine virtuelle de Docker dans Azure.

### <a name="install-hello-azure-command-line-interface-azure-cli"></a>Installer hello Azure Interface de ligne (Azure)
tooinstall et configurer hello CLI d’Azure, consultez [comment tooinstall hello Interface de ligne de commande Azure](../../../cli-install-nodejs.md). installation de hello tooconfirm, type `azure` à l’invite de commande hello et après un court instant, vous devez voir hello art Azure CLI ASCII, qui répertorie les basic de hello commandes tooyou disponible. Si l’installation de hello fonctionne correctement, vous devez être en mesure de tootype `azure help vm` et qu’une des commandes de hello répertorié est « docker ».

> [!NOTE]
> Docker a des outils pour Windows, [Docker Machine](https://docs.docker.com/installation/windows/), qui vous permet également la création de hello tooautomate d’un client docker que vous pouvez utiliser toowork avec des machines virtuelles Azure en tant qu’hôtes de docker.
> 
> 

### <a name="connect-hello-azure-cli-tootooyour-azure-account"></a>Se connecter hello CLI d’Azure tootooyour compte Azure
Avant de pouvoir utiliser hello CLI d’Azure, vous devez associer vos informations d’identification de compte Azure avec hello CLI d’Azure sur votre plateforme. Hello section [comment tooconnect tooyour abonnement Azure](../../../xplat-cli-connect.md) explique comment tooeither télécharger et importer votre **.publishsettings** de fichiers ou d’associer votre CLI d’Azure avec un id d’organisation.

> [!NOTE]
> Il existe quelques différences de comportement lorsque l’un ou hello autres méthodes d’authentification, donc que tooread hello document au-dessus des fonctionnalités différentes toounderstand hello.
> 
> 

### <a name="install-docker-and-use-hello-docker-vm-extension-for-azure"></a>Installer Docker et utiliser hello Extension de machine virtuelle Docker pour Azure
Suivez hello [des instructions d’installation Docker](https://docs.docker.com/installation/#installation) tooinstall Docker localement sur votre ordinateur.

toouse Docker avec une Machine virtuelle de Azure, image de Linux hello utilisé pour hello machine virtuelle doit disposer de hello [Agent de machine virtuelle Azure Linux](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) installé. Actuellement, seuls deux types d'image le permettent :

* Une image de Ubuntu à partir de la galerie d’images Azure de hello ou
* Une image personnalisée de Linux que vous avez créés avec hello Agent de machine virtuelle Azure Linux installé et configuré. Consultez [Agent de machine virtuelle Azure Linux](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) pour plus d’informations sur la façon toobuild une VM Linux personnalisé avec hello Agent de machine virtuelle Azure.

### <a name="using-hello-azure-image-gallery"></a>À l’aide de la galerie d’images Azure hello
À partir d’un interpréteur de commandes ou une session Terminal Server, utilisez hello commande CLI d’Azure toolocate hello image la plus récente Ubuntu dans toouse de la galerie de machine virtuelle hello en tapant suivante

`azure vm image list | grep Ubuntu-14_04`

Sélectionnez un des noms d’images hello, tels que `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`, et des commandes suivantes de hello utilisation toocreate un nouvel ordinateur virtuel à l’aide de cette image.

```
azure vm docker create -e 22 -l "West US" <vm-cloudservice name> "b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB" <username> <password>
```

où :

* *&lt;nom de la machine virtuelle-cloudservice&gt;*  hello désigne hello machine virtuelle qui deviendra ordinateur d’hôte de conteneur d’hello Docker dans Azure
* *&lt;nom d’utilisateur&gt;*  est username hello d’utilisateur de racine par défaut hello Hello machine virtuelle
* *&lt;mot de passe&gt;*  est un mot de passe hello Hello *nom d’utilisateur* compte qui répond aux normes hello de complexité pour Azure

> [!NOTE]
> Actuellement, un mot de passe doit comporter au moins 8 caractères, contenir une lettre minuscule et une lettre majuscule, un nombre et un caractère spécial, tel que celui de hello les caractères suivants : `!@#$%^&+=`. Non, la période de hello à fin hello Hello précédant la phrase n’est pas un caractère spécial.
> 
> 

Si la commande hello a réussi, vous devez voir quelque chose comme hello suivantes, selon les arguments précis hello et options que vous avez utilisé :

![](media/cli-use-docker/dockercreateresults.png)

> [!NOTE]
> Création d’un ordinateur virtuel peut prendre quelques minutes, mais une fois que ce dernier a été configuré (valeur d’état hello est `ReadyRole`) hello démarre le démon (service Docker de hello) de Docker et vous pouvez vous connecter hôte de conteneur Docker toohello.
> 
> 

tootest hello virtuelle Docker que vous avez créé dans Azure, type

`docker --tls -H tcp://<vm-name-you-used>.cloudapp.net:2376 info`

où  *&lt;vm-nom-vous-utilisé&gt;*  est le nom hello de machine virtuelle hello que vous avez utilisé dans votre appel trop`azure vm docker create`. Vous devez voir quelque chose de similaire suivant toohello, ce qui indique que votre machine virtuelle d’hôte Docker est disponible et en cours d’exécution dans Azure et en attente de vos commandes. 

Maintenant vous pouvez essayer de tooconnect à l’aide de vos informations de tooobtain client docker (dans certaines configurations de client Docker, tel que sur un Mac, vous devrez peut-être toouse `sudo`) :

    sudo docker --tls -H tcp://testsshasm.cloudapp.net:2376 info
    Password:
    Containers: 0
    Images: 0
    Storage Driver: devicemapper
    Pool Name: docker-8:1-131781-pool
    Pool Blocksize: 65.54 kB
    Backing Filesystem: extfs
    Data file: /dev/loop0
    Metadata file: /dev/loop1
    Data Space Used: 1.821 GB
    Data Space Total: 107.4 GB
    Data Space Available: 28 GB
    Metadata Space Used: 1.479 MB
    Metadata Space Total: 2.147 GB
    Metadata Space Available: 2.146 GB
    Udev Sync Supported: true
    Deferred Removal Enabled: false
    Data loop file: /var/lib/docker/devicemapper/devicemapper/data
    Metadata loop file: /var/lib/docker/devicemapper/devicemapper/metadata
    Library Version: 1.02.77 (2012-10-15)
    Execution Driver: native-0.2
    Logging Driver: json-file
    Kernel Version: 3.19.0-28-generic
    Operating System: Ubuntu 14.04.3 LTS
    CPUs: 1
    Total Memory: 1.637 GiB
    Name: testsshasm
    WARNING: No swap limit support

Simplement toobe certain qu’il s’agit d’utilisation, vous pouvez examiner hello VM pour hello extension Docker :

    azure vm extension get testsshasm
    info: Executing command vm extension get
    + Getting virtual machines
    data: Publisher Extension name ReferenceName Version State
    data: -------------------- --------------- ------------------------- ------- ------
    data: Microsoft.Azure.E... DockerExtension DockerExtension 1.* Enable
    info: vm extension get command OK

### <a name="docker-host-vm-authentication"></a>Authentification de la machine virtuelle hôte Docker
En outre toocreating hello machine virtuelle Docker, hello `azure vm docker create` commande crée également automatiquement hello certificats nécessaires tooallow votre Docker client ordinateur tooconnect toohello Azure hôte de conteneur à l’aide de HTTPS, et les certificats hello sont stockés sur les deux Bonjour les ordinateurs clients et hôtes, comme il convient. Lors des tentatives suivantes, les certificats existants hello sont réutilisées et partagées avec le nouvel hôte de hello.

Par défaut, les certificats sont placés dans `~/.docker`, et Docker sera toorun configuré sur le port **2376**. Si vous souhaitez que toouse un autre port ou le répertoire, vous pouvez utiliser une des manières suivantes les hello `azure vm docker create` les options de ligne de commande tooconfigure votre Docker conteneur hôte VM toouse un autre port ou les différents certificats pour la connexion des clients :

```
-dp, --docker-port [port]              Port toouse for docker [2376]
-dc, --docker-cert-dir [dir]           Directory containing docker certs [.docker/]
```

est configuré toolisten pour Hello démon Docker sur l’ordinateur hôte de hello et authentifier les connexions sur hello spécifié de port à l’aide de certificats de hello générés par hello de client `azure vm docker create` commande. Hello client doit être ces hôte Docker de certificats toogain accès toohello.

> [!NOTE]
> Un hôte en réseau en cours d’exécution sans ces certificats sera vulnérable tooanyone pouvant tooconnect toohello machine. Avant de modifier de la configuration par défaut de hello, assurez-vous que vous comprenez hello risques tooyour ordinateurs et applications.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
* Vous êtes prêt toogo toohello [Guide de l’utilisateur Docker] et utiliser votre machine virtuelle Docker. toocreate une machine virtuelle de Docker activée dans le nouveau portail de hello, consultez [comment toouse hello Extension de machine virtuelle Docker avec hello Portal].
* également, Hello extension de machine virtuelle Docker de Azure prend en charge de composer Docker, qui utilise un tootake de fichier YAML déclarative une application modélisée de développeur dans tous les environnements et générer un déploiement cohérent. Consultez [prise en main Docker et toodefine de composer et exécuter une application conteneur multiples sur une machine virtuelle Azure].  

<!--Anchors-->
[Subheading 1]:#subheading-1
[Subheading 2]:#subheading-2
[Subheading 3]:#subheading-3
[Next steps]:#next-steps

[How toouse hello Docker VM Extension with Azure]:#How-to-use-the-Docker-VM-Extension-with-Azure
[Virtual Machine Extensions for Linux and Windows]:#Virtual-Machine-Extensions-For-Linux-and-Windows
[Container and Container Management Resources for Azure]:#Container-and-Container-Management-Resources-for-Azure



<!--Link references-->
[Link 1 tooanother azure.microsoft.com documentation topic]:../../virtual-machines-windows-hero-tutorial.md
[Link 2 tooanother azure.microsoft.com documentation topic]:../../../app-service-web/web-sites-custom-domain-name.md
[Link 3 tooanother azure.microsoft.com documentation topic]:../storage-whatis-account.md
[comment toouse hello Extension de machine virtuelle Docker avec hello Portal]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-portal/

[Guide de l’utilisateur Docker]:https://docs.docker.com/userguide/

[prise en main Docker et toodefine de composer et exécuter une application conteneur multiples sur une machine virtuelle Azure]:../docker-compose-quickstart.md
