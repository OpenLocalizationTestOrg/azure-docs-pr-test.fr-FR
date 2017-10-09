---
title: sur les ordinateurs virtuels de clusters aaaMATLAB | Documents Microsoft
description: "Utiliser Microsoft Azure virtual machines toocreate MATLAB Distributed Computing Server clusters toorun vos charges de travail de calcul intensif parallèles MATLAB"
services: virtual-machines-windows
documentationcenter: 
author: mscurrell
manager: timlt
editor: 
ms.assetid: e9980ce9-124a-41f1-b9ec-f444c8ea5c72
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Windows
ms.workload: infrastructure-services
ms.date: 05/09/2016
ms.author: markscu
ms.openlocfilehash: 266749dbdcfefac42c94b74aa612bfee18075a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-matlab-distributed-computing-server-clusters-on-azure-vms"></a>Créer des clusters MATLAB Distributed Computing Server sur des machines virtuelles Azure
Utilisez Microsoft Azure virtual machines toocreate un ou plusieurs serveur MATLAB Distributed Computing Server clusters toorun vos charges de travail de calcul intensif parallèles MATLAB. Installer le logiciel de serveur MATLAB Distributed Computing Server sur un toouse de machine virtuelle comme une image de base et utiliser un modèle de démarrage rapide Azure ou d’un script Azure PowerShell (disponible sur [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster)) toodeploy et gérer hello cluster. Après le déploiement, connectez-vous toohello cluster toorun vos charges de travail.

