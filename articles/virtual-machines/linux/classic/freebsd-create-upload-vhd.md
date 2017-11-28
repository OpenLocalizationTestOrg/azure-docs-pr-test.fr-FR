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
# <a name="create-and-upload-a-freebsd-vhd-tooazure"></a><span data-ttu-id="ec4f5-103">Créer et télécharger un tooAzure FreeBSD VHD</span><span class="sxs-lookup"><span data-stu-id="ec4f5-103">Create and upload a FreeBSD VHD tooAzure</span></span>
<span data-ttu-id="ec4f5-104">Cet article vous explique comment toocreate et téléchargez un disque dur virtuel (VHD) qui contient hello système d’exploitation de FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-104">This article shows you how toocreate and upload a virtual hard disk (VHD) that contains hello FreeBSD operating system.</span></span> <span data-ttu-id="ec4f5-105">Après que l’avoir téléchargée, vous pouvez l’utiliser en tant que vos propres toocreate image un ordinateur virtuel (VM) dans Azure.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-105">After you upload it, you can use it as your own image toocreate a virtual machine (VM) in Azure.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="ec4f5-106">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ec4f5-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ec4f5-107">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="ec4f5-108">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="ec4f5-109">Pour plus d’informations sur le téléchargement d’un disque dur virtuel à l’aide du modèle de gestionnaire de ressources hello, consultez [ici](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ec4f5-109">For information about uploading a VHD using hello Resource Manager model, see [here](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec4f5-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ec4f5-110">Prerequisites</span></span>
<span data-ttu-id="ec4f5-111">Cet article suppose que vous avez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ec4f5-111">This article assumes that you have hello following items:</span></span>

* <span data-ttu-id="ec4f5-112">**Abonnement Azure**: si vous ne possédez pas de compte, vous pouvez en créer un en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-112">**An Azure subscription**--If you don't have an account, you can create one in just a couple of minutes.</span></span> <span data-ttu-id="ec4f5-113">Si vous disposez d’un abonnement MSDN, consultez [Crédit Azure mensuel pour les abonnés Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="ec4f5-113">If you have an MSDN subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="ec4f5-114">Dans le cas contraire, découvrez comment trop[créer un compte d’évaluation gratuit](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ec4f5-114">Otherwise, learn how too[create a free trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span>  
* <span data-ttu-id="ec4f5-115">**Outils Azure PowerShell**--module Azure PowerShell de hello doit être installé et configuré toouse votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-115">**Azure PowerShell tools**--hello Azure PowerShell module must be installed and configured toouse your Azure subscription.</span></span> <span data-ttu-id="ec4f5-116">module de hello toodownload, consultez [téléchargements Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="ec4f5-116">toodownload hello module, see [Azure downloads](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="ec4f5-117">Un didacticiel décrivant comment tooinstall et configurer le module de hello est disponible ici.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-117">A tutorial that describes how tooinstall and configure hello module is available here.</span></span> <span data-ttu-id="ec4f5-118">Hello d’utilisation [téléchargements Azure](https://azure.microsoft.com/downloads/) applet de commande hello de tooupload disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-118">Use hello [Azure Downloads](https://azure.microsoft.com/downloads/) cmdlet tooupload hello VHD.</span></span>
* <span data-ttu-id="ec4f5-119">**Système d’exploitation FreeBSD dans un fichier .vhd**--un système d’exploitation FreeBSD pris en charge doit être un disque dur virtuel tooa installé.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-119">**FreeBSD operating system installed in a .vhd file**--A supported   FreeBSD operating system must be installed tooa virtual hard disk.</span></span> <span data-ttu-id="ec4f5-120">Plusieurs outils existent toocreate les fichiers .vhd.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-120">Multiple tools exist toocreate .vhd files.</span></span> <span data-ttu-id="ec4f5-121">Par exemple, vous pouvez utiliser une solution de virtualisation tels que les fichiers de disque dur virtuel Hyper-V toocreate hello et installer le système d’exploitation de hello.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-121">For example, you can use a virtualization solution such as Hyper-V toocreate hello .vhd file and install hello operating system.</span></span> <span data-ttu-id="ec4f5-122">Pour obtenir des instructions sur la façon dont tooinstall et l’utilisation de Hyper-V, consultez [installer Hyper-V et créer une machine virtuelle](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec4f5-122">For instructions about how tooinstall and use Hyper-V, see [Install Hyper-V and create a virtual machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="ec4f5-123">nouveau format VHDX de Hello n’est pas pris en charge dans Azure.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-123">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="ec4f5-124">Vous pouvez convertir le format de tooVHD hello disque à l’aide du Gestionnaire Hyper-V ou hello applet de commande [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec4f5-124">You can convert hello disk tooVHD format by using Hyper-V Manager or hello cmdlet [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx).</span></span> <span data-ttu-id="ec4f5-125">En outre, il existe un [didacticiel sur le site MSDN sur la façon toouse FreeBSD avec Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec4f5-125">In addition, there is a [tutorial on MSDN about how toouse FreeBSD with Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).</span></span>
>
>

<span data-ttu-id="ec4f5-126">Cette tâche inclut hello cinq comme suit :</span><span class="sxs-lookup"><span data-stu-id="ec4f5-126">This task includes hello following five steps:</span></span>

## <a name="step-1-prepare-hello-image-for-upload"></a><span data-ttu-id="ec4f5-127">Étape 1 : Préparer l’image de hello pour le téléchargement</span><span class="sxs-lookup"><span data-stu-id="ec4f5-127">Step 1: Prepare hello image for upload</span></span>
<span data-ttu-id="ec4f5-128">Sur la machine virtuelle du hello où vous avez installé le système d’exploitation de FreeBSD hello, procédez hello procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="ec4f5-128">On hello virtual machine where you installed hello FreeBSD operating system, complete hello following procedures:</span></span>

1. <span data-ttu-id="ec4f5-129">Activez DHCP.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-129">Enable DHCP.</span></span>

        # echo 'ifconfig_hn0="SYNCDHCP"' >> /etc/rc.conf
        # service netif restart
2. <span data-ttu-id="ec4f5-130">Activez SSH.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-130">Enable SSH.</span></span>

    <span data-ttu-id="ec4f5-131">Vérifiez le serveur SSH hello est installé et configuré toostart au moment du démarrage.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-131">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span> <span data-ttu-id="ec4f5-132">Il est activé par défaut après l’installation à partir du disque FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-132">By default it is enabled after installation from FreeBSD disc.</span></span> 
3. <span data-ttu-id="ec4f5-133">Configurez une console série.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-133">Set up a serial console.</span></span>

        # echo 'console="comconsole vidconsole"' >> /boot/loader.conf
        # echo 'comconsole_speed="115200"' >> /boot/loader.conf
4. <span data-ttu-id="ec4f5-134">Installez sudo.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-134">Install sudo.</span></span>

    <span data-ttu-id="ec4f5-135">compte de racine Hello est désactivé dans Azure.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-135">hello root account is disabled in Azure.</span></span> <span data-ttu-id="ec4f5-136">Cela signifie que vous avez besoin de sudo tooutilize une une des commandes toorun utilisateur non privilégié avec des privilèges élevés.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-136">This means you need tooutilize sudo from an unprivileged user toorun commands with elevated privileges.</span></span>

        # pkg install sudo
   
5. <span data-ttu-id="ec4f5-137">Composants requis pour l'Agent Azure.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-137">Prerequisites for Azure Agent.</span></span>

        # pkg install python27  
        # pkg install Py27-setuptools  
        # ln -s /usr/local/bin/python2.7 /usr/bin/python   
        # pkg install git
6. <span data-ttu-id="ec4f5-138">Installez l’Agent Azure.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-138">Install Azure Agent.</span></span>

    <span data-ttu-id="ec4f5-139">Hello dernière version de hello Azure Agent peut toujours être trouvée sur [github](https://github.com/Azure/WALinuxAgent/releases).</span><span class="sxs-lookup"><span data-stu-id="ec4f5-139">hello latest release of hello Azure Agent can always be found on [github](https://github.com/Azure/WALinuxAgent/releases).</span></span> <span data-ttu-id="ec4f5-140">Hello version 2.0.10 + prend officiellement en charge FreeBSD 10 & 10.1 et version hello 2.1.4 + (y compris 2.2.x) prend officiellement en charge FreeBSD 10.2 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-140">hello version 2.0.10 + officially supports FreeBSD 10 & 10.1, and hello version 2.1.4 + (including 2.2.x) officially supports FreeBSD 10.2 and later releases.</span></span>

        # git clone https://github.com/Azure/WALinuxAgent.git  
        # cd WALinuxAgent  
        # git tag  
        …
        WALinuxAgent-2.0.16
        …
        v2.1.4
        v2.1.4.rc0
        v2.1.4.rc1

    <span data-ttu-id="ec4f5-141">Pour la version 2.0, utilisons 2.0.16 comme exemple :</span><span class="sxs-lookup"><span data-stu-id="ec4f5-141">For 2.0, let's use 2.0.16 as an example:</span></span>

        # git checkout WALinuxAgent-2.0.16
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  

    <span data-ttu-id="ec4f5-142">Pour la version 2.1, utilisons 2.1.4 comme exemple :</span><span class="sxs-lookup"><span data-stu-id="ec4f5-142">For 2.1, let's use 2.1.4 as an example:</span></span>

        # git checkout v2.1.4
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  
        # ln -sf /usr/local/sbin/waagent2.0 /usr/sbin/waagent2.0

   > [!IMPORTANT]
   > <span data-ttu-id="ec4f5-143">Après avoir installé l’Agent Azure, il est tooverify une bonne idée qu’il est en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="ec4f5-143">After you install Azure Agent, it's a good idea tooverify that it's running:</span></span>
   >
   >

        # waagent -version
        WALinuxAgent-2.1.4 running on freebsd 10.3
        Python: 2.7.11
        # ps auxw | grep waagent
        root   639   0.0  0.5 104620 17520 u0- I    05:17    0:00.20 python /usr/local/sbin/waagent -daemon (python2.7)
        # cat /var/log/waagent.log
7. <span data-ttu-id="ec4f5-144">Annuler le déploiement de système de hello.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-144">Deprovision hello system.</span></span>

    <span data-ttu-id="ec4f5-145">Annuler le déploiement hello système tooclean et elle est adaptée à la préparation.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-145">Deprovision hello system tooclean it and make it suitable for reprovisioning.</span></span> <span data-ttu-id="ec4f5-146">Hello commande suivante supprime également dernier compte d’utilisateur configuré hello et les données de salutation associée :</span><span class="sxs-lookup"><span data-stu-id="ec4f5-146">hello following command also deletes hello last provisioned user account and hello associated data:</span></span>

        # echo "y" |  /usr/local/sbin/waagent -deprovision+user  
        # echo  'waagent_enable="YES"' >> /etc/rc.conf

    <span data-ttu-id="ec4f5-147">Vous pouvez à présent arrêter votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-147">Now you can shut down your VM.</span></span>

## <a name="step-2-create-a-storage-account-in-azure"></a><span data-ttu-id="ec4f5-148">Étape 2 : création d'un compte de stockage dans Azure</span><span class="sxs-lookup"><span data-stu-id="ec4f5-148">Step 2: Create a storage account in Azure</span></span>
<span data-ttu-id="ec4f5-149">Vous avez besoin d’un compte de stockage dans un fichier .vhd de tooupload Azure afin qu’il peut être utilisé toocreate une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-149">You need a storage account in Azure tooupload a .vhd file so it can be used toocreate a virtual machine.</span></span> <span data-ttu-id="ec4f5-150">Vous pouvez utiliser hello toocreate portail classique Azure un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-150">You can use hello Azure classic portal toocreate a storage account.</span></span>

1. <span data-ttu-id="ec4f5-151">Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="ec4f5-151">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="ec4f5-152">Dans la barre de commandes hello, sélectionnez **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-152">On hello command bar, select **New**.</span></span>
3. <span data-ttu-id="ec4f5-153">Sélectionnez **Services de données** > **Stockage** > **Création rapide**.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-153">Select **Data Services** > **Storage** > **Quick Create**.</span></span>

    ![Créer rapidement un compte de stockage](./media/freebsd-create-upload-vhd/Storage-quick-create.png)
4. <span data-ttu-id="ec4f5-155">Complétez les champs de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ec4f5-155">Fill out hello fields as follows:</span></span>

   * <span data-ttu-id="ec4f5-156">Bonjour **URL** , tapez un toouse de nom de sous-domaine dans l’URL du compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-156">In hello **URL** field, type a subdomain name toouse in hello storage account URL.</span></span> <span data-ttu-id="ec4f5-157">Hello peut comporter de 3 à 24 chiffres et des lettres minuscules.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-157">hello entry can contain from 3-24 numbers and lowercase letters.</span></span> <span data-ttu-id="ec4f5-158">Ce nom devient le nom d’hôte hello dans URL hello tooaddress utilisé le stockage Blob Azure, le stockage de file d’attente Azure ou des ressources de stockage Azure Table pour l’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-158">This name becomes hello host name within hello URL that is used tooaddress Azure Blob storage, Azure Queue storage, or Azure Table storage resources for hello subscription.</span></span>
   * <span data-ttu-id="ec4f5-159">Bonjour **emplacement/groupe d’affinités** menu déroulant, choisissez hello **groupe d’affinités ou emplacement** hello compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-159">In hello **Location/Affinity Group** drop-down menu, choose hello **location or affinity group** for hello storage account.</span></span> <span data-ttu-id="ec4f5-160">Un groupe d’affinités vous permet de placer vos services cloud et le stockage Bonjour même centre de données.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-160">An affinity group lets you put your cloud services and storage in hello same data center.</span></span>
   * <span data-ttu-id="ec4f5-161">Bonjour **réplication** champ, de décider si toouse **géo-redondant** réplication hello compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-161">In hello **Replication** field, decide whether toouse **Geo-Redundant** replication for hello storage account.</span></span> <span data-ttu-id="ec4f5-162">La géo-réplication est activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-162">Geo-replication is turned on by default.</span></span> <span data-ttu-id="ec4f5-163">Cette option réplique vos données tooa secondaire emplacement, aucun coût de tooyou, afin que votre stockage bascule toothat emplacement si une défaillance majeure se produit au niveau de l’emplacement principal de hello.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-163">This option replicates your data tooa secondary location, at no cost tooyou, so that your storage fails over toothat location if a major failure occurs at hello primary location.</span></span> <span data-ttu-id="ec4f5-164">emplacement secondaire de Hello est affecté automatiquement et ne peut pas être modifié.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-164">hello secondary location is assigned automatically and can't be changed.</span></span> <span data-ttu-id="ec4f5-165">Si vous avez besoin de davantage de contrôle sur l’emplacement de hello de votre stockage en cloud en raison des exigences de toolegal ou de la stratégie de l’organisation, vous pouvez désactiver la géo-réplication.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-165">If you need more control over hello location of your cloud-based storage due toolegal requirements or organizational policy, you can turn off geo-replication.</span></span> <span data-ttu-id="ec4f5-166">Toutefois, n’oubliez pas que si vous activez ultérieurement géo-réplication, vous serez facturé un unique votre emplacement secondaire d’existant données toohello tooreplicate des frais de transfert de données.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-166">However, be aware that if you later turn on geo-replication, you will be charged a one-time data transfer fee tooreplicate your existing data toohello secondary location.</span></span> <span data-ttu-id="ec4f5-167">Vous pouvez bénéficier d’une réduction pour les services de stockage sans géo-réplication.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-167">Storage services without geo-replication are offered at a discount.</span></span> <span data-ttu-id="ec4f5-168">Vous trouverez plus d'informations sur la gestion de la géoréplication des comptes de stockage ici : [Réplication Azure Storage](../../../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="ec4f5-168">More details about managing geo-replication of storage accounts can be found here: [Azure Storage replication](../../../storage/common/storage-redundancy.md).</span></span>

     ![Entrer les détails du compte de stockage](./media/freebsd-create-upload-vhd/Storage-create-account.png)
5. <span data-ttu-id="ec4f5-170">Sélectionnez **Créer un compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-170">Select **Create Storage Account**.</span></span> <span data-ttu-id="ec4f5-171">Hello compte apparaît désormais sous **stockage**.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-171">hello account now appears under **storage**.</span></span>

    ![Compte de stockage correctement créé](./media/freebsd-create-upload-vhd/Storagenewaccount.png)
6. <span data-ttu-id="ec4f5-173">Ensuite, créez un conteneur pour vos fichiers .vhd téléchargés.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-173">Next, create a container for your uploaded .vhd files.</span></span> <span data-ttu-id="ec4f5-174">Sélectionnez le nom de compte de stockage hello et sélectionnez **conteneurs**.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-174">Select hello storage account name, and then select **Containers**.</span></span>

    ![Détails du compte de stockage](./media/freebsd-create-upload-vhd/storageaccount_detail.png)
7. <span data-ttu-id="ec4f5-176">Sélectionnez **Créer un conteneur**.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-176">Select **Create a Container**.</span></span>

    ![Détails du compte de stockage](./media/freebsd-create-upload-vhd/storageaccount_container.png)
8. <span data-ttu-id="ec4f5-178">Bonjour **nom** , tapez un nom pour votre conteneur.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-178">In hello **Name** field, type a name for your container.</span></span> <span data-ttu-id="ec4f5-179">Ensuite, dans hello **accès** menu déroulant, sélectionnez le type de stratégie d’accès.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-179">Then, in hello **Access** drop-down menu, select what type of access policy you want.</span></span>

    ![Nom du conteneur](./media/freebsd-create-upload-vhd/storageaccount_containervalues.png)

   > [!NOTE]
   > <span data-ttu-id="ec4f5-181">Par défaut, le conteneur de hello est privé et sont accessibles par le propriétaire du compte hello.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-181">By default, hello container is private and can only be accessed by hello account owner.</span></span> <span data-ttu-id="ec4f5-182">accès en lecture public de tooallow toohello objets BLOB dans le conteneur de hello, mais pas les propriétés de conteneur toohello et des métadonnées, utilisent hello **objet Blob Public** option.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-182">tooallow public read access toohello blobs in hello container, but not toohello container properties and metadata, use hello **Public Blob** option.</span></span> <span data-ttu-id="ec4f5-183">accès en lecture public complet de tooallow pour hello conteneur et les objets BLOB, utilisez hello **conteneur Public** option.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-183">tooallow full public read access for hello container and blobs, use hello **Public Container** option.</span></span>
   >
   >

## <a name="step-3-prepare-hello-connection-tooazure"></a><span data-ttu-id="ec4f5-184">Étape 3 : Préparer hello connexion tooAzure</span><span class="sxs-lookup"><span data-stu-id="ec4f5-184">Step 3: Prepare hello connection tooAzure</span></span>
<span data-ttu-id="ec4f5-185">Avant de pouvoir télécharger un fichier .vhd, vous devez tooestablish une connexion sécurisée entre votre ordinateur et votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-185">Before you can upload a .vhd file, you need tooestablish a secure connection between your computer and your Azure subscription.</span></span> <span data-ttu-id="ec4f5-186">Vous pouvez utiliser la méthode d’Azure Active Directory (Azure AD) hello ou hello certificat méthode toodo il.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-186">You can use hello Azure Active Directory (Azure AD) method or hello certificate method toodo it.</span></span>

### <a name="use-hello-azure-ad-method-tooupload-a-vhd-file"></a><span data-ttu-id="ec4f5-187">Utilisez tooupload de méthode hello Azure AD un fichier .vhd</span><span class="sxs-lookup"><span data-stu-id="ec4f5-187">Use hello Azure AD method tooupload a .vhd file</span></span>
1. <span data-ttu-id="ec4f5-188">Console Azure PowerShell hello ouvert.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-188">Open hello Azure PowerShell console.</span></span>
2. <span data-ttu-id="ec4f5-189">Tapez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ec4f5-189">Type hello following command:</span></span>  
    `Add-AzureAccount`

    <span data-ttu-id="ec4f5-190">Cette commande ouvre une fenêtre de connexion qui vous permet de vous connecter avec votre compte professionnel ou scolaire.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-190">This command opens a sign-in window where you can sign in with your work or school account.</span></span>

    ![Fenêtre PowerShell](./media/freebsd-create-upload-vhd/add_azureaccount.png)
3. <span data-ttu-id="ec4f5-192">Azure authentifie et enregistre les informations d’identification de hello.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-192">Azure authenticates and saves hello credential information.</span></span> <span data-ttu-id="ec4f5-193">Puis il ferme la fenêtre hello.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-193">Then it closes hello window.</span></span>

### <a name="use-hello-certificate-method-tooupload-a-vhd-file"></a><span data-ttu-id="ec4f5-194">Utilisez tooupload de méthode hello certificat un fichier .vhd</span><span class="sxs-lookup"><span data-stu-id="ec4f5-194">Use hello certificate method tooupload a .vhd file</span></span>
1. <span data-ttu-id="ec4f5-195">Console Azure PowerShell hello ouvert.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-195">Open hello Azure PowerShell console.</span></span>
2. <span data-ttu-id="ec4f5-196">Saisissez : `Get-AzurePublishSettingsFile`.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-196">Type:  `Get-AzurePublishSettingsFile`.</span></span>
3. <span data-ttu-id="ec4f5-197">Une fenêtre de navigateur s’ouvre et vous invite à entrer vous toodownload hello fichier .publishsettings.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-197">A browser window opens and prompts you toodownload hello .publishsettings file.</span></span> <span data-ttu-id="ec4f5-198">Ce fichier contient des informations et un certificat pour votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-198">This file contains information and a certificate for your Azure subscription.</span></span>

    ![Page de téléchargement du navigateur](./media/freebsd-create-upload-vhd/Browser_download_GetPublishSettingsFile.png)
4. <span data-ttu-id="ec4f5-200">Enregistrez le fichier .publishsettings de hello.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-200">Save hello .publishsettings file.</span></span>
5. <span data-ttu-id="ec4f5-201">Type : `Import-AzurePublishSettingsFile <PathToFile>`, où `<PathToFile>` est le fichier .publishsettings de hello chemin d’accès complet toohello.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-201">Type:  `Import-AzurePublishSettingsFile <PathToFile>`, where `<PathToFile>` is hello full path toohello .publishsettings file.</span></span>

   <span data-ttu-id="ec4f5-202">Pour plus d'informations, consultez la page [Prise en main des applets de commande Azure](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec4f5-202">For more information, see [Get started with Azure cmdlets](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx).</span></span>

   <span data-ttu-id="ec4f5-203">Pour plus d’informations sur l’installation et configuration de PowerShell, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ec4f5-203">For more information about installing and configuring PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="step-4-upload-hello-vhd-file"></a><span data-ttu-id="ec4f5-204">Étape 4 : Téléchargez le fichier .vhd de hello</span><span class="sxs-lookup"><span data-stu-id="ec4f5-204">Step 4: Upload hello .vhd file</span></span>
<span data-ttu-id="ec4f5-205">Lorsque vous téléchargez le fichier .vhd de hello, vous pouvez le placer n’importe où dans votre stockage d’objets Blob.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-205">When you upload hello .vhd file, you can place it anywhere within your Blob storage.</span></span> <span data-ttu-id="ec4f5-206">Voici certains termes que vous utiliserez lorsque vous téléchargez le fichier de hello :</span><span class="sxs-lookup"><span data-stu-id="ec4f5-206">Following are some terms you will use when you upload hello file:</span></span>

* <span data-ttu-id="ec4f5-207">**BlobStorageURL** est hello URL hello compte de stockage que vous avez créé à l’étape 2.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-207">**BlobStorageURL** is hello URL for hello storage account that you created in Step 2.</span></span>
* <span data-ttu-id="ec4f5-208">**YourImagesFolder** est conteneur hello dans le stockage d’objets Blob dans lequel vous souhaitez que toostore vos images.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-208">**YourImagesFolder** is hello container within Blob storage where you want toostore your images.</span></span>
* <span data-ttu-id="ec4f5-209">**VHDName** hello étiquette qui apparaît dans le disque dur virtuel de hello tooidentify de portail classique Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-209">**VHDName** is hello label that appears in hello Azure classic portal tooidentify hello virtual hard disk.</span></span>
* <span data-ttu-id="ec4f5-210">**PathToVHDFile** est le chemin d’accès complet de hello et nom du fichier .vhd de hello.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-210">**PathToVHDFile** is hello full path and name of hello .vhd file.</span></span>

<span data-ttu-id="ec4f5-211">À partir de la fenêtre d’Azure PowerShell hello utilisé à l’étape précédente de hello, tapez :</span><span class="sxs-lookup"><span data-stu-id="ec4f5-211">From hello Azure PowerShell window you used in hello previous step, type:</span></span>

        Add-AzureVhd -Destination "<BlobStorageURL>/<YourImagesFolder>/<VHDName>.vhd" -LocalFilePath <PathToVHDFile>

## <a name="step-5-create-a-vm-with-hello-uploaded-vhd-file"></a><span data-ttu-id="ec4f5-212">Étape 5 : Créer un ordinateur virtuel avec un fichier .vhd téléchargé de hello</span><span class="sxs-lookup"><span data-stu-id="ec4f5-212">Step 5: Create a VM with hello uploaded .vhd file</span></span>
<span data-ttu-id="ec4f5-213">Après avoir téléchargé le fichier .vhd de hello, vous pouvez l’ajouter en tant qu’une liste d’images toohello d’images personnalisées qui sont associés à votre abonnement et créer une machine virtuelle avec cette image personnalisée.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-213">After you upload hello .vhd file, you can add it as an image toohello list of custom images that are associated with your subscription and create a virtual machine with this custom image.</span></span>

1. <span data-ttu-id="ec4f5-214">À partir de la fenêtre d’Azure PowerShell hello utilisé à l’étape précédente de hello, tapez :</span><span class="sxs-lookup"><span data-stu-id="ec4f5-214">From hello Azure PowerShell window you used in hello previous step, type:</span></span>

        Add-AzureVMImage -ImageName <Your Image's Name> -MediaLocation <location of hello VHD> -OS <Type of hello OS on hello VHD>

   > [!NOTE]
   > <span data-ttu-id="ec4f5-215">Utilisez Linux en tant que type de système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-215">Use Linux as hello OS type.</span></span> <span data-ttu-id="ec4f5-216">version d’Azure PowerShell actuelle Hello accepte uniquement « Linux » ou « Windows » en tant que paramètre.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-216">hello current Azure PowerShell version accepts only “Linux” or “Windows” as a parameter.</span></span>
   >
   >
2. <span data-ttu-id="ec4f5-217">Après avoir effectué les étapes précédentes hello, la nouvelle image de hello est répertoriée lorsque vous choisissez hello **Images** onglet hello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-217">After you complete hello previous steps, hello new image is listed when you choose hello **Images** tab on hello Azure classic portal.</span></span>  

    ![Choose an image](./media/freebsd-create-upload-vhd/addfreebsdimage.png)
3. <span data-ttu-id="ec4f5-219">Créer un ordinateur virtuel à partir de la galerie de hello.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-219">Create a virtual machine from hello gallery.</span></span> <span data-ttu-id="ec4f5-220">Cette nouvelle image est maintenant disponible sous **Mes Images**.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-220">This new image is now available under **My Images**.</span></span>
4. <span data-ttu-id="ec4f5-221">Sélectionnez la nouvelle image de hello.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-221">Select hello new image.</span></span> <span data-ttu-id="ec4f5-222">Ensuite, accédez à hello invite tooset un nom d’hôte, un mot de passe, clé SSH, et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-222">Next, go through hello prompts tooset up a host name, password, SSH key, and so on.</span></span>

    ![Image personnalisée](./media/freebsd-create-upload-vhd/createfreebsdimageinazure.png)
5. <span data-ttu-id="ec4f5-224">Après avoir terminé la configuration de hello, vous verrez votre VM FreeBSD s’exécutant dans Azure.</span><span class="sxs-lookup"><span data-stu-id="ec4f5-224">After you complete hello provisioning, you'll see your FreeBSD VM running in Azure.</span></span>

    ![Image FreeBSD dans Azure](./media/freebsd-create-upload-vhd/freebsdimageinazure.png)
