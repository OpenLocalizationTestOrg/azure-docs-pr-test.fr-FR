---
title: "pools d’aaaProvision Azure Batch à partir d’images personnalisées | Documents Microsoft"
description: "Vous pouvez créer un lot de calcul pool à partir d’une image personnalisée de tooprovision les nœuds qui contiennent des logiciels de hello et les données dont vous avez besoin pour votre application. Images personnalisées sont un moyen efficace tooconfigure toorun de nœuds de calcul vos charges de travail de traitement par lots."
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: article
ms.date: 08/07/2017
ms.author: tamram
ms.openlocfilehash: 5cb698ee90f7d3ec9ffe69fa4dc602132c3f7569
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-a-custom-image-toocreate-a-pool-of-virtual-machines"></a>Utiliser une image personnalisée de toocreate un pool de machines virtuelles

Lorsque vous créez un pool de machines virtuelles dans Azure Batch, vous spécifiez une image de machine virtuelle (VM) qui fournit un système d’exploitation de hello pour chaque nœud de calcul dans le pool de hello. Vous pouvez créer un pool de machines virtuelles à partir d’une image de la Place de marché ou en fournissant une image de disque dur virtuel (VHD) personnalisée que vous avez préparée. Lorsque vous fournissez une image personnalisée, vous pouvez contrôler la configuration de système d’exploitation de hello au moment de hello chaque nœud de calcul est configurée. Votre image personnalisée peut également inclure des applications et le nœud de calcul des données de référence qui sont disponibles sur hello dès qu’elle est configurée.

À l’aide d’une image personnalisée peut gagner du temps lors de l’obtention des nœuds de calcul de votre pool prêt toorun votre charge de travail de traitement par lots. Même si vous pouvez utiliser une image de la Place de marché et installer les logiciels sur chaque nœud de calcul une fois le nœud approvisionné, cette approche peut être moins efficace qu’utiliser une image personnalisée. 

Certaines des raisons toouse une image personnalisée qui est configurée pour votre scénario incluent devoir :

- **Configurer le système d’exploitation de hello (système d’exploitation)** configuration spéciale du système d’exploitation de hello peut être effectuée sur une image personnalisée de hello. 
- **Installer des applications volumineuses** : il est plus judicieux d’installer des applications sur une image personnalisée que de les installer sur chaque nœud de calcul après leur approvisionnement.
- **Copier des quantités importantes de données** : Si les données de salutation sont image personnalisée de toohello copié, il doit uniquement toobe copié qu’une seule fois, au lieu de nœud de calcul tooeach, gagner du temps et bande passante.
- **Redémarrez hello machine virtuelle pendant le processus d’installation de hello.** Hello redémarrage machine virtuelle peut prendre du temps, surtout si vous avez un nombre de nœuds de calcul.

## <a name="prerequisites"></a>Composants requis

