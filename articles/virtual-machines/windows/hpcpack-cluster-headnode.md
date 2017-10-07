---
title: "aaaCreate un nœud principal HPC Pack dans une machine virtuelle Azure | Documents Microsoft"
description: "Découvrez comment toouse hello déploiement de gestionnaire de ressources Azure portal et hello modèle toocreate un nœud principal de Microsoft HPC Pack 2012 R2 dans une machine virtuelle Azure."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,hpc-pack
ms.assetid: e6a13eaf-9124-47b4-8d75-2bc4672b8f21
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 3ddefb74b053a48a15f1ba1ca8edbc0192da51a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hello-head-node-of-an-hpc-pack-cluster-in-an-azure-vm-with-a-marketplace-image"></a>Créer un nœud principal de hello d’un cluster HPC Pack dans une machine virtuelle de Azure avec une image de Marketplace
Utilisez un [image de machine virtuelle Microsoft HPC Pack 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) hello Azure Marketplace et hello toocreate portail Azure hello nœud principal d’un cluster HPC. Cette image de machine virtuelle HPC Pack est basée sur Windows Server 2012 R2 Datacenter avec HPC Pack 2012 R2 Update 3 préinstallé. Utilisez ce nœud principal pour un déploiement preuve de concept de HPC Pack dans Azure. Vous pouvez ensuite ajouter calcul nœuds toohello cluster toorun HPC les charges de travail.