## <a name="about-matlab-and-matlab-distributed-computing-server"></a>Présentation de MATLAB et de MATLAB Distributed Computing Server
Hello [MATLAB](http://www.mathworks.com/products/matlab/) plate-forme est optimisé pour la résolution des problèmes techniques et scientifiques. Les utilisateurs MATLAB simulations à grande échelle et les tâches de traitement des données peuvent utiliser parallèle MathWorks informatique toospeed produits des leurs charges de travail intensives en tirant parti des services de la grille et de clusters de calcul. [Parallel Computing Toolbox](http://www.mathworks.com/products/parallel-computing/) permet aux utilisateurs MATLAB de mettre des applications en parallèle et de tirer parti de processeurs multicœur, de GPU et de clusters de calcul. [Serveur MATLAB Distributed Computing Server](http://www.mathworks.com/products/distriben/) MATLAB utilisateurs tooutilize permet à plusieurs ordinateurs d’un cluster de calcul.

À l’aide de machines virtuelles, vous pouvez créer des clusters de serveur MATLAB Distributed Computing Server dont toutes les hello même mécanismes disponibles toosubmit un travail parallèle en tant que clusters sur site, tels que les travaux interactive, les traitements par lots, les tâches indépendantes, et communication des tâches. À l’aide d’Azure conjointement avec la plate-forme MATLAB hello a de nombreux avantages par rapport tooprovisioning et à l’aide de traditionnel sur site matériel : tailles d’une plage de la machine virtuelle, la création de clusters à la demande et de payer uniquement pour les ressources de calcul hello vous utilisez, et modèles de tootest Hello possibilité à grande échelle.  

## <a name="prerequisites"></a>Composants requis
* **Ordinateur client** -vous aurez besoin d’un toocommunicate d’ordinateur client basé sur Windows Azure et hello cluster de serveur MATLAB Distributed Computing Server après le déploiement.
* **Azure PowerShell** -consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) tooinstall sur votre ordinateur client.
* **Abonnement Azure** : si vous n’en avez pas, vous pouvez créer un [compte gratuit](https://azure.microsoft.com/free/) en quelques minutes. Pour les clusters de grande taille, envisagez de souscrire un abonnement de paiement à l’utilisation ou d’autres options d’achat.
* **Quota de cœurs** -vous devrez peut-être tooincrease hello core quota toodeploy un grand cluster ou plusieurs clusters de serveur MATLAB Distributed Computing Server. tooincrease un quota, [ouvrir une demande de support client en ligne](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) sans frais.
* **Licences MATLAB, boîte à outils de calcul parallèle et MATLAB Distributed Computing Server** -scripts de hello supposent que hello [Gestionnaire de licences hébergé MathWorks](http://www.mathworks.com/products/parallel-computing/mathworks-hosted-license-manager/) est utilisé pour toutes les licences.  
* **Logiciel de serveur MATLAB Distributed Computing Server** -sera installé sur un ordinateur virtuel qui doit servir en tant qu’image de machine virtuelle base hello pour les machines virtuelles du cluster hello.

## <a name="high-level-steps"></a>Étapes de haut niveau
toouse des machines virtuelles Azure pour votre serveur MATLAB Distributed Computing Server clusters, hello étapes générales suivantes sont requises. Les instructions détaillées sont dans la documentation hello qui accompagnent le modèle de démarrage rapide de hello et des scripts sur [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster).

1. **Créer une image de machine virtuelle de base**  

   * Téléchargez et installez le logiciel MATLAB Distributed Computing Server sur cette machine virtuelle.

     > [!NOTE]
     > Ce processus peut prendre quelques heures, mais il vous suffit de toodo une fois pour chaque version de MATLAB que vous utilisez.   
     >
     >
2. **Créer un ou plusieurs clusters**  

   * Utilisez hello fourni de script PowerShell ou hello quickstart modèle toocreate un cluster à partir de l’image de machine virtuelle base hello.   
   * Gérer les clusters hello à l’aide de script PowerShell hello fourni qui vous permet de toolist, suspendre, reprendre et supprimer les clusters.

## <a name="cluster-configurations"></a>Configurations de cluster
Actuellement, modèle et le script de création de cluster hello permettent toocreate une topologie de serveur MATLAB Distributed Computing Server unique. Si vous le souhaitez, créez un ou plusieurs clusters supplémentaires, comportant chacun un nombre distinct de machines virtuelles de travail, utilisant différentes tailles de machine virtuelle, et ainsi de suite.

### <a name="matlab-client-and-cluster-in-azure"></a>Client MATLAB et cluster dans Azure
nœuds de client Hello MATLAB, Planificateur de travaux MATLAB et MATLAB Distributed Computing Server « travail » nœuds configurés en tant que machines virtuelles Azure dans un réseau virtuel, comme indiqué dans les éléments suivants de hello figure.


* toouse hello de cluster, vous connecter à un nœud du client Bureau à distance toohello. nœud Hello du client exécute le client MATLAB hello.
* nœud Hello du client a un partage de fichiers qui peut être accessible par tous les traitements.
* MathWorks hébergé le Gestionnaire de licences est utilisé pour les contrôles de licence hello pour tous les logiciels MATLAB.
* Par défaut, un travail de serveur MATLAB Distributed Computing Server par cœur est créé sur le travail hello machines virtuelles, mais vous pouvez spécifier n’importe quel nombre.

## <a name="use-an-azure-based-cluster"></a>Utiliser un cluster Azure
Comme avec d’autres types de serveur MATLAB Distributed Computing Server clusters, vous devez toouse hello Gestionnaire du Cluster de profil dans hello MATLAB client (sur le client hello VM) toocreate un profil de cluster du Planificateur de travaux MATLAB.

![Cluster Profile Manager](./media/matlab-mdcs-cluster/cluster_profile_manager.png)

## <a name="next-steps"></a>Étapes suivantes
* Pour obtenir des instructions détaillées toodeploy et gérer des clusters de serveur MATLAB Distributed Computing Server dans Azure, consultez hello [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster) référentiel contenant des modèles de hello et de scripts.
* Accédez toohello [MathWorks site](http://www.mathworks.com/) pour obtenir une documentation détaillée pour MATLAB et MATLAB Distributed Computing Server.
