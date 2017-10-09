---
title: aaaUsing Extension de machine virtuelle Docker pour Linux | Documents Microsoft
description: "Décrit Docker et extensions des Machines virtuelles Azure hello et comment toocreate Machines virtuelles Azure qui sont des hôtes docker à l’aide de hello CLI d’Azure dans le modèle de déploiement classique."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 19cf64e8-f92c-43ad-a120-8976cd9102ac
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/27/2016
ms.author: rasquill
ms.openlocfilehash: 9d455b63c48b0c1b6f14862e072f899a73b46153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-docker-vm-extension-with-hello-azure-classic-portal"></a>À l’aide de hello Extension de machine virtuelle Docker avec hello portail Azure classic
> [!IMPORTANT] 
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.

[Docker](https://www.docker.com/) d'entre hello est la virtualisation qui utilise les plus populaires [les conteneurs Linux](http://en.wikipedia.org/wiki/LXC) plutôt que des machines virtuelles comme un moyen d’isoler les données et le calcul sur des ressources partagées. Vous pouvez utiliser extension de machine virtuelle de Docker hello gérée par [Linux Agent Azure] toocreate une machine virtuelle Docker qui héberge un nombre quelconque de conteneurs pour vos applications sur Azure.

> [!NOTE]
> Cette rubrique décrit comment toocreate une machine virtuelle de Docker à partir de hello portail Azure classic. toosee toocreate une machine virtuelle de Docker à la ligne de commande hello, voir [comment toouse hello Extension de machine virtuelle Docker à partir de hello Azure Interface de ligne (Azure)]. toosee une description détaillée des conteneurs et leurs avantages, consultez hello [tableau blanc de niveau élevé Docker](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).
> 
> 

## <a name="create-a-new-vm-from-hello-image-gallery"></a>Créer une machine virtuelle à partir de la galerie d’images de hello
première étape de Hello nécessite une machine virtuelle de Azure à partir d’une image Linux qui prend en charge hello Extension de machine virtuelle Docker, à l’aide d’une image Ubuntu 14.04 LTS hello Galerie d’images en tant qu’une image de serveur exemple et Ubuntu 14.04 Desktop en tant que client. Dans le portail de hello, cliquez sur **+ nouveau** Bonjour bas à gauche angle toocreate une nouvelle instance de la machine virtuelle et sélectionnez une image d’Ubuntu 14.04 LTS à partir de sélections hello disponibles ou de hello terminer la galerie d’images, comme indiqué ci-dessous.

> [!NOTE]
> Actuellement, seules les images Ubuntu 14.04 LTS plus récentes que celle de juillet 2014 prend en charge hello Extension de machine virtuelle Docker.
> 
> 

![Create a new Ubuntu Image](./media/portal-use-docker/ChooseUbuntu.png)

## <a name="create-docker-certificates"></a>Création de certificats Docker
Après avoir hello machine virtuelle a été créé, vérifiez que Docker est installé sur votre ordinateur client. (pour plus d'informations, voir [Instructions d'installation de Docker](https://docs.docker.com/installation/#installation).)

Créer des fichiers de certificat et la clé pour la communication Docker selon trop hello[en cours d’exécution de Docker avec https] et placez-les dans hello  **`~/.docker`**  répertoire sur votre ordinateur client.

> [!NOTE]
> actuellement, Hello Extension de machine virtuelle Docker dans le portail de hello requiert les informations d’identification qui sont codées en base64.
> 
> 

À la ligne de commande hello, utilisez  **`base64`**  ou favori un autre encodage rubriques codé en base 64 des toocreate d’outil. Cette opération avec un ensemble simple de fichiers de certificat et la clé peut se présenter toothis similaire :

```
 ~/.docker$ ls
 ca-key.pem  ca.pem  cert.pem  key.pem  server-cert.pem  server-key.pem
 ~/.docker$ base64 ca.pem > ca64.pem
 ~/.docker$ base64 server-cert.pem > server-cert64.pem
 ~/.docker$ base64 server-key.pem > server-key64.pem
 ~/.docker$ ls
 ca64.pem    ca.pem    key.pem            server-cert.pem   server-key.pem
 ca-key.pem  cert.pem  server-cert64.pem  server-key64.pem
```

## <a name="add-hello-docker-vm-extension"></a>Ajouter hello Extension de machine virtuelle Docker
tooadd hello Extension de machine virtuelle Docker, recherchez l’instance de machine virtuelle hello vous avez créé et faites défiler trop**Extensions** et cliquez sur toobring des Extensions de machine virtuelle, comme illustré ci-dessous.

> [!NOTE]
> Cette fonctionnalité est prise en charge dans le portail en version préliminaire hello uniquement : https://portal.azure.com/
> 
> 

![](media/portal-use-docker/ClickExtensions.png)

### <a name="add-an-extension"></a>Ajout d’une extension
Cliquez sur hello **+ ajouter** toodisplay hello possibles Extensions de machine virtuelle vous pouvez ajouter toothis machine virtuelle.

![](media/portal-use-docker/ClickAdd.png)

### <a name="select-hello-docker-vm-extension"></a>Sélectionnez hello Extension de machine virtuelle Docker
Hello, Extension de machine virtuelle Docker, qui met à jour les description de Docker hello et les liens importants, et cliquez sur **créer** au niveau de la procédure d’installation hello bas toobegin hello.

![](media/portal-use-docker/ChooseDockerExtension.png)

![](media/portal-use-docker/CreateButtonFocus.png)

### <a name="add-your-certificate-and-key-files"></a>Ajout de vos certificats et de vos fichiers de clés :
Dans les champs de formulaire hello, entrez hello codée en base64 les versions de votre certificat d’autorité de certification, votre certificat de serveur et votre clé de serveur, comme indiqué dans le graphique suivant de hello.

![](media/portal-use-docker/AddExtensionFormFilled.png)

> [!NOTE]
> Notez que (par exemple hello précédant l’image) hello 2376 est renseigné par défaut. Vous pouvez entrer n’importe quel point de terminaison ici, mais maintenant hello seront tooopen des hello point de terminaison de mise en correspondance. Si vous modifiez la valeur par défaut de hello, assurez-vous que tooopen des hello correspondant à un point de terminaison à l’étape suivante de hello.
> 
> 

## <a name="add-hello-docker-communication-endpoint"></a>Ajouter hello point de terminaison de Communication Docker
Lorsque vous affichez un groupe de ressources hello que vous avez créé, sélectionnez hello groupe de sécurité réseau associé à votre machine virtuelle, puis cliquez sur **règles de sécurité de trafic entrant** tooview hello règles comme illustré ici.

![](media/portal-use-docker/AddingEndpoint.png)

Cliquez sur **+ ajouter** tooadd une autre règle et dans le cas par défaut de hello, entrez un nom pour le point de terminaison hello (dans cet exemple, **Docker**) et 2376 « plage de Port de Destination ». Définir l’affichage de valeur de protocole hello **TCP**, puis cliquez sur **OK** règle de hello toocreate.

![](media/portal-use-docker/AddEndpointFormFilledOut.png)

## <a name="test-your-docker-client-and-azure-docker-host"></a>Tester le client Docker et l’hôte Azure Docker
Recherchez et copiez hello nom de domaine de votre machine virtuelle et à la ligne de commande hello de votre ordinateur client, tapez `docker --tls -H tcp://` *dockerextension* `.cloudapp.net:2376 info` (où *dockerextension* est remplacé par hello sous-domaine de votre machine virtuelle).

résultat de Hello doit apparaître toothis similaire :

```
$ docker --tls -H tcp://dockerextension.cloudapp.net:2376 info
Containers: 0
Images: 0
Storage Driver: devicemapper
 Pool Name: docker-8:1-131214-pool
 Pool Blocksize: 65.54 kB
 Data file: /var/lib/docker/devicemapper/devicemapper/data
 Metadata file: /var/lib/docker/devicemapper/devicemapper/metadata
 Data Space Used: 305.7 MB
 Data Space Total: 107.4 GB
 Metadata Space Used: 729.1 kB
 Metadata Space Total: 2.147 GB
 Library Version: 1.02.82-git (2013-10-04)
Execution Driver: native-0.2
Kernel Version: 3.13.0-36-generic
WARNING: No swap limit support
```

Après avoir terminé hello étapes ci-dessus, vous avez maintenant un hôte Docker entièrement fonctionnel en cours d’exécution sur une machine virtuelle Azure, configuré toobe connecté tooremotely à partir d’autres clients.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Étapes suivantes
Vous êtes prêt toogo toohello [Guide de l’utilisateur Docker] et utiliser votre machine virtuelle Docker. Si vous souhaitez tooautomate création d’hôtes Docker sur les machines virtuelles Azure via l’interface de ligne de commande, consultez [comment toouse hello Extension de machine virtuelle Docker à partir de hello Azure Interface de ligne (Azure)]

<!--Anchors-->
[Create a new VM from hello Image Gallery]:#createvm
[Create Docker Certificates]:#dockercerts
[Add hello Docker VM Extension]:#adddockerextension
[Test Docker Client and Azure Docker Host]:#testclientandserver
[Next steps]:#next-steps

<!--Image references-->
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[6]:./media/markdown-template-for-new-articles/pretty49.png
[7]:./media/markdown-template-for-new-articles/channel-9.png


<!--Link references-->
[comment toouse hello Extension de machine virtuelle Docker à partir de hello Azure Interface de ligne (Azure)]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-xplat-cli/
[Linux Agent Azure]:../agent-user-guide.md
[Link 3 tooanother azure.microsoft.com documentation topic]:../storage-whatis-account.md

[en cours d’exécution de Docker avec https]:http://docs.docker.com/articles/https/
[Guide de l’utilisateur Docker]:https://docs.docker.com/userguide/
