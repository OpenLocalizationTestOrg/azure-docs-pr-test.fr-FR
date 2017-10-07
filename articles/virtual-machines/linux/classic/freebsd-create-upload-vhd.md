---
title: "aaaCreate et télécharger un VM FreeBSD image | Documents Microsoft"
description: "En savoir plus toocreate et téléchargez un disque dur virtuel (VHD) qui contient le toocreate de système d’exploitation FreeBSD hello une machine virtuelle Azure"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ef30f32-61c1-4ba8-9542-801d7b18e9bf
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: kyliel
ms.openlocfilehash: f3bd155e496f1a2713d36bb66ea9824ed4c210ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-a-freebsd-vhd-tooazure"></a>Créer et télécharger un tooAzure FreeBSD VHD
Cet article vous explique comment toocreate et téléchargez un disque dur virtuel (VHD) qui contient hello système d’exploitation de FreeBSD. Après que l’avoir téléchargée, vous pouvez l’utiliser en tant que vos propres toocreate image un ordinateur virtuel (VM) dans Azure.

> [!IMPORTANT] 
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. Pour plus d’informations sur le téléchargement d’un disque dur virtuel à l’aide du modèle de gestionnaire de ressources hello, consultez [ici](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="prerequisites"></a>Composants requis
Cet article suppose que vous avez hello éléments suivants :

* **Abonnement Azure**: si vous ne possédez pas de compte, vous pouvez en créer un en quelques minutes. Si vous disposez d’un abonnement MSDN, consultez [Crédit Azure mensuel pour les abonnés Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/). Dans le cas contraire, découvrez comment trop[créer un compte d’évaluation gratuit](https://azure.microsoft.com/pricing/free-trial/).  
* **Outils Azure PowerShell**--module Azure PowerShell de hello doit être installé et configuré toouse votre abonnement Azure. module de hello toodownload, consultez [téléchargements Azure](https://azure.microsoft.com/downloads/). Un didacticiel décrivant comment tooinstall et configurer le module de hello est disponible ici. Hello d’utilisation [téléchargements Azure](https://azure.microsoft.com/downloads/) applet de commande hello de tooupload disque dur virtuel.
* **Système d’exploitation FreeBSD dans un fichier .vhd**--un système d’exploitation FreeBSD pris en charge doit être un disque dur virtuel tooa installé. Plusieurs outils existent toocreate les fichiers .vhd. Par exemple, vous pouvez utiliser une solution de virtualisation tels que les fichiers de disque dur virtuel Hyper-V toocreate hello et installer le système d’exploitation de hello. Pour obtenir des instructions sur la façon dont tooinstall et l’utilisation de Hyper-V, consultez [installer Hyper-V et créer une machine virtuelle](http://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> nouveau format VHDX de Hello n’est pas pris en charge dans Azure. Vous pouvez convertir le format de tooVHD hello disque à l’aide du Gestionnaire Hyper-V ou hello applet de commande [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx). En outre, il existe un [didacticiel sur le site MSDN sur la façon toouse FreeBSD avec Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).
>
>

Cette tâche inclut hello cinq comme suit :

## <a name="step-1-prepare-hello-image-for-upload"></a>Étape 1 : Préparer l’image de hello pour le téléchargement
Sur la machine virtuelle du hello où vous avez installé le système d’exploitation de FreeBSD hello, procédez hello procédures suivantes :

1. Activez DHCP.

        # echo 'ifconfig_hn0="SYNCDHCP"' >> /etc/rc.conf
        # service netif restart
2. Activez SSH.

    Vérifiez le serveur SSH hello est installé et configuré toostart au moment du démarrage. Il est activé par défaut après l’installation à partir du disque FreeBSD. 
3. Configurez une console série.

        # echo 'console="comconsole vidconsole"' >> /boot/loader.conf
        # echo 'comconsole_speed="115200"' >> /boot/loader.conf
4. Installez sudo.

    compte de racine Hello est désactivé dans Azure. Cela signifie que vous avez besoin de sudo tooutilize une une des commandes toorun utilisateur non privilégié avec des privilèges élevés.

        # pkg install sudo
   
5. Composants requis pour l'Agent Azure.

        # pkg install python27  
        # pkg install Py27-setuptools  
        # ln -s /usr/local/bin/python2.7 /usr/bin/python   
        # pkg install git
6. Installez l’Agent Azure.

    Hello dernière version de hello Azure Agent peut toujours être trouvée sur [github](https://github.com/Azure/WALinuxAgent/releases). Hello version 2.0.10 + prend officiellement en charge FreeBSD 10 & 10.1 et version hello 2.1.4 + (y compris 2.2.x) prend officiellement en charge FreeBSD 10.2 et versions ultérieures.

        # git clone https://github.com/Azure/WALinuxAgent.git  
        # cd WALinuxAgent  
        # git tag  
        …
        WALinuxAgent-2.0.16
        …
        v2.1.4
        v2.1.4.rc0
        v2.1.4.rc1

    Pour la version 2.0, utilisons 2.0.16 comme exemple :

        # git checkout WALinuxAgent-2.0.16
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  

    Pour la version 2.1, utilisons 2.1.4 comme exemple :

        # git checkout v2.1.4
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  
        # ln -sf /usr/local/sbin/waagent2.0 /usr/sbin/waagent2.0

   > [!IMPORTANT]
   > Après avoir installé l’Agent Azure, il est tooverify une bonne idée qu’il est en cours d’exécution :
   >
   >

        # waagent -version
        WALinuxAgent-2.1.4 running on freebsd 10.3
        Python: 2.7.11
        # ps auxw | grep waagent
        root   639   0.0  0.5 104620 17520 u0- I    05:17    0:00.20 python /usr/local/sbin/waagent -daemon (python2.7)
        # cat /var/log/waagent.log
7. Annuler le déploiement de système de hello.

    Annuler le déploiement hello système tooclean et elle est adaptée à la préparation. Hello commande suivante supprime également dernier compte d’utilisateur configuré hello et les données de salutation associée :

        # echo "y" |  /usr/local/sbin/waagent -deprovision+user  
        # echo  'waagent_enable="YES"' >> /etc/rc.conf

    Vous pouvez à présent arrêter votre machine virtuelle.

## <a name="step-2-create-a-storage-account-in-azure"></a>Étape 2 : création d'un compte de stockage dans Azure
Vous avez besoin d’un compte de stockage dans un fichier .vhd de tooupload Azure afin qu’il peut être utilisé toocreate une machine virtuelle. Vous pouvez utiliser hello toocreate portail classique Azure un compte de stockage.

1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com).
2. Dans la barre de commandes hello, sélectionnez **nouveau**.
3. Sélectionnez **Services de données** > **Stockage** > **Création rapide**.

    ![Créer rapidement un compte de stockage](./media/freebsd-create-upload-vhd/Storage-quick-create.png)
4. Complétez les champs de hello comme suit :

   * Bonjour **URL** , tapez un toouse de nom de sous-domaine dans l’URL du compte de stockage hello. Hello peut comporter de 3 à 24 chiffres et des lettres minuscules. Ce nom devient le nom d’hôte hello dans URL hello tooaddress utilisé le stockage Blob Azure, le stockage de file d’attente Azure ou des ressources de stockage Azure Table pour l’abonnement de hello.
   * Bonjour **emplacement/groupe d’affinités** menu déroulant, choisissez hello **groupe d’affinités ou emplacement** hello compte de stockage. Un groupe d’affinités vous permet de placer vos services cloud et le stockage Bonjour même centre de données.
   * Bonjour **réplication** champ, de décider si toouse **géo-redondant** réplication hello compte de stockage. La géo-réplication est activée par défaut. Cette option réplique vos données tooa secondaire emplacement, aucun coût de tooyou, afin que votre stockage bascule toothat emplacement si une défaillance majeure se produit au niveau de l’emplacement principal de hello. emplacement secondaire de Hello est affecté automatiquement et ne peut pas être modifié. Si vous avez besoin de davantage de contrôle sur l’emplacement de hello de votre stockage en cloud en raison des exigences de toolegal ou de la stratégie de l’organisation, vous pouvez désactiver la géo-réplication. Toutefois, n’oubliez pas que si vous activez ultérieurement géo-réplication, vous serez facturé un unique votre emplacement secondaire d’existant données toohello tooreplicate des frais de transfert de données. Vous pouvez bénéficier d’une réduction pour les services de stockage sans géo-réplication. Vous trouverez plus d'informations sur la gestion de la géoréplication des comptes de stockage ici : [Réplication Azure Storage](../../../storage/common/storage-redundancy.md).

     ![Entrer les détails du compte de stockage](./media/freebsd-create-upload-vhd/Storage-create-account.png)
5. Sélectionnez **Créer un compte de stockage**. Hello compte apparaît désormais sous **stockage**.

    ![Compte de stockage correctement créé](./media/freebsd-create-upload-vhd/Storagenewaccount.png)
6. Ensuite, créez un conteneur pour vos fichiers .vhd téléchargés. Sélectionnez le nom de compte de stockage hello et sélectionnez **conteneurs**.

    ![Détails du compte de stockage](./media/freebsd-create-upload-vhd/storageaccount_detail.png)
7. Sélectionnez **Créer un conteneur**.

    ![Détails du compte de stockage](./media/freebsd-create-upload-vhd/storageaccount_container.png)
8. Bonjour **nom** , tapez un nom pour votre conteneur. Ensuite, dans hello **accès** menu déroulant, sélectionnez le type de stratégie d’accès.

    ![Nom du conteneur](./media/freebsd-create-upload-vhd/storageaccount_containervalues.png)

   > [!NOTE]
   > Par défaut, le conteneur de hello est privé et sont accessibles par le propriétaire du compte hello. accès en lecture public de tooallow toohello objets BLOB dans le conteneur de hello, mais pas les propriétés de conteneur toohello et des métadonnées, utilisent hello **objet Blob Public** option. accès en lecture public complet de tooallow pour hello conteneur et les objets BLOB, utilisez hello **conteneur Public** option.
   >
   >

## <a name="step-3-prepare-hello-connection-tooazure"></a>Étape 3 : Préparer hello connexion tooAzure
Avant de pouvoir télécharger un fichier .vhd, vous devez tooestablish une connexion sécurisée entre votre ordinateur et votre abonnement Azure. Vous pouvez utiliser la méthode d’Azure Active Directory (Azure AD) hello ou hello certificat méthode toodo il.

### <a name="use-hello-azure-ad-method-tooupload-a-vhd-file"></a>Utilisez tooupload de méthode hello Azure AD un fichier .vhd
1. Console Azure PowerShell hello ouvert.
2. Tapez hello de commande suivante :  
    `Add-AzureAccount`

    Cette commande ouvre une fenêtre de connexion qui vous permet de vous connecter avec votre compte professionnel ou scolaire.

    ![Fenêtre PowerShell](./media/freebsd-create-upload-vhd/add_azureaccount.png)
3. Azure authentifie et enregistre les informations d’identification de hello. Puis il ferme la fenêtre hello.

### <a name="use-hello-certificate-method-tooupload-a-vhd-file"></a>Utilisez tooupload de méthode hello certificat un fichier .vhd
1. Console Azure PowerShell hello ouvert.
2. Saisissez : `Get-AzurePublishSettingsFile`.
3. Une fenêtre de navigateur s’ouvre et vous invite à entrer vous toodownload hello fichier .publishsettings. Ce fichier contient des informations et un certificat pour votre abonnement Azure.

    ![Page de téléchargement du navigateur](./media/freebsd-create-upload-vhd/Browser_download_GetPublishSettingsFile.png)
4. Enregistrez le fichier .publishsettings de hello.
5. Type : `Import-AzurePublishSettingsFile <PathToFile>`, où `<PathToFile>` est le fichier .publishsettings de hello chemin d’accès complet toohello.

   Pour plus d'informations, consultez la page [Prise en main des applets de commande Azure](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx).

   Pour plus d’informations sur l’installation et configuration de PowerShell, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).

## <a name="step-4-upload-hello-vhd-file"></a>Étape 4 : Téléchargez le fichier .vhd de hello
Lorsque vous téléchargez le fichier .vhd de hello, vous pouvez le placer n’importe où dans votre stockage d’objets Blob. Voici certains termes que vous utiliserez lorsque vous téléchargez le fichier de hello :

* **BlobStorageURL** est hello URL hello compte de stockage que vous avez créé à l’étape 2.
* **YourImagesFolder** est conteneur hello dans le stockage d’objets Blob dans lequel vous souhaitez que toostore vos images.
* **VHDName** hello étiquette qui apparaît dans le disque dur virtuel de hello tooidentify de portail classique Azure hello.
* **PathToVHDFile** est le chemin d’accès complet de hello et nom du fichier .vhd de hello.

À partir de la fenêtre d’Azure PowerShell hello utilisé à l’étape précédente de hello, tapez :

        Add-AzureVhd -Destination "<BlobStorageURL>/<YourImagesFolder>/<VHDName>.vhd" -LocalFilePath <PathToVHDFile>

## <a name="step-5-create-a-vm-with-hello-uploaded-vhd-file"></a>Étape 5 : Créer un ordinateur virtuel avec un fichier .vhd téléchargé de hello
Après avoir téléchargé le fichier .vhd de hello, vous pouvez l’ajouter en tant qu’une liste d’images toohello d’images personnalisées qui sont associés à votre abonnement et créer une machine virtuelle avec cette image personnalisée.

1. À partir de la fenêtre d’Azure PowerShell hello utilisé à l’étape précédente de hello, tapez :

        Add-AzureVMImage -ImageName <Your Image's Name> -MediaLocation <location of hello VHD> -OS <Type of hello OS on hello VHD>

   > [!NOTE]
   > Utilisez Linux en tant que type de système d’exploitation hello. version d’Azure PowerShell actuelle Hello accepte uniquement « Linux » ou « Windows » en tant que paramètre.
   >
   >
2. Après avoir effectué les étapes précédentes hello, la nouvelle image de hello est répertoriée lorsque vous choisissez hello **Images** onglet hello portail Azure classic.  

    ![Choose an image](./media/freebsd-create-upload-vhd/addfreebsdimage.png)
3. Créer un ordinateur virtuel à partir de la galerie de hello. Cette nouvelle image est maintenant disponible sous **Mes Images**.
4. Sélectionnez la nouvelle image de hello. Ensuite, accédez à hello invite tooset un nom d’hôte, un mot de passe, clé SSH, et ainsi de suite.

    ![Image personnalisée](./media/freebsd-create-upload-vhd/createfreebsdimageinazure.png)
5. Après avoir terminé la configuration de hello, vous verrez votre VM FreeBSD s’exécutant dans Azure.

    ![Image FreeBSD dans Azure](./media/freebsd-create-upload-vhd/freebsdimageinazure.png)
