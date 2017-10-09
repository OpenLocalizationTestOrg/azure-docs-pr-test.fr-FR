---
title: "aaaSet de votre environnement de développement sur toowork Mac OS X avec Azure Service Fabric | Documents Microsoft"
description: "Installer le runtime de hello, Kit de développement logiciel et les outils et créer un cluster de développement local. Après avoir terminé cette installation, vous serez prêt toobuild des applications sur Mac OS X."
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/21/2017
ms.author: saysa
ms.openlocfilehash: 0b8a6c1fc1871fa76f3e21cefbc7f66f79072797
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-your-development-environment-on-mac-os-x"></a>Configurer votre environnement de développement sur Mac OS X
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md)
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
>
>  

Vous pouvez générer toorun des applications de Service Fabric sur les clusters Linux à l’aide de Mac OS X. Cet article décrit comment tooset de votre Mac pour le développement.

## <a name="prerequisites"></a>Composants requis
L’infrastructure de service ne s’exécute pas en mode natif sur OS X. toorun un cluster Service Fabric local, nous fournir l’ordinateur virtuel préconfiguré Ubuntu à l’aide de Vagrant et VirtualBox. Avant de commencer, vous avez besoin des éléments suivants :

* [Vagrant (v1.8.4 ou version ultérieure)](http://www.vagrantup.com/downloads.html)
* [VirtualBox](http://www.virtualbox.org/wiki/Downloads)

>[!NOTE]
> Vous devez toouse mutuellement pris en charge les versions de Vagrant et VirtualBox. Vagrant peut avoir un comportement erratique sur une version non prise en charge de VirtualBox.
>

## <a name="create-hello-local-vm"></a>Créer hello VM locale
toocreate hello local machine virtuelle contenant un cluster Service Fabric 5, effectuez les hello comme suit :

1. Hello du clone `Vagrantfile` référentiel

    ```bash
    git clone https://github.com/azure/service-fabric-linux-vagrant-onebox.git
    ```
    Cette procédure mettre downloads hello fichier `Vagrantfile` contenant hello VM configuration ainsi que de hello d’emplacement hello machine virtuelle est téléchargée depuis.

2. Accédez toohello le clone local de dépôt de hello

    ```bash
    cd service-fabric-linux-vagrant-onebox
    ```
3. (Facultatif) Modifier les paramètres de machine virtuelle par défaut hello

    Par défaut, hello local machine virtuelle est configurée comme suit :

   * 3 Go de mémoire allouée
   * Réseau privé hôte configuré sur l’IP 192.168.50.50 l’activation de relais du trafic de l’hôte de Mac hello

     Vous pouvez modifier une de ces paramètres ou ajouter d’autres toohello configuration VM Bonjour `Vagrantfile`. Consultez hello [documentation de Vagrant](http://www.vagrantup.com/docs) pour la liste complète des options de configuration hello.
4. Créer hello machine virtuelle

    ```bash
    vagrant up
    ```

   Cette étape télécharge l’image de machine virtuelle hello préconfiguré, démarrage du cluster local, puis configurer une infrastructure de Service local qu’il contient. Vous devez prévoir il tootake quelques minutes. Si le programme d’installation se termine correctement, vous consultez un message dans la sortie de hello indiquant le que démarrage de ce cluster hello.

    ![La configuration du cluster démarre après l’approvisionnement de la machine virtuelle][cluster-setup-script]

    >[!TIP]
    > Si le téléchargement de machine virtuelle hello prend beaucoup de temps, vous pouvez le télécharger à l’aide de wget ou curl ou via un navigateur en parcourant le lien toohello spécifié par **config.vm.box_url** dans le fichier de hello `Vagrantfile`. Après l’avoir téléchargé localement, modifier `Vagrantfile` toopoint toohello chemin d’accès local où vous avez téléchargé l’image de hello. Pour exemple si vous avez téléchargé hello image too/home/users/test/azureservicefabric.tp8.box, puis définissez **config.vm.box_url** toothat chemin.
    >

5. Tester ce hello cluster a été correctement configuré en accédant tooService Fabric Explorer dans http://192.168.50.50:19080/Explorateur (en supposant que vous avez conservé l’adresse IP de réseau privé hello par défaut).

    ![Service Fabric Explorer affichés à partir de l’hôte hello Mac][sfx-mac]


## <a name="create-application-on-mac-using-yeoman"></a>Créer l’application sur Mac à l’aide de Yeoman
Service Fabric fournit des outils de génération de modèles automatique qui vous aideront à créer une application Service Fabric depuis un terminal à l’aide du générateur de modèles Yeoman. Veuillez suivre les étapes de hello ci-dessous tooensure que vous possédez Générateur de modèle yeoman Service Fabric hello vous travaillez sur votre ordinateur.

1. Vous devez toohave Node.js et NPM installé sur le mac vous. Si ce n’est pas le cas, vous pouvez installer Node.js et NPM à l’aide de Homebrew utilisant hello. versions de hello toocheck de Node.js et NPM installé sur votre Mac, vous pouvez utiliser hello ``-v`` option.

  ```bash
  brew install node
  node -v
  npm -v
  ```
2. Installer le générateur de modèles [Yeoman](http://yeoman.io/) sur votre machine à partir de NPM

  ```bash
  npm install -g yo
  ```
3. Installer hello Yeoman générateur souhaité toouse, hello comme suit dans la mise en route de hello [documentation](service-fabric-get-started-linux.md). Applications de l’infrastructure de Service toocreate Yeoman, à l’aide de la procédure hello-

  ```bash
  npm install -g generator-azuresfjava       # for Service Fabric Java Applications
  npm install -g generator-azuresfguest      # for Service Fabric Guest executables
  npm install -g generator-azuresfcontainer  # for Service Fabric Container Applications
  ```
4. toobuild une application Java de l’infrastructure de Service sur le Mac, vous devriez - JDK 1.8 et Gradle installé sur l’ordinateur de hello.


## <a name="install-hello-service-fabric-plugin-for-eclipse-neon"></a>Installer le plug-in de hello Service Fabric pour Eclipse Neon

L’infrastructure de service fournit un plug-in pour hello **Neon Eclipse pour Java IDE** qui peuvent simplifier le processus de hello de création, la création et déploiement des services de Java. Vous pouvez suivre les étapes d’installation hello mentionnés dans cette général [documentation](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) sur l’installation ou la mise à jour du plug-in Eclipse de l’infrastructure de Service.

>[!TIP]
> Par défaut nous prenons en charge hello par défaut IP comme indiqué dans hello ``Vagrantfile`` Bonjour ``Local.json`` de l’application hello généré. Si vous modifiez qui et déployez Vagrant avec une autre adresse IP, mettez à jour hello adresse IP correspondante dans ``Local.json`` de votre application.

## <a name="next-steps"></a>Étapes suivantes
<!-- Links -->
* [Create and deploy your first Service Fabric Java application on Linux using Yeoman (Créer et déployer votre première application Java Service Fabric sur Linux à l’aide de Yeoman)](service-fabric-create-your-first-linux-application-with-java.md)
* [Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse (Créer et déployer votre première application Java Service Fabric sur Linux à l’aide du plug-in Service Fabric pour Eclipse)](service-fabric-get-started-eclipse.md)
* [Créer un cluster Service Fabric Bonjour portail Azure](service-fabric-cluster-creation-via-portal.md)
* [Créer un cluster Service Fabric à l’aide de hello Azure Resource Manager](service-fabric-cluster-creation-via-arm.md)
* [Comprendre le modèle d’application hello Service Fabric](service-fabric-application-model.md)

<!-- Images -->
[cluster-setup-script]: ./media/service-fabric-get-started-mac/cluster-setup-mac.png
[sfx-mac]: ./media/service-fabric-get-started-mac/sfx-mac.png
[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-mac/sf-eclipse-plugin-install.png
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
