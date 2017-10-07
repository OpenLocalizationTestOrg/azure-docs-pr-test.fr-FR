---
title: "le cluster HPC Pack tooan aaaAdd rafale nœuds | Documents Microsoft"
description: "Découvrez comment tooexpand un Pack de HPC cluster dans Azure à la demande en ajoutant des instances de rôle de travail en cours d’exécution dans un service cloud"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 24b79a8a-24ad-4002-ae76-75abc9b28c83
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 10/14/2016
ms.author: danlep
ms.openlocfilehash: 7ec40ffe76485742c9e458ec49e11805990974e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-on-demand-burst-nodes-tooan-hpc-pack-cluster-in-azure"></a>Ajouter le cluster des HPC Pack de support pour les tooan de nœuds à la demande « de « croissance dans Azure
Si vous configurez un [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster dans Azure, vous pouvez choisir une méthode tooquickly échelle hello la capacité de cluster vers le haut ou vers le bas, sans conserver un ensemble de machines virtuelles de nœud de calcul préconfiguré. Cet article explique comment tooadd à la demande « croître » nœuds (instances de rôle de travail en cours d’exécution dans un service cloud) en tant que nœud principal tooa ressources compute dans Azure. 

> [!IMPORTANT] 
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.

![Nœuds d’extension][burst]

étapes Hello dans cet article vous aident à ajouter rapidement des nœuds Azure tooa nuage nœud principal HPC Pack machine virtuelle pour un déploiement de test ou de preuve de concept. Hello, procédez hello capacité tooan local HPC Pack cluster de calcul tooadd cloud identique, comme les étapes hello trop « croître tooAzure ». Pour obtenir un didacticiel, consultez [Configuration d’un cluster de calcul hybride avec Microsoft HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md). Pour obtenir des instructions détaillées et des recommandations pour les déploiements de production, consultez [croître tooAzure avec Microsoft HPC Pack](https://technet.microsoft.com/library/gg481749.aspx).

## <a name="prerequisites"></a>Composants requis
* **Nœud principal HPC Pack déployé dans une machine virtuelle Azure** : vous pouvez utiliser une machine virtuelle à nœud principal autonome ou une machine virtuelle faisant partie d’un cluster plus grand. toocreate un nœud principal autonome, consultez [déployer un nœud principal de HPC Pack dans une machine virtuelle Azure](../../virtual-machines-windows-hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Pour les options de déploiement cluster HPC Pack automatisées, consultez [toocreate les Options et de gérer un cluster Windows HPC dans Azure avec Microsoft HPC Pack](../../virtual-machines-windows-hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
  
  > [!TIP]
  > Si vous utilisez hello [script de déploiement IaaS de HPC Pack](hpcpack-cluster-powershell-script.md) toocreate hello cluster dans Azure, vous pouvez inclure des nœuds de croissance Azure dans votre déploiement automatisé. Consultez les exemples hello dans cet article.
  > 
  > 
* **Abonnement Azure** -tooadd Azure nœuds, vous pouvez choisir hello même abonnement utilisé toodeploy hello nœud principal, ou un autre abonnement (ou les abonnements).
* **Quota de cœurs** -vous devrez peut-être le quota de hello tooincrease de cœurs, en particulier si vous choisissez toodeploy plusieurs nœuds Azure avec des tailles multicœurs. tooincrease un quota, [ouvrir une demande de support client en ligne](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) sans frais.

## <a name="step-1-create-a-cloud-service-and-a-storage-account-for-hello-azure-nodes"></a>Étape 1 : Créer un service cloud et un compte de stockage pour hello nœuds Azure
Utilisez hello portail Azure classic ou hello de tooconfigure outils équivalent suivant des ressources qui sont nécessaire toodeploy vos nœuds Azure :

* Un nouveau service cloud Azure
* Un nouveau compte de stockage Azure

> [!NOTE]
> Ne réutilisez pas un service cloud existant dans votre abonnement. 
> 
> 

**Considérations**

* Configurer un service cloud distinct pour chaque modèle de nœud Azure que vous envisagez de toocreate. Toutefois, vous pouvez utiliser hello même compte de stockage pour plusieurs modèles de nœud.
* Nous recommandons de placer le service cloud hello et compte de stockage hello pour le déploiement de hello Bonjour même région Azure.

## <a name="step-2-configure-an-azure-management-certificate"></a>Étape 2 : configurer un certificat de gestion Azure
tooadd Azure nœuds en tant que ressources de calcul, vous avez besoin d’un certificat de gestion sur le nœud principal de hello et le téléchargement correspondante du certificat toohello abonnement Azure utilisé pour le déploiement de hello.

Pour ce scénario, vous pouvez choisir hello **par défaut de certificat de gestion Azure HPC** HPC Pack installe et configure automatiquement sur le nœud principal. Ce certificat est utile à des fins de test et pour les déploiements pour validation technique. toouse de ce certificat, téléchargez le fichier C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer à partir du nœud principal hello abonnement toothe de machine virtuelle. certificat de hello tooupload Bonjour [portail Azure classic](https://manage.windowsazure.com), cliquez sur **paramètres** > **certificats de gestion**.

Pour le certificat de gestion tooconfigure hello des options supplémentaires, consultez [hello tooConfigure de scénarios le certificat de gestion Azure pour les déploiements en rafale Azure](http://technet.microsoft.com/library/gg481759.aspx).

## <a name="step-3-deploy-azure-nodes-toohello-cluster"></a>Étape 3 : Déployer le cluster toohello de nœuds Azure
Hello étapes tooadd et démarrez Azure nœuds dans ce scénario sont généralement identiques hello en tant qu’étapes hello avec un nœud principal local. Pour plus d’informations, consultez hello suivant des sections de [étapes tooDeploy des nœuds Azure avec Microsoft HPC Pack](https://technet.microsoft.com/library/gg481758.aspx):

* Créer un modèle de nœud Azure
* Ajouter un cluster de nœuds Azure toohello Windows HPC
* Démarrer (approvisionner) hello des nœuds Azure

Après avoir ajouté et démarrer les nœuds hello, elles sont prêtes pour vous toouse toorun les travaux du cluster.

Si vous rencontrez des problèmes pendant le déploiement des nœuds Azure, consultez [Dépannage de problèmes liés aux déploiements de nœuds Azure avec Microsoft HPC Pack](http://technet.microsoft.com/library/jj159097.aspx).

## <a name="next-steps"></a>Étapes suivantes
* nœuds de croissance toouse une taille d’instance de calcul intensif pour hello, voir Considérations hello dans [tailles de machine virtuelle de calcul haute performance](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Si vous souhaitez augmenter ou réduire automatiquement hello Azure les ressources en fonction de la charge de travail de cluster hello informatiques, consultez [croître automatiquement et de réduire les ressources de calcul Azure dans un cluster HPC Pack](hpcpack-cluster-node-autogrowshrink.md).

<!--Image references-->
[burst]: ./media/hpcpack-cluster-node-burst/burst.png