> [!TIP]
> toodeploy un cluster HPC Pack 2012 R2 complète dans Azure qui inclut le nœud principal de hello et les nœuds de calcul, nous vous recommandons d’utiliser une méthode automatisée. Les options sont hello [script de déploiement IaaS de HPC Pack](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) et les modèles de gestionnaire de ressources tels que hello [cluster HPC Pack pour les charges de travail Windows](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/). Des modèles Resource Manager sont également disponibles pour les [clusters Microsoft HPC Pack 2016](https://github.com/MsHpcPack/HPCPack2016/tree/master/newcluster-templates). 
> 
> 

## <a name="planning-considerations"></a>Considérations en matière de planification
Comme indiqué dans la figure suivante de hello, vous déployez le nœud principal de HPC Pack hello dans un domaine Active Directory dans un réseau virtuel Azure.

![Nœud principal HPC Pack][headnode]

* **Domaine Active Directory**: hello HPC Pack 2012 R2 nœud principal doit être joints à un domaine Active Directory de tooan dans Azure avant de démarrer les services HPC hello sur hello machine virtuelle. Comme indiqué dans cet article, pour un déploiement de preuve de concept, vous pouvez promouvoir hello machine virtuelle que vous créez pour le nœud principal de hello comme contrôleur de domaine avant de démarrer les services HPC hello. Une autre option consiste à toodeploy un contrôleur de domaine distincts et de forêt dans Azure toowhich vous joignez hello machine virtuelle du nœud principal.

* **Modèle de déploiement**: la plupart des déploiements de nouveau, Microsoft recommande d’utiliser le modèle de déploiement du Gestionnaire de ressources hello. Cet article suppose que vous utilisez ce modèle de déploiement.

* **Réseau virtuel Azure**: lorsque vous utilisez hello Gestionnaire de ressources du déploiement modèle toodeploy hello nœud principal, vous spécifiez ou créez un réseau virtuel Azure. Vous utilisez les réseaux virtuels hello si vous avez besoin de tooan-domaine d’Active Directory existant toojoin hello du nœud principal. Vous besoin également ultérieure tooadd de nœud de calcul cluster toohello de machines virtuelles.

## <a name="steps-toocreate-hello-head-node"></a>Nœud de tête hello toocreate étapes
Voici les principales étapes à suivre toouse hello toocreate portail Azure une machine virtuelle de Azure pour le nœud principal HPC Pack de hello à l’aide du modèle de déploiement du Gestionnaire de ressources hello. 

1. Si vous souhaitez toocreate une nouvelle forêt Active Directory dans Azure avec des machines virtuelles de contrôleur de domaine séparé, une option consiste à toouse un [modèle Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/active-directory-new-domain-ha-2-dc). Pour une simple déploiement de preuve de concept, il a fine tooomit cette étape et configurer la machine virtuelle elle-même d’un nœud principal hello comme contrôleur de domaine. Cette option est décrites plus loin dans cet article.
2. Sur hello [HPC Pack 2012 R2 sur Windows Server 2012 R2 page](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) Bonjour Azure Marketplace, cliquez sur **créer un ordinateur virtuel**. 
3. Dans le portail hello, sur hello **HPC Pack 2012 R2 sur Windows Server 2012 R2** page, sélectionnez hello **le Gestionnaire de ressources** modèle de déploiement, puis cliquez sur **créer**.
   
    ![Image HPC Pack][marketplace]
4. Utiliser les paramètres de hello tooconfigure portail hello et créer hello machine virtuelle. Si vous êtes de nouveau tooAzure, suivez le didacticiel de hello [créer une machine virtuelle Windows Bonjour Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Pour un déploiement de preuve de concept, vous pouvez généralement acceptez hello par défaut ou les paramètres recommandés.
   
   > [!NOTE]
   > Si vous souhaitez toojoin hello du nœud principal tooan existant de domaine Active Directory dans Azure, assurez-vous que vous spécifiez le réseau virtuel de hello pour ce domaine lors de la création de hello machine virtuelle.
   > 
   > 
5. Une fois que vous créez hello machine virtuelle et hello machine virtuelle est en cours d’exécution, [connecter toohello VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Bureau à distance. 
6. Joignez la forêt de domaines Active Directory hello VM tooan en choisissant une des options suivantes de hello :
   
   * Si vous avez créé hello machine virtuelle dans un réseau virtuel Azure avec une forêt de domaines existante, joindre la forêt de toohello hello machine virtuelle à l’aide d’outils standard du Gestionnaire de serveur ou Windows PowerShell. Ensuite, redémarrez.
   * Si vous avez créé hello machine virtuelle dans un réseau virtuel (sans une forêt de domaines), puis promouvoir hello machine virtuelle comme contrôleur de domaine. Utilisez les étapes standard tooinstall et configurer le rôle des Services de domaine Active Directory hello sur le nœud principal de hello. Pour obtenir la procédure détaillée, consultez [Installer une nouvelle forêt Active Directory Windows Server 2012](https://technet.microsoft.com/library/jj574166.aspx).
7. Après avoir hello machine virtuelle est en cours d’exécution et est joint à un tooan forêt Active Directory, démarrez les services HPC Pack hello comme suit :
   
    a. Se connecter toohello nœud principal à l’aide d’un compte de domaine qui est membre du groupe Administrateurs local de hello. Par exemple, utiliser le compte d’administrateur hello configuré lorsque vous avez créé la machine virtuelle du nœud principal hello.
   
    b. Pour une configuration de nœud principal par défaut, démarrez Windows PowerShell en tant qu’administrateur et tapez Bonjour suivant :
   
    ```PowerShell
    & $env:CCP_HOME\bin\HPCHNPrepare.ps1 –DBServerInstance ".\ComputeCluster"
    ```
   
    Il peut prendre plusieurs minutes pour hello HPC Pack services toostart.
   
    Pour d’autres options de configuration du nœud principal, tapez `get-help HPCHNPrepare.ps1`.

## <a name="next-steps"></a>Étapes suivantes
* Vous pouvez désormais travailler avec le nœud principal de hello de votre cluster HPC Pack. Par exemple, démarrez HPC Cluster Manager et hello complète [liste des tâches de déploiement](https://technet.microsoft.com/library/jj884141.aspx).
* Si vous souhaitez tooincrease hello cluster calcul capacité à la demande, ajoutez [nœuds de croissance Azure](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) dans un service cloud. 
* Essayez d’exécuter un test de charge sur le cluster de hello. Pour obtenir un exemple, consultez hello HPC Pack [mise en route](https://technet.microsoft.com/library/jj884144).

<!--Image references-->
[headnode]: ./media/hpcpack-cluster-headnode/headnode.png
[marketplace]: ./media/hpcpack-cluster-headnode/marketplace.png