- **Un compte de traitement par lots créé avec le mode d’allocation de pool hello abonnement utilisateur.** toouse un pools de Machine virtuelle tooprovision image personnalisée, créer votre compte Batch avec hello abonnement utilisateur [mode d’allocation de pool](batch-api-basics.md#pool-allocation-mode). Avec ce mode, les pools de lot sont allouées en abonnement hello dans laquelle réside hello compte. Consultez hello [compte](batch-api-basics.md#account) section [parallèles à grande échelle de développer des solutions avec le traitement par lots de calcul](batch-api-basics.md) pour plus d’informations sur la configuration de mode d’allocation de pool hello lorsque vous créez un compte Batch.

- **Un compte de stockage Azure.** toocreate un pool d’ordinateurs virtuels à l’aide d’une image personnalisée, vous avez besoin d’un compte de stockage Azure standard, à usage général Bonjour même abonnement et région. Si vous créez une image personnalisée à partir d’une machine virtuelle Azure, vous allez copier compte de stockage hello image toohello où se trouve le disque du système d’exploitation de la machine virtuelle hello, et vous n’aurez pas toocreate un compte de stockage distinct. 
    
## <a name="prepare-a-custom-image"></a>Préparer une image personnalisée

tooprepare une image personnalisée pour une utilisation avec le traitement par lots, vous devez généraliser une installation existante de Windows ou Linux. La généralisation d’une installation de système d’exploitation supprime les informations spécifiques à la machine. résultat de Hello est une image qui peut être installée sur d’autres ordinateurs ou les machines virtuelles.  

> [!IMPORTANT]
> Traitement par lots ne prend pas en charge l’utilisation d’Azure géré images tooprovision un pool. image personnalisée de Hello, vous utilisez tooprovision qu'un pool doit être stocké dans le stockage Azure. 
>
> Lorsque vous préparez votre image personnalisée, gardez Bonjour l’esprit les points suivants :
> - Vérifiez cette image de système d’exploitation à base de hello, vous utilisez tooprovision vos pools de lot est n’a pas un préalable installé des extensions Azure, comme extension de Script personnalisé hello. Si l’image de hello contient une extension préinstallée, Azure peut rencontrer des problèmes de la déployer hello machine virtuelle.
> - Assurez-vous que cette image du système d’exploitation de base de hello que vous fournir utilise hello lecteur temp de la valeur par défaut, comme hello agent de nœud de lot actuellement attend lecteur temp de hello par défaut.
>
>

Vous pouvez utiliser une image Windows ou Linux préparée comme image personnalisée. Par exemple, si vous souhaitez toouse une image locale, puis téléchargez le compte de stockage Azure hello image tooan qui se trouve dans hello même abonnement et région que votre compte de traitement par lots à l’aide de [AzCopy](../storage/storage-use-azcopy.md) ou un autre outil de téléchargement.

Vous pouvez aussi préparer une image personnalisée à partir d’une machine virtuelle Azure nouvelle ou existante. Si vous créez une machine virtuelle, vous pouvez utiliser une image Azure Marketplace en tant qu’image de base hello pour votre image personnalisée et puis de le personnaliser. image de base toocustomize hello, créez une machine virtuelle Azure et ajoutez vos applications ou les données tooit. Généraliser tooserve de machine virtuelle hello en tant que votre image personnalisée, puis enregistrez-le tooAzure stockage. 

tooprepare une image personnalisée à partir d’une machine virtuelle Azure, procédez comme suit :

1. Créez une machine virtuelle Azure **non gérée** à partir d’une image de la Place de marché Azure. La Place de marché Azure propose des images pour [Windows](../virtual-machines/windows/quick-create-portal.md) et [Linux](../virtual-machines/linux/quick-create-portal.md).
    
    À l’étape 3 de hello les processus de création de machine virtuelle, assurez-vous que vous sélectionnez **non** pour **stockage : utiliser des disques gérés** option. Notez également du nom de compte de stockage hello pour le disque du système d’exploitation de la machine virtuelle de hello, que ce compte de stockage est également où Azure enregistre votre image personnalisée :

    ![Créer une machine virtuelle non managé et le nom de compte de stockage hello Remarque](media/batch-custom-images/vm-create-storage.png)
 
2. Effectuer hello du processus de création de votre machine virtuelle, puis attendez qu’elle toobe allouée par Azure. Voici une image qui montre une machine virtuelle Bonjour Azure portal Bonjour état d’exécution :

    ![Créer une machine virtuelle à partir d’une image de la Place de marché](media/batch-custom-images/vm-status-running.png)

3. Une fois hello machine virtuelle est en cours d’exécution, vous connecter tooit via le protocole RDP (pour Windows) ou de SSH (pour Linux). Installer des logiciels nécessaires ou copier les données souhaitées et puis généraliser hello machine virtuelle. Suivez les étapes de hello décrites dans [Generalize hello VM](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sa-copy-generalized.md#generalize-the-vm). 
   
4. Suivez les étapes de hello trop[connecter tooAzure PowerShell](../virtual-machines/windows/sa-copy-generalized.md#log-in-to-azure-powershell). tooinstall Azure PowerShell, consultez [vue d’ensemble de Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.2.0). 

5. Ensuite, suivez les étapes de hello trop[Deallocate hello VM et ensemble hello état toogeneralized](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sa-copy-generalized#deallocate-the-vm-and-set-the-state-to-generalized). 

    Bonjour portail Azure, notez que hello que machine virtuelle est libérée :

    ![Vérifiez que hello que machine virtuelle est désallouée.](media/batch-custom-images/vm-status-deallocated.png)

6.  Créez et enregistrez hello VM image tooAzure stockage à l’aide de hello [Save-AzureRmVMImage](https://docs.microsoft.com/powershell/module/azurerm.compute/save-azurermvmimage) applet de commande PowerShell. Suivez les instructions de hello décrites dans [créer une image hello](../virtual-machines/windows/sa-copy-generalized.md#create-the-image).
    
    image de machine virtuelle Hello est enregistré le compte de stockage Azure toohello créé en hello machine virtuelle, comme indiqué à l’étape 1 de cette procédure. applet de commande Hello Save-AzureRmVMImage enregistre hello image toohello **système** conteneur dans ce compte de stockage. Hello `-DestinationContainername` paramètre désigne un répertoire virtuel d’hello **système** conteneur. Hello `-VHDNamePrefix` paramètre spécifie un préfixe de nom d’objet blob hello. Ce préfixe est le nom d’objet blob toohello ajoutant au début d’un trait d’union. 

    Par exemple, supposons que vous appelez Save-AzureRmVMImage avec hello paramètres suivants :  

        Save-AzureRmVMImage -ResourceGroupName sample-resource-group -Name vm-custom-image -DestinationContainerName batchimages -VHDNamePrefix custom -Path C:\Temp\Images\vm-custom-image.json

    l’image obtenue Hello est enregistré toohello emplacement et nom d’objet blob indiqué ici :

    ![Emplacement du VHD enregistré dans le conteneur système](media/batch-custom-images/vhd-in-vm-storage-account.png)

    > [!NOTE]
    > Une machine virtuelle non gérée Azure crée plusieurs comptes de stockage à des différentes fins. Si vous n’avez pas noté nom hello hello du conteneur de stockage pour le disque du système d’exploitation de hello lorsque hello machine virtuelle a été créé, puis rechercher que du compte de stockage de hello associé contient hello **système** conteneur. Naviguer dans hello **système** conteneur toofind hello personnalisée à l’aide de valeurs hello spécifiées pour hello **Save-AzureRmVMImage** commande.

## <a name="create-a-pool-from-a-custom-image-in-hello-portal"></a>Créer un pool à partir d’une image personnalisée dans le portail de hello

Une fois que vous avez enregistré votre image personnalisée et que vous connaissez son emplacement, vous pouvez créer un pool Batch à partir de cette image. Suivez ces étapes de toocreate un pool de hello portail Azure :

1. Accédez à tooyour du compte Batch Bonjour portail Azure. Ce compte doit être Bonjour même abonnement et région en tant que stockage de hello compte contenant personnalisée hello. 
2. Bonjour **paramètres** fenêtre sur hello de gauche, sélectionnez hello **Pools** élément de menu.
3. Bonjour **Pools** fenêtre, sélectionnez hello **ajouter** commande.
4. Sur hello **ajouter un Pool** fenêtre, sélectionnez **l’Image personnalisée (Linux/Windows)** de hello **le Type d’Image** liste déroulante. portail de Hello affiche hello **Image personnalisée** sélecteur. Accédez toohello compte de stockage où se trouve votre image personnalisée, et sélectionnez hello VHD souhaitée à partir du conteneur de hello. 
5. Sélectionnez hello correct **Publisher offre/référence (SKU)** pour votre disque dur virtuel personnalisé.
6. Spécifiez hello restant requis de paramètres, y compris hello **taille du nœud**, **dédiés nœuds cibles**, et **faible des nœuds de priorité**, ainsi que les paramètres facultatifs vous le souhaitez.

    Par exemple, pour une image personnalisée de Microsoft Windows Server Datacenter 2016, hello **ajouter un Pool** fenêtre s’affiche comme illustré ici :

    ![Ajouter un pool à partir d’une image Windows personnalisée](media/batch-custom-images/add-pool-custom-image.png)
  
toocheck si un pool existant est basé sur une image personnalisée, consultez hello **système d’exploitation** propriété dans la section Résumé de ressource hello Hello **Pool** fenêtre. Si le pool de hello a été créé à partir d’une image personnalisée, il est défini trop**Image de machine virtuelle personnalisée**.

Tous les disques durs virtuels personnalisés associés à un pool sont affichés sur du pool hello **propriétés** fenêtre.
 
## <a name="next-steps"></a>Étapes suivantes

- Pour obtenir une présentation détaillée de Batch, consultez [Développer des solutions de calcul parallèles à grande échelle avec Batch](batch-api-basics.md).
- Pour plus d’informations sur la création d’un compte de traitement par lots, consultez [créer un compte de traitement par lots avec hello Azure portal](batch-account-create-portal.md).
