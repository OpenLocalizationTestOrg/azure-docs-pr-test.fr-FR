---
title: "Vue d’ensemble d’Azure Batch pour développeurs | Microsoft Docs"
description: "Découvrez les fonctionnalités du service Batch et de ses API du point de vue du développeur."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 416b95f8-2d7b-4111-8012-679b0f60d204
ms.service: batch
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c2f2a878414e4efd626d674ef9a182ae52eeb1ff
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="develop-large-scale-parallel-compute-solutions-with-batch"></a>Développer des solutions de calcul parallèles à grande échelle avec Batch

Dans cette vue d’ensemble des principaux composants du service Azure Batch, nous aborderons les fonctionnalités et ressources du service Batch qui permettent aux développeurs de créer des solutions de calcul parallèles à grande échelle.

Que vous développiez une application ou un service de calcul distribué émettant des appels [d’API REST][batch_rest_api] directs, ou que vous utilisiez l’un des [Kits de développement logiciel (SDK) Batch](batch-apis-tools.md#azure-accounts-for-batch-development), vous utiliserez la plupart des ressources et des fonctionnalités présentées dans cet article.

> [!TIP]
> Pour une présentation plus poussée du service Batch, consultez l’article [Notions de base d’Azure Batch](batch-technical-overview.md).
>
>

## <a name="batch-service-workflow"></a>Flux de travail du service Batch
Le flux de travail de haut niveau suivant est caractéristique de la plupart des applications et services utilisant le service Batch pour le traitement des charges de travail parallèles :

1. Chargez les **fichiers de données** que vous souhaitez traiter vers un compte [Stockage Azure][azure_storage]. Le service Batch inclut la prise en charge intégrée de l’accès au stockage d’objets Blob Azure ; lorsque les tâches sont exécutées, celles-ci peuvent télécharger les fichiers en question vers les [nœuds de calcul](#compute-node) .
2. Chargez le **fichiers d’application** que les tâches exécuteront. Ces fichiers peuvent être des fichiers binaires ou des scripts, accompagnés de leurs dépendances, et sont exécutés par les tâches dans vos travaux. Vos tâches peuvent télécharger ces fichiers à partir de votre compte Azure Storage ; vous pouvez également utiliser la fonctionnalité [packages d’application](#application-packages) de Batch pour le déploiement et la gestion des applications.
3. Créez un [pool](#pool) de nœuds de calcul. Lors de la création d’un pool, vous devez spécifier le nombre de nœuds de calcul du pool, leur taille ainsi que le système d’exploitation. Pour chaque exécution de tâche dans votre travail, cette dernière est exécutée sur l’un des nœuds du pool.
4. Créez un [travail](#job). Un travail gère une collection de tâches. Vous associez chaque travail à un pool spécifique, dans lequel s’exécuteront les tâches du travail concerné.
5. Ajoutez des [tâches](#task) au travail. Chaque tâche exécute l’application ou le script téléchargés afin de traiter les fichiers de données téléchargés à partir de votre compte de stockage. Lorsque chaque tâche est terminée, celle-ci peut télécharger sa sortie vers Azure Storage.
6. Surveillez la progression du travail et récupérez la sortie de la tâche à partir d’Azure Storage.

Les sections suivantes portent sur ces points ainsi que sur les autres ressources de Batch qui permettent l’exécution de votre scénario de calcul distribué.

> [!NOTE]
> Un [compte Batch](#account) est nécessaire pour utiliser le service Batch. La plupart des solutions Batch utilisent aussi un compte [Stockage Azure][azure_storage], afin de stocker et récupérer un fichier. Actuellement, le service Batch prend uniquement en charge le type de compte de stockage à **usage général**, comme décrit à l’étape 5 de la section [Créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account) de l’article [À propos des comptes de stockage Azure](../storage/common/storage-create-storage-account.md).
>
>

## <a name="batch-service-resources"></a>Ressources du service Batch
Certaines des ressources suivantes (comptes, nœuds de calcul, pools, travaux et tâches) sont requises par toutes les solutions qui utilisent le service Batch. D’autres, telles que les planifications de travaux et les packages d’applications, sont utiles, mais facultatives.

* [Compte](#account)
* [Nœud de calcul](#compute-node)
* [Pool](#pool)
* [Travail](#job)

  * [Planifications de travaux](#scheduled-jobs)
* [Tâche](#task)

  * [Tâche de démarrage](#start-task)
  * [Tâche du gestionnaire de travaux](#job-manager-task)
  * [Tâches de préparation et lancement](#job-preparation-and-release-tasks)
  * [Tâche multi-instance (MPI)](#multi-instance-tasks)
  * [Dépendances de la tâche](#task-dependencies)
* [Packages d’applications](#application-packages)

## <a name="account"></a>Compte
Un compte Batch est une entité identifiée de façon unique au sein du service Batch. Tout le traitement s’effectue via un compte Batch.

Vous pouvez créer un compte Azure Batch à l’aide du [Portail Azure](batch-account-create-portal.md) ou par programme, par exemple avec la [bibliothèque .NET de gestion Batch](batch-management-dotnet.md). Au moment de la création du compte, vous pouvez associer un compte de Stockage Azure.

### <a name="pool-allocation-mode"></a>Mode d’allocation de pool

Lorsque vous créez un compte Batch, vous pouvez spécifier la manière dont les [pools](#pool) de nœuds de calcul sont alloués. Vous pouvez choisir d’allouer les pools de nœuds de calcul dans un abonnement géré par Azure Batch. Vous pouvez aussi les allouer dans votre propre abonnement. La propriété *mode d’allocation de pool* du compte détermine l’endroit où les pools sont alloués. 

Pour déterminer le mode d’allocation de pool à utiliser, il convient de réfléchir au mode qui est le plus adapté à votre scénario :

* **Service Batch** est le mode d’allocation de pool par défaut. Les pools sont alloués en arrière-plan dans des abonnements gérés par Azure. Gardez à l’esprit ces points clés concernant le mode d’allocation de pool Service Batch :

    - Le mode d’allocation de pool Service Batch prend en charge les pools de service cloud et de machines virtuelles.
    - Le mode d’allocation de pool Service Batch prend en charge l’authentification par clé partagée ou [l’authentification Azure Active Directory](batch-aad-auth.md) (Azure AD). 
    - Grâce au mode d’allocation de pool Service Batch, vous pouvez utiliser des nœuds de calcul dédiés ou à faible priorité dans des pools alloués.
    - N’utilisez pas ce mode d’allocation de pool si vous souhaitez créer des pools de machines virtuelles Azure à partir d’images de VM, ou si vous prévoyez d’utiliser un réseau virtuel. À la place, créez votre compte avec le mode d’allocation de pool Abonnement utilisateur.
    - Les pools de machines virtuelles configurés dans un compte créé grâce au mode d’allocation de pool Service Batch doivent être créés à partir d’images de la [Place de marché de machines virtuelles Microsoft Azure][vm_marketplace].

* Avec le mode d’allocation de pool **Abonnement utilisateur**, les pools Batch sont alloués dans l’abonnement Azure où le compte est créé. Gardez à l’esprit ces points clés concernant le mode d’allocation de pool Abonnement utilisateur :
     
    - Ce mode d’allocation de pool prend uniquement en charge les pools de machines virtuelles. elle ne gère pas les pools de services cloud.
    - Pour créer des pools de machines virtuelles à partir d’images VM, ou pour utiliser un réseau virtuel avec des pools de machines virtuelles, vous devez utiliser le mode d’allocation de pool Abonnement utilisateur.  
    - Vous devez utiliser [l’authentification Azure Active Directory](batch-aad-auth.md) avec les pools qui sont alloués dans l’abonnement de l’utilisateur. 
    - Si le mode d’allocation de pool est défini sur Abonnement utilisateur, vous devez configurer un Azure Key Vault pour votre compte Batch. 
    - Vous pouvez uniquement utiliser des nœuds de calcul dans des pools dont le compte est créé avec le mode d’allocation de pool Abonnement utilisateur. Les nœuds à faible priorité ne sont pas pris en charge.
    - Les pools de machines virtuelles configurés dans un compte associé au mode d’allocation de pool Abonnement utilisateur peuvent être créés à partir d’images de la [Place de marché Microsoft Azure][vm_marketplace] ou d’images personnalisées fournies par vos soins.

Le tableau suivant compare les modes d’allocation de pool Service Batch et d’Abonnement utilisateur.

| **Mode d’allocation de pool**                 | **Service Batch**                                                                                       | **Abonnement utilisateur**                                                              |
|-------------------------------------------|---------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------|
| **Les pools sont alloués dans**               | Un abonnement Azure géré                                                                           | L’abonnement de l’utilisateur dans lequel le compte Batch est créé                        |
| **Configurations prises en charge**             | <ul><li>Configuration service cloud</li><li>Configuration de machines virtuelles (Linux et Windows)</li></ul> | <ul><li>Configuration de machines virtuelles (Linux et Windows)</li></ul>                |
| **Images de machine virtuelle prises en charge**                  | <ul><li>Images de la Place de marché Azure</li></ul>                                                              | <ul><li>Images de la Place de marché Azure</li><li>Images personnalisées</li></ul>                   |
| **Types de nœuds de calcul pris en charge**         | <ul><li>Nœuds dédiés</li><li>Nœuds de faible priorité</li></ul>                                            | <ul><li>Nœuds dédiés</li></ul>                                                  |
| **Authentification prise en charge**             | <ul><li>Clé partagée</li><li>Azure AD</li></ul>                                                           | <ul><li>Azure AD</li></ul>                                                         |
| **Azure Key Vault requis**             | Non                                                                                                      | Oui                                                                                |
| **Quota de cœurs**                           | Déterminé par le quota de cœurs Batch                                                                          | Déterminé par le quota de cœurs Batch                                              |
| **Support réseau virtuel Azure (Vnet)** | Pools créés avec une configuration du service cloud                                                      | Pools créés avec une configuration de machines virtuelles                               |
| **Modèle de déploiement de réseau virtuel pris en charge**      | Vnets créés avec un modèle de déploiement classique                                                             | Réseaux virtuels créés avec le modèle de déploiement classique ou Azure Resource Manager |

## <a name="azure-storage-account"></a>un compte Azure Storage.

La plupart des solutions Batch utilisent Stockage Azure pour stocker les fichiers de ressources et les fichiers de sortie.  

Actuellement, le service Batch prend uniquement en charge le type de compte de stockage à usage général, comme décrit à l’étape 5 de la section [Créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account) de l’article [À propos des comptes de stockage Azure](../storage/common/storage-create-storage-account.md). Vos tâches Batch (y compris les tâches standard, de démarrage, de préparation des travaux et de validation des travaux) doivent spécifier des fichiers de ressources se trouvant dans les comptes de stockage à usage général.


## <a name="compute-node"></a>Nœud de calcul
Un nœud de calcul est une machine virtuelle Azure ou une machine virtuelle de service cloud dédiée au traitement d’une partie de la charge de travail de votre application. La taille d’un nœud détermine le nombre de cœurs du processeur, la capacité de mémoire et la taille du système de fichiers local qui lui est allouée. Vous pouvez créer des pools de nœuds Windows ou Linux à l’aide des services Azure Cloud Services, des images provenant de la [Place de marché de machines virtuelles Azure][vm_marketplace] ou des images personnalisées par vos soins. Pour plus d’informations sur ces options, voir la section suivante [Pool](#pool) .

Les nœuds peuvent exécuter tout fichier exécutable ou script pris en charge par l’environnement de système d’exploitation du nœud. Cela inclut les scripts \*.exe, \*.cmd, \*.bat et PowerShell pour Windows, les fichiers binaires, ainsi que les scripts shell et Python pour Linux.

Tous les nœuds de calcul Batch incluent également les éléments suivants :

* Une [structure de dossiers](#files-and-directories) standard et des [variables d’environnement](#environment-settings-for-tasks) associées pouvant être référencées par les tâches.
* **pare-feu** configurés pour le contrôle de l’accès.
* [accès distant](#connecting-to-compute-nodes) aux nœuds Windows (protocole RDP [Remote Desktop Protocol]) et Linux (Secure Shell [SSH]).

## <a name="pool"></a>pool
Un pool est une collection de nœuds sur lesquels votre application s’exécute. Vous pouvez créer le pool manuellement. Il peut également être créé automatiquement par le service Batch lorsque vous spécifiez le travail à accomplir. Vous pouvez créer et gérer un pool qui répond aux besoins en ressources de votre application. Un pool ne peut être utilisé que par le compte Batch dans lequel il a été créé. Un compte Batch peut avoir plusieurs pools.

Les pools Azure Batch sont créés en parallèle à la plate-forme de calcul Azure principale. Ils permettent d’effectuer des allocations à grande échelle, l’installation d’applications, la distribution de données, des analyses de fonctionnement et des ajustements flexibles du nombre de nœuds de calcul au sein d’un pool ([mise à l’échelle](#scaling-compute-resources)).

Chaque nœud ajouté à un pool se voit attribuer un nom unique et l’adresse IP. Lorsqu’un nœud est supprimé d’un pool, toutes les modifications apportées au système d’exploitation ou aux fichiers sont perdues, et son nom et son adresse IP sont libérés pour une utilisation ultérieure. Lorsqu’un nœud quitte un pool, sa durée de vie est terminée.

Lorsque vous créez un pool, vous pouvez spécifier les attributs suivants. Certains paramètres varient en fonction du mode d’allocation de pool associé au [compte](#account) Batch :

- Système d’exploitation et version de nœud de calcul
- Type de nœud de calcul et nombre cible de nœuds
- Taille des nœuds de calcul
- Stratégie de mise à l’échelle
- Stratégie de planification des tâches
- État de communication des nœuds de calcul
- Tâches de démarrage des nœuds de calcul
- packages d’application
- Configuration réseau

Chacun de ces paramètres est décrit plus en détail dans les sections suivantes.

> [!IMPORTANT]
> Les comptes Batch créés avec le mode d’allocation de pool Service Batch possèdent un quota par défaut. Ce quota limite le nombre de cœurs dans un compte Batch. Le nombre de cœurs correspond au nombre de nœuds de calcul. Pour en savoir plus sur les quotas par défaut et obtenir des instructions sur [l’augmentation d’un quota](batch-quota-limit.md#increase-a-quota), consultez l’article [Quotas et limites pour le service Azure Batch](batch-quota-limit.md). Si votre pool n’a pas obtenu son nombre cible de nœuds, cela peut être dû au quota principal.
>
>Les comptes Batch créés avec le mode d’allocation de pool Abonnement utilisateur ne tiennent pas compte des quotas relatifs aux services Batch. Au lieu de cela, ils partagent le quota principal de l’abonnement spécifié. Pour en savoir plus, consultez le paragraphe [Limites de machines virtuelles](../azure-subscription-service-limits.md#virtual-machines-limits) de la section [Abonnement Azure et limites, quotas et contraintes de service](../azure-subscription-service-limits.md).
>
>

### <a name="compute-node-operating-system-and-version"></a>Système d’exploitation et version de nœud de calcul

Lorsque vous créez un pool Batch, vous pouvez spécifier la configuration de machines virtuelles Azure et le type de système d’exploitation que vous souhaitez exécuter sur chaque nœud de calcul dans le pool. Les deux types de configurations Batch disponibles sont les suivants :

- La **configuration de machines virtuelles** indique que le pool est composé de machines virtuelles Azure. Ces machines virtuelles peuvent être créées à partir d’images Linux ou Windows. 

    Lorsque vous créez un pool basé sur la configuration de machine virtuelle, vous devez spécifier la taille des nœuds, mais aussi la source et les images utilisées pour les créer, la **référence d’image de machine virtuelle** et la **référence SKU de l’agent du nœud** à installer sur les nœuds. Pour plus d’informations sur la spécification des propriétés de pool, voir [Configurer des nœuds de calcul Linux dans des pools Azure Batch](batch-linux-nodes.md).

- La **configuration de Cloud Services** indique que le pool est composé de nœuds Microsoft Azure Cloud Services. Ce dernier fournit *uniquement* des nœuds de calcul Windows.

    Les systèmes d’exploitation disponibles pour les pools de configuration des services coud sont répertoriés dans [Versions du SE invité et matrice de compatibilité du Kit de développement logiciel (SDK) Azure](../cloud-services/cloud-services-guestos-update-matrix.md). Lorsque vous créez un pool qui contient des nœuds Cloud Services, vous devez spécifier la taille du nœud et sa *famille de systèmes d’exploitation*. Les services cloud sont déployés plus rapidement sur Azure que les machines virtuelles exécutant Windows. Si vous souhaitez créer des nœuds de calcul Windows, vous pouvez constater que Cloud Services propose un délai de déploiement moins important.

    * La *famille de système d’exploitation* détermine également les versions de .NET qui sont installées avec le système d’exploitation.
    * Comme avec les rôles de travail dans Services cloud, vous pouvez spécifier une *Version du système d’exploitation* (pour plus d’informations sur les rôles de travail, consultez la section [En savoir plus sur Services cloud](../cloud-services/cloud-services-choose-me.md#tell-me-about-cloud-services) de l’article [Vue d’ensemble de Services cloud](../cloud-services/cloud-services-choose-me.md)).
    * Comme avec les rôles de travail, nous vous recommandons de spécifier `*` comme *version du système d’exploitation* afin que les nœuds soient automatiquement mis à niveau et qu’aucun travail supplémentaire ne soit requis pour gérer ces nouvelles versions. La principale raison de sélectionner une version de système d’exploitation spécifique est d’assurer la compatibilité des applications, ce qui permet aux tests de compatibilité descendante d’être réalisés avant d’autoriser la mise à jour de la version. Une fois validée, la *version du système d’exploitation* du pool peut être mise à jour et la nouvelle image du système d’exploitation peut être installée. Toutes les tâches en cours d’exécution sont interrompues et remises en file d’attente.

Lorsque vous créez un pool, vous devez sélectionner la valeur **nodeAgentSkuId** appropriée, selon le système d’exploitation de l’image de base de votre VHD. Pour obtenir un mappage des ID de référence SKU d’agent de nœud disponible sur les références des images de système d’exploitation, appelez l’opération permettant de [répertorier les références SKU d’agent de nœud prises en charge](https://docs.microsoft.com/rest/api/batchservice/list-supported-node-agent-skus).

Consultez la section relative au [compte](#account) pour en savoir plus sur la définition du mode d’allocation de pool lorsque vous créez un compte Batch.

#### <a name="custom-images-for-virtual-machine-pools"></a>Images personnalisées pour les pools de machines virtuelles

Pour pouvoir utiliser des images personnalisées pour vos pools de machines virtuelles, créez votre compte Batch avec le mode d’allocation de pool Abonnement utilisateur. Grâce à ce mode, les pools Batch sont alloués au sein de l’abonnement où se trouve le compte. Consultez la section relative au [compte](#account) pour en savoir plus sur la définition du mode d’allocation de pool lorsque vous créez un compte Batch.

Pour utiliser une image personnalisée, vous devez préparer l’image en la généralisant. Pour en savoir plus sur la préparation d’images Linux personnalisées à partir de machines virtuelles Azure, consultez la section [Capturer une machine virtuelle Linux exécutée sur Azure](../virtual-machines/linux/capture-image-nodejs.md). Pour plus d’informations sur la préparation d’images Windows personnalisées à partir de machines virtuelles Azure, consultez la section [Créer une image personnalisée d’une machine virtuelle Azure à l’aide de PowerShell](../virtual-machines/windows/tutorial-custom-images.md). 

> [!IMPORTANT]
> Lors de la préparation de votre image personnalisée, gardez à l’esprit les points suivants :
> - Vérifiez que l’image de base du système d’exploitation utilisée pour approvisionner les pools Batch ne comporte pas d’extensions Azure préinstallées, telle que l’extension Script personnalisé. Si l’image contient une extension préinstallée, Azure peut rencontrer des problèmes de déploiement de la machine virtuelle.
> - Assurez-vous que l’image de base du système d’exploitation utilise le lecteur temporaire par défaut, puisque l’agent de nœud Batch attend actuellement ce lecteur.
>
>

Pour créer un pool de configuration de machines virtuelles à l’aide d’une image personnalisée, vous devez disposer au minimum d’un compte de stockage Microsoft Azure standard, dans lequel stocker vos images VHD personnalisées. Les images personnalisées sont stockées en tant que blobs. Pour faire référence à vos images personnalisées lorsque vous créez un pool, spécifiez les URI des blobs VHD d’images personnalisées pour la propriété [osDisk](https://docs.microsoft.com/rest/api/batchservice/add-a-pool-to-an-account#bk_osdisk) de la propriété [virtualMachineConfiguration](https://docs.microsoft.com/rest/api/batchservice/add-a-pool-to-an-account#bk_vmconf).

Assurez-vous que vos comptes de stockage répondent aux critères suivants :   

- Les comptes de stockage contenant des blobs VHD d’images personnalisées doivent se trouver dans le même abonnement que le compte Batch (abonnement utilisateur).
- Les comptes de stockage spécifiés doivent se trouver dans la même région que le compte Batch.
- Actuellement, seuls les comptes de stockage standards sont pris en charge. Nous prendrons prochainement en charge le stockage Azure Premium.
- Vous pouvez spécifier un compte de stockage avec plusieurs blobs VHD personnalisés, ou plusieurs comptes de stockage incluant un seul blob. Nous vous recommandons d’utiliser plusieurs comptes de stockage, afin d’optimiser les performances.
- Un seul blob VHD d’images personnalisées peut gérer jusqu’à 40 instances de machines virtuelles Linux, ou 20 instances de machines virtuelles Windows. Vous devez créer des copies des blobs VHD pour pouvoir générer des pools incluant plusieurs machines virtuelles. Par exemple, un pool incluant 200 machines virtuelles Windows requiert la spécification de 10 blobs VHD uniques pour la propriété **osDisk**.

Pour créer un pool à partir d’une image personnalisée, à l’aide du portail Azure, procédez comme suit :

1. Accédez à votre compte  Batch dans le portail Azure.
2. Dans le panneau **Paramètres**, sélectionnez l’élément de menu **Pools**.
3. Sur le panneau **Pools**, sélectionnez la commande **Ajouter**. Le panneau **Ajouter un pool** s’affiche.
4. Sélectionnez l’option **Image personnalisée (Linux/Windows)** dans la liste déroulante **Type d’image**. Le portail affiche le sélecteur **Image personnalisée**. Choisissez un ou plusieurs VHD dans le même conteneur et cliquez sur le bouton **Sélectionner**. 
    La prise en charge de plusieurs VHD à partir de plusieurs comptes de stockage et conteneurs différents sera assurée prochainement.
5. Sélectionnez les valeurs **d’éditeur/d’offre/de référence SKU** adéquates de vos VHD personnalisés, choisissez le mode de **mise en cache**, puis indiquez l’ensemble des autres paramètres du pool.
6. Pour vérifier si un pool est basé sur une image personnalisée, consultez la propriété relative au **système d’exploitation** dans la section Récapitulatif des ressources du panneau **Pool**. La valeur de cette propriété doit être **Image de machine virtuelle personnalisée**.
7. Tous les VHD associés à un pool sont affichés sur le panneau **Propriétés** de ce dernier.

### <a name="compute-node-type-and-target-number-of-nodes"></a>Type de nœud de calcul et nombre cible de nœuds

Lorsque vous créez un pool, vous pouvez spécifier les types de nœuds de calcul souhaités et le nombre cible pour chacun. Les deux types de nœuds de calcul sont les suivants :

- **Nœuds de calcul dédiés.** Les nœuds de calcul dédiés sont réservés à vos charges de travail. Ils sont plus chers que les nœuds à faible priorité, mais sont assurés de ne jamais être reportés.

- **Nœuds de calcul à faible priorité.** Les nœuds à faible priorité tirent profit de la capacité excédentaire dans Azure pour exécuter vos charges de travail par lots. Le coût horaire des nœuds à faible priorité est moins élevé que celui des nœuds dédiés. Par ailleurs, ces nœuds activent des charges de travail nécessitant une importante puissance de calcul. Pour plus d’informations, consultez [Utiliser des machines virtuelles à faible priorité avec Batch](batch-low-pri-vms.md).

    Les nœuds de calcul à faible priorité peuvent être reportés lorsque Azure n’a pas suffisamment de capacité excédentaire. Si un nœud est reporté lors de l’exécution de tâches, celles-ci sont remises dans la file d’attente et exécutées à nouveau dès qu’un nœud de calcul redevient disponible. Les nœuds à faible priorité sont intéressants pour les charges de travail pour lesquelles l’heure d’achèvement est flexible et le travail est réparti entre plusieurs nœuds. Avant de décider d’utiliser des nœuds à faible priorité pour votre scénario, assurez-vous que le nombre de tâches risquant d’être perdues sera peu élevé, et que ces tâches seront faciles à recréer, le cas échéant.

    Les nœuds de calcul à faible priorité sont disponibles uniquement pour les comptes Batch créés avec le mode d’allocation de pool défini sur **Service Batch**.

Un même pool peut contenir des nœuds de calcul dédiés et à faible priorité. Chaque type de nœud &mdash; dédié et à faible priorité &mdash; a son propre paramètre de cible pour lequel vous pouvez spécifier le nombre de nœuds souhaité. 
    
Le nombre de nœuds de calcul est appelé *cible* car, dans certaines situations, votre pool ne pourra peut-être pas atteindre le nombre de nœuds souhaité. Par exemple, un pool ne pourra peut-être pas atteindre la cible s’il atteint d’abord le [quota de base](batch-quota-limit.md) de votre compte Batch ou si vous avez appliqué au pool une formule de mise à l’échelle automatique qui limite le nombre maximal de nœuds.

Pour obtenir les informations de tarification des nœuds de calcul dédiés et à faible priorité, consultez [Tarification du service Batch](https://azure.microsoft.com/pricing/details/batch/).

### <a name="size-of-the-compute-nodes"></a>Taille des nœuds de calcul

**Configuration de Cloud Services** sont répertoriées dans [Tailles de services cloud](../cloud-services/cloud-services-sizes-specs.md). Le service Batch prend en charge l’ensemble des tailles de services cloud, à l’exception de `ExtraSmall`, `STANDARD_A1_V2` et `STANDARD_A2_V2`.

Les tailles de nœud de calcul de la **configuration de machines virtuelles** sont répertoriées dans [Tailles des machines virtuelles dans Azure](../virtual-machines/linux/sizes.md) (Linux) et [Tailles des machines virtuelles dans Azure](../virtual-machines/windows/sizes.md) (Windows). Le service Batch prend en charge l’ensemble des tailles de machine virtuelle Azure, à l’exception de `STANDARD_A0` et de celles comprises dans Premium Storage (série `STANDARD_GS`, `STANDARD_DS`, et `STANDARD_DSV2`).

Lorsque vous sélectionnez une taille de nœud de calcul, tenez compte des caractéristiques et des exigences des applications que vous allez exécuter sur les nœuds. Des aspects tels que la nature multithread de l’application et le volume de mémoire utilisé vous aideront à déterminer la taille de nœud la mieux adaptée et la plus rentable. La taille du nœud est souvent sélectionnée en supposant qu’une tâche s’exécutera sur un nœud à la fois. Cependant, plusieurs tâches (et par conséquent, plusieurs instances d’application) peuvent [s’exécuter en parallèle](batch-parallel-node-tasks.md) sur les nœuds de calcul lors de l’exécution du travail. Dans ce cas, il est courant de choisir une plus grande taille de nœud pour prendre en charge la demande accrue de l’exécution parallèle des tâches. Pour plus d’informations, consultez la section [Stratégie de planification de tâches](#task-scheduling-policy).

Tous les nœuds du pool ont la même taille. Si vous prévoyez d’exécuter des applications dont la configuration système requise et/ou les niveaux de charge diffèrent, nous vous recommandons d’utiliser des pools distincts.

### <a name="scaling-policy"></a>Stratégie de mise à l’échelle

Pour les charges de travail dynamiques, vous pouvez écrire et appliquer une [formule de mise à l’échelle automatique](#scaling-compute-resources) à un pool. Le service Batch évalue régulièrement la formule et ajuste le nombre de nœuds dans le pool en fonction de différents paramètres de pool, de travail et de tâche que vous pouvez spécifier.

### <a name="task-scheduling-policy"></a>Stratégie de planification des tâches

L’option de configuration [Nombre maximal de tâches par nœud](batch-parallel-node-tasks.md) détermine le nombre maximal de tâches qui peuvent être exécutées en parallèle sur chaque nœud de calcul au sein du pool.

La configuration par défaut prévoit de n’exécuter qu’une seule tâche à la fois sur un nœud. Toutefois, dans certains scénarios, il est préférable d’exécuter plusieurs tâches simultanément sur un nœud. Consultez [l’exemple de scénario](batch-parallel-node-tasks.md#example-scenario) de l’article sur les [tâches de nœud simultanées](batch-parallel-node-tasks.md) pour découvrir comment tirer parti de plusieurs tâches par nœud.

Vous pouvez également spécifier un *type de remplissage* qui détermine si l’option Batch répartit les tâches uniformément sur tous les nœuds dans un pool, ou remplit chaque nœud avec le nombre maximal de tâches avant d’affecter des tâches à un autre nœud.

### <a name="communication-status-for-compute-nodes"></a>État de communication des nœuds de calcul

Dans la plupart des scénarios, les tâches fonctionnent indépendamment et n’ont pas besoin de communiquer les unes avec les autres. Cependant, il existe des applications dans lesquelles les tâches doivent communiquer, par exemple les [scénarios impliquant des applications MPI](batch-mpi.md).

Vous pouvez configurer un pool en activant la **communication entre nœuds** afin de permettre aux nœuds du pool de communiquer au moment de l’exécution. Lorsque la communication entre les nœuds est activée, les nœuds des pools Configuration de Cloud Services peuvent communiquer entre eux sur les ports supérieurs à 1100, et les pools Configuration de la machine virtuelle ne limitent pas le trafic sur les ports.

Notez que l’activation de la communication entre les nœuds affecte également le placement des nœuds au sein des clusters et peut limiter le nombre maximal de nœuds dans un pool en raison des restrictions de déploiement. Si votre application ne nécessite pas de communication entre les nœuds, le service Batch peut éventuellement allouer au pool un grand nombre de nœuds issus de différents centres de données et clusters pour accroître la puissance de traitement parallèle.

### <a name="start-tasks-for-compute-nodes"></a>Tâches de démarrage des nœuds de calcul

La *tâche de démarrage* facultative s’exécute sur chacun des nœuds rejoignant le pool, ainsi qu’à chaque redémarrage ou réinitialisation d’un nœud. La tâche de démarrage est particulièrement utile pour la préparation des nœuds de calcul à l’exécution de tâches, comme l’installation des applications que vos tâches exécutent sur les nœuds de calcul.

### <a name="application-packages"></a>packages d’application

Vous pouvez spécifier des [packages d’applications](#application-packages) à déployer sur les nœuds de calcul dans le pool. Les packages d’applications permettent un déploiement simplifié et le contrôle de version des applications exécutées par vos tâches. Les packages d’applications que vous spécifiez pour un pool sont installés sur chaque nœud qui rejoint le pool, et à chaque fois qu’un nœud est redémarré ou réinitialisé.

> [!NOTE]
> Les packages d’applications sont pris en charge sur tous les pools Batch créés après le 5 juillet 2017. Ils sont pris en charge sur les pools Batch créés entre le 10 mars 2016 et le 5 juillet 2017 uniquement si le pool a été créé à l’aide d’une configuration de service cloud. Les pools Batch créés avant le 10 mars 2016 ne prennent pas en charge les packages d’applications. Pour plus d’informations sur l’utilisation de packages d’applications pour déployer vos applications sur vos nœuds Batch, consultez [Déployer des applications sur les nœuds avec des packages d’applications Batch](batch-application-packages.md).
>
>

### <a name="network-configuration"></a>Configuration réseau

Vous pouvez spécifier le sous-réseau d’un [réseau virtuel (VNet)](../virtual-network/virtual-networks-overview.md) Azure dans lequel les nœuds de calcul du pool doivent être créés. Pour plus d'informations, consultez [Configuration du réseau de pools](#pool-network-configuration).


## <a name="job"></a>Travail
Un travail est une collection de tâches. Il gère la façon dont le calcul est effectué par ses tâches sur les nœuds de calcul d’un pool.

* Le travail spécifie le **pool** sur lequel le travail doit être exécuté. Vous pouvez créer un nouveau pool pour chaque tâche, ou utiliser un pool pour plusieurs travaux. Vous pouvez créer un pool pour chaque travail associé à une planification de travail, ou pour tous les travaux associés à une planification de travail.
* Une **priorité de travail**facultative peut être spécifiée. Quand un travail dont la priorité est supérieure à celle des autres travaux en cours est envoyé, les tâches du travail dont la priorité est la plus élevée sont insérées dans la file d’attente devant les tâches des travaux de priorité inférieure. Les tâches des travaux de priorité inférieure qui sont déjà en cours d’exécution ne sont pas reportées.
* Vous pouvez utiliser des **contraintes** de travail pour spécifier certaines limites pour vos travaux :

    Vous pouvez définir une **durée maximale**pour les travaux ; si la durée d’exécution du travail est supérieure à la durée maximale spécifiée, le travail et toutes les tâches qui lui sont associées seront terminés.

    Le service Batch peut détecter, puis relancer des tâches ayant échoué. Vous pouvez spécifier le **nombre maximal de nouvelles tentatives de tâche** en tant que contrainte, et indiquer notamment si une tâche doit *toujours* être systématiquement relancée ou ne *jamais* l’être. Lorsqu’une tâche est relancée, cela signifie qu’elle est remise en file d’attente afin d’être réexécutée.
* Votre application cliente peut ajouter des tâches à un travail. Vous pouvez également spécifier une [tâche du gestionnaire de travaux](#job-manager-task). Une tâche de ce type contient les informations nécessaires à la création des tâches requises pour un travail et elle s’exécute sur l’un des nœuds de calcul du pool. La tâche du gestionnaire de travaux est gérée spécifiquement par Batch : elle est mise en file d’attente dès que le travail est créé et elle est redémarrée en cas d’échec. Une tâche du gestionnaire de travaux est *requise* pour les travaux créés dans le cadre d’une [planification de travail](#scheduled-jobs), car il s’agit du seul moyen de définir les tâches avant que le travail ne soit instancié.
* Par défaut, l’état des tâches est maintenu comme actif lorsque toutes les tâches du travail sont terminées. Vous pouvez modifier cette configuration pour terminer automatiquement le travail lorsque toutes les tâches afférentes ont été accomplies. Définissez la propriété **onAllTasksComplete** du travail ([OnAllTasksComplete][net_onalltaskscomplete] dans .NET Batch) sur *terminatejob* pour terminer automatiquement le travail lorsque l’état de toutes les tâches afférentes est défini comme terminé.

    Notez que le service Batch considère les travaux ne présentant *aucune* tâche comme des travaux dont toutes les tâches sont terminées. C’est la raison pour laquelle cette option est généralement utilisée avec une [tâche de gestionnaire de travaux](#job-manager-task). Si vous souhaitez définir l’arrêt automatique d’un travail sans utiliser de gestionnaire de travaux, définissez initialement la propriété **onAllTasksComplete** d’un nouveau travail sur *noaction*, puis sur *terminatejob* seulement une fois que vous avez terminé d’ajouter des tâches au travail.

### <a name="job-priority"></a>priorité de travail
Vous pouvez établir une priorité pour les travaux que vous créez dans Batch. Le service Batch utilise les valeurs de priorité du travail pour déterminer l’ordre de planification du travail dans un compte (à ne pas confondre avec le [travail planifié](#scheduled-jobs)). Les valeurs de priorité sont comprises entre -1000 et 1000, -1000 étant la priorité la plus basse et 1000 la plus élevée. Pour mettre à jour la priorité d’un travail, appelez l’opération [Mettre à jour les propriétés d’un travail][rest_update_job] (REST Batch) ou modifiez la propriété [CloudJob.Priority][net_cloudjob_priority] (.NET Batch).

Dans un même compte, les travaux de priorité supérieure sont prioritaires en termes de planification sur les travaux de priorité inférieure. Un travail à priorité supérieure dans un compte n’est pas prioritaire en termes de planification sur un autre travail à priorité inférieure dans un autre compte.

La planification de travail entre pools est indépendante. Entre des pools différents, un travail à priorité supérieure n’est pas systématiquement planifié en premier si le pool auquel il est associé n’a pas suffisamment de nœuds inactifs. Dans le même pool, les travaux avec le même niveau de priorité ont autant de chance d’être planifiés.

### <a name="scheduled-jobs"></a>Scheduled jobs
Les [planifications de travaux][rest_job_schedules] vous permettent de créer des travaux périodiques au sein du service Batch. Une planification de travail indique le moment où exécuter des tâches et les spécifications des travaux à exécuter. Vous pouvez spécifier la durée de la planification (durée proprement dite et date d’entrée en vigueur de la planification), ainsi que la fréquence de création des travaux au cours de la période de planification.

## <a name="task"></a>Task
Une tâche est une unité de calcul associée à un travail. Elle s’exécute sur un nœud. Les tâches sont affectées à un nœud afin d’être exécutées ou sont mises en file d’attente jusqu’à ce qu’un nœud soit disponible. Une tâche exécute un ou plusieurs programmes ou scripts sur un nœud de calcul afin d’effectuer le travail nécessaire.

Lorsque vous créez une tâche, vous pouvez spécifier les éléments suivants :

* **Ligne de commande** de la tâche. Il s’agit de la ligne de commande qui exécute votre application ou script sur le nœud de calcul.

    Il est important de noter que la ligne de commande ne s’exécute pas réellement sous un interpréteur de commandes. Elle ne peut donc pas tirer parti en mode natif des fonctionnalités de l’interpréteur de commandes, comme l’expansion de [variables d’environnement](#environment-settings-for-tasks) (qui inclut le `PATH`). Pour tirer parti de ces fonctionnalités, vous devez appeler l’interpréteur de commandes dans la ligne de commande, par exemple, en lançant `cmd.exe` sur les nœuds Windows ou `/bin/sh` sur Linux :

    `cmd /c MyTaskApplication.exe %MY_ENV_VAR%`

    `/bin/sh -c MyTaskApplication $MY_ENV_VAR`

    Si vos tâches doivent exécuter une application ou un script hors du `PATH` du nœud ou référencer des variables d’environnement, appelez l’interpréteur de commandes explicitement dans la ligne de commande de la tâche.
* **Fichiers de ressources** contenant les données à traiter. Ces fichiers sont automatiquement copiés sur le nœud à partir de Stockage Blob dans un compte Stockage Azure à usage général avant l’exécution de la ligne de commande de la tâche. Pour plus d’informations, consultez les sections [Tâche de démarrage](#start-task) et [Fichiers et répertoires](#files-and-directories).
* Les **variables d’environnement** requises par l’application. Pour plus d’informations, consultez la section [Paramètres d’environnement des tâches](#environment-settings-for-tasks) .
* Les **contraintes** sous lesquelles la tâche doit s’exécuter. Les contraintes comprennent notamment la durée maximale pendant laquelle la tâche est autorisée à s’exécuter, le nombre maximal de nouvelles tentatives en cas d’échec de la tâche, ainsi que la durée maximale de conservation des fichiers dans le répertoire de travail de la tâche.
* **Packages d’applications** à déployer sur le nœud de calcul sur lequel l’exécution de la tâche est planifiée. [Application packages](#application-packages) permettent le déploiement simplifié et le contrôle de version des applications exécutées par vos tâches. Les packages d’applications au niveau des tâches sont particulièrement utiles dans les environnements de pool partagé, où différentes tâches sont exécutées sur un même pool et le pool n’est pas supprimé lorsqu’un travail est terminé. Si votre travail présente moins de tâches que le pool ne contient de nœuds, les packages d’applications au niveau des tâches peuvent réduire le transfert de données, votre application n’étant déployée que sur les nœuds exécutant les tâches.

Outre les tâches que vous pouvez définir pour effectuer des calculs sur un nœud, les tâches spéciales suivantes sont également fournies par le service Batch :

* [Tâche de démarrage](#start-task)
* [Tâche du gestionnaire de travaux](#job-manager-task)
* [Tâches de préparation et lancement](#job-preparation-and-release-tasks)
* [Tâches multi-instances (MPI)](#multi-instance-tasks)
* [Dépendances de la tâche](#task-dependencies)

### <a name="start-task"></a>Tâche de démarrage
En associant une **tâche de démarrage** à un pool, vous pouvez préparer l’environnement d’exploitation de ses nœuds. Par exemple, vous pouvez effectuer des opérations telles que l’installation des applications que vos tâches exécuteront ou le démarrage des processus d’arrière-plan. La tâche de démarrage s’exécute à chaque démarrage d’un nœud tant qu’il reste dans le pool, notamment lorsque le nœud est ajouté au pool en premier lieu, redémarré ou réinitialisé.

Le principal avantage de la tâche de démarrage est qu’elle peut contenir toutes les informations nécessaires pour configurer un nœud de calcul et installer les applications requises pour l’exécution de la tâche. L’augmentation du nombre de nœuds dans un pool revient donc tout simplement à spécifier le nouveau nombre de nœuds cible. La tâche de démarrage fournit au service Batch les informations nécessaires pour la configuration des nouveaux nœuds et pour leur préparation à l’acceptation des tâches.

Comme dans le cas de n’importe quelle tâche Azure Batch, vous pouvez spécifier une liste de **fichiers de ressources** dans [Stockage Azure][azure_storage], en plus d’une **ligne de commande** à exécuter. Le service Batch commence par copier les fichiers de ressources sur le nœud à partir de Stockage Azure, puis exécute la ligne de commande. Pour une tâche de démarrage de pool, la liste des fichiers contient généralement l’application de la tâche et ses dépendances.

Toutefois, la tâche de démarrage peut également inclure des données de référence qui doivent être utilisées par toutes les tâches exécutées sur le nœud de calcul. Par exemple, la ligne de commande d’une tâche de démarrage peut effectuer une opération `robocopy` afin de copier les fichiers d’application (qui ont été spécifiés comme fichiers de ressources et téléchargés vers le nœud) à partir du [répertoire de travail](#files-and-directories) de la tâche de démarrage vers le [dossier partagé](#files-and-directories), puis exécuter un MSI ou `setup.exe`.

Il est généralement préférable pour le service Batch d’attendre que la tâche de démarrage soit terminée avant de considérer que le nœud est prêt à recevoir des tâches, mais vous pouvez configurer ce paramètre.

Si une tâche de démarrage échoue sur un nœud du pool, l’état du nœud est mis à jour pour refléter l’échec et aucune tâche n’est affectée au nœud. Une tâche de démarrage peut échouer en cas de problème de copie des fichiers de ressources depuis le stockage, ou si le processus exécuté par sa ligne de commande retourne un code de sortie différent de zéro.

Si vous ajoutez ou mettez à jour la tâche de démarrage pour un pool existant, vous devez redémarrer ses nœuds de calcul pour que cette tâche soit appliquée aux nœuds.

>[!NOTE]
> La taille totale d’une tâche de démarrage doit être inférieure ou égale à 32 768 caractères, y compris les fichiers de ressources et les variables d’environnement. Pour vous assurer que votre tâche de démarrage répond à cette exigence, vous pouvez utiliser l’une des deux approches suivantes :
>
> 1. Utilisez des packages d’application pour distribuer des applications ou des données sur chaque nœud de votre pool  Batch. Pour en savoir plus sur les packages d’applications, consultez [Déployer des applications sur les nœuds avec des packages d’applications Batch](batch-application-packages.md).
> 2. Vous pouvez créer manuellement une archive au format ZIP contenant vos fichiers d’applications. Chargez l’archive ZIP dans le stockage Azure, en tant que blob. Spécifiez cette archive sous la forme d’un fichier de ressources pour votre tâche de démarrage. Avant d’exécuter la ligne de commande pour votre tâche de démarrage, décompressez l’archive à partir de la ligne de commande. 
>
>    Pour ce faire, vous pouvez utiliser l’outil d’archivage de votre choix. Vous devez inclure l’outil qui vous permet de décompresser l’archive en tant que fichier de ressources pour la tâche de démarrage.
>
>

### <a name="job-manager-task"></a>Tâche du gestionnaire de travaux
Vous utilisez généralement une **tâche du gestionnaire de travaux** pour contrôler et/ou surveiller l’exécution des travaux, par exemple, pour créer et soumettre les tâches d’un travail, identifier les autres tâches à exécuter et déterminer lorsque le travail est terminé. Toutefois, une tâche du gestionnaire de travaux n’est pas limitée à ces activités. C’est une tâche à part entière qui peut effectuer toutes les actions requises pour le travail. Par exemple, une tâche du gestionnaire de travaux peut télécharger un fichier spécifié en tant que paramètre, en analyser le contenu et soumettre des tâches supplémentaires en fonction de ce contenu.

Une tâche du gestionnaire de travaux est lancée avant toutes les autres tâches. Elle fournit les fonctionnalités suivantes :

* Elle est automatiquement soumise en tant que tâche par le service Batch lorsque le travail est créé.
* Elle est planifiée pour s’exécuter avant les autres tâches d’un projet.
* Le nœud associé est le dernier à être supprimé d’un pool lorsque la taille de ce dernier diminue.
* Son arrêt peut être lié à l'arrêt de toutes les tâches du travail.
* Une tâche de gestionnaire de travaux reçoit la priorité la plus élevée lorsqu’elle doit être redémarrée. Si aucun nœud inactif n’est disponible, le service Batch peut mettre fin à une tâche en cours d’exécution dans le pool pour libérer de l’espace pour l’exécution de la tâche du gestionnaire de travaux.
* Une tâche du gestionnaire de travaux associée à un travail n’a pas la priorité sur les tâches d’autres travaux. Parmi les travaux, seules les priorités au niveau du travail sont observées.

### <a name="job-preparation-and-release-tasks"></a>Tâches de préparation et lancement
Batch fournit des tâches de préparation des travaux pour la configuration de l’exécution des travaux préliminaire. Les tâches de validation des travaux sont destinées à la maintenance ou au nettoyage postérieurs aux travaux.

* **Tâche de préparation de travail**: une tâche de préparation de travail s’exécute sur tous les nœuds de calcul qui sont planifiés pour exécuter les tâches avant l’exécution des autres tâches du travail. Vous pouvez utiliser une tâche de préparation du travail pour copier les données partagées par toutes les tâches, mais propres au travail, par exemple.
* **Tâche de validation de travail**: lorsqu’un travail est terminé, une tâche de validation de travail s’exécute sur chaque nœud du pool ayant exécuté au moins une tâche. Vous pouvez utiliser une tâche de validation de travail pour supprimer les données copiées par la tâche de préparation de travail, ou pour compresser et charger des données de journaux de diagnostic, par exemple.

Les tâches de préparation et de validation de travail vous permettent de spécifier une ligne de commande à exécuter lorsque la tâche est appelée. Elles offrent des fonctionnalités telles que le téléchargement de fichiers, une exécution élevée, des variables d’environnement personnalisées, une durée d’exécution maximale, le nombre de tentatives et la durée de rétention des fichiers.

Pour plus d’informations sur les tâches de préparation de travail et de validation, consultez [Exécuter les tâches de préparation de travail et de validation sur les nœuds de calcul Azure Batch](batch-job-prep-release.md).

### <a name="multi-instance-task"></a>Tâche multi-instance
Une [tâche multi-instance](batch-mpi.md) est une tâche configurée pour s’exécuter simultanément sur plusieurs nœuds de calcul. Avec des tâches multi-instances, vous pouvez permettre des scénarios de calcul haute performance qui requièrent un groupe de nœuds de calcul alloués ensemble pour traiter une seule et même charge de travail (comme MPI).

Pour une présentation détaillée de l’exécution des travaux MPI dans Batch à l’aide de la bibliothèque .NET Batch, consultez l’article [Utiliser les tâches multi-instances pour exécuter des applications MPI (Message Passing Interface) dans Azure Batch](batch-mpi.md).

### <a name="task-dependencies"></a>Dépendances de la tâche
La [dépendance entre tâches](batch-task-dependencies.md), comme son nom l’indique, vous permet de préciser que l’exécution d’une tâche dépend de l’achèvement préalable d’autres tâches. Cette fonctionnalité prend en charge des situations dans lesquelles une tâche « en aval » consomme la sortie d’une tâche « en amont », ou lorsqu’une tâche en amont effectue une initialisation requise par une tâche en aval. Pour utiliser cette fonctionnalité, vous devez d’abord activer les dépendances de tâche sur la tâche Batch. Ensuite, pour chaque tâche qui dépend d’une autre (ou de plusieurs autres), vous devez spécifier les tâches dont elle dépend.

Avec l’interdépendance des tâches, vous pouvez configurer des scénarios tels que :

* *taskB* dépend de *taskA* (l’exécution de *taskB* ne commence pas tant que celle de *taskA* n’est pas terminée).
* *taskC* dépend de *taskA* et de *taskB*.
* *taskD* dépend d’une plage de tâches, notamment des tâches *1* à *10* avant de pouvoir s’exécuter.

Pour plus d’informations détaillées sur cette fonctionnalité, consultez l’article [Dépendances de tâches dans Azure Batch](batch-task-dependencies.md) et l’exemple de code [TaskDependencies][github_sample_taskdeps] dans le référentiel GitHub [azure-batch-samples][github_samples].

## <a name="environment-settings-for-tasks"></a>Paramètres d’environnement des tâches
Chaque tâche exécutée par le service Batch a accès aux variables d’environnement définies sur les nœuds de calcul. Cela inclut les variables d’environnement définies par le service Batch (voir [cet article][msdn_env_vars]) et les variables d’environnement personnalisées que vous pouvez définir pour vos tâches. Les applications et les scripts que vos tâches exécutent sur les nœuds ont accès à ces variables d’environnement pendant l’exécution.

Vous pouvez définir des variables d’environnement personnalisées au niveau de la tâche ou du travail en remplissant la propriété de *paramètres d’environnement* pour ces entités. Par exemple, consultez l’opération [Ajouter une tâche à un travail][rest_add_task] (API REST Batch) ou les propriétés [CloudTask.EnvironmentSettings][net_cloudtask_env] et [CloudJob.CommonEnvironmentSettings][net_job_env] dans .NET Batch.

L’application cliente ou le service peuvent obtenir des variables d’environnement d’une tâche, à la fois définies par le service et personnalisées, à l’aide de l’opération [Obtenir des informations sur une tâche][rest_get_task_info] (REST Batch) ou en accédant à la propriété [CloudTask.EnvironmentSettings][net_cloudtask_env] (.NET Batch). Les processus qui s’exécutent sur un nœud de calcul peuvent accéder à ces dernières ainsi qu’à d’autres variables d’environnement sur le nœud, par exemple à l’aide de la syntaxe classique `%VARIABLE_NAME%` (Windows) ou la syntaxe `$VARIABLE_NAME` (Linux).

Vous trouverez la liste complète des variables d’environnement définies par le service dans l’article [Compute node environment variables][msdn_env_vars] (Variables d’environnement de nœud de calcul).

## <a name="files-and-directories"></a>Fichiers et répertoires
Chaque tâche possède un *répertoire de travail* sous lequel elle crée zéro ou plusieurs fichiers et répertoires. Ce répertoire de travail peut être utilisé pour stocker le programme exécuté par la tâche, les données qu’il traite et la sortie du traitement qu’il effectue. Tous les fichiers et répertoires d’une tâche sont détenus par l’utilisateur de la tâche.

Le service Batch expose une partie du système de fichiers sur un nœud en tant que *répertoire racine*. Les tâches peuvent accéder au répertoire racine en référençant la variable d’environnement `AZ_BATCH_NODE_ROOT_DIR` . Pour plus d’informations sur l’utilisation de variables d’environnement, consultez la section [Paramètres d’environnement des tâches](#environment-settings-for-tasks).

Le répertoire racine contient la structure de répertoires suivante :

![Structure de répertoire du nœud de calcul][1]

* **Partagé**: ce répertoire fournit un accès en lecture/écriture à *toutes* les tâches qui s’exécutent sur un nœud. Les tâches qui s’exécutent sur le nœud peuvent créer, lire, mettre à jour et supprimer des fichiers dans ce répertoire. Les tâches peuvent accéder à ce répertoire en référençant la variable d’environnement `AZ_BATCH_NODE_SHARED_DIR` .
* **Démarrage**: ce répertoire est utilisé par une tâche de démarrage en tant que répertoire de travail. Tous les fichiers téléchargés vers le nœud par la tâche de démarrage sont stockés ici. La tâche de démarrage peut créer, lire, mettre à jour et supprimer des fichiers dans ce répertoire. Les tâches peuvent accéder à ce répertoire en référençant la variable d’environnement `AZ_BATCH_NODE_STARTUP_DIR` .
* **Tâches**: un répertoire est créé pour chaque tâche qui s’exécute sur le nœud. Il est accessible en référençant la variable d’environnement `AZ_BATCH_TASK_DIR` .

    Dans chaque répertoire de la tâche, le service Batch crée un répertoire de travail (`wd`) dont le chemin unique est spécifié par la variable d’environnement `AZ_BATCH_TASK_WORKING_DIR`. Ce répertoire fournit un accès en lecture/écriture à la tâche. La tâche peut créer, lire, mettre à jour et supprimer des fichiers dans ce répertoire. Ce répertoire est conservé en fonction de la contrainte *RetentionTime* spécifiée pour la tâche.

    `stdout.txt` et `stderr.txt` : ces fichiers sont écrits dans le dossier des tâches lors de l’exécution de la tâche.

> [!IMPORTANT]
> Lorsqu’un nœud est supprimé du pool, *tous* les fichiers stockés sur ce nœud sont supprimés.
>
>

## <a name="application-packages"></a>packages d’application
La fonctionnalité [packages d’application](batch-application-packages.md) facilite la gestion et le déploiement d’applications sur les nœuds de calcul dans vos pools. Vous pouvez facilement charger et gérer plusieurs versions des applications exécutées par vos tâches, notamment leurs fichiers binaires et leurs fichiers de prise en charge. Vous pouvez ensuite déployer automatiquement une ou plusieurs de ces applications sur les nœuds de calcul dans le pool.

Vous pouvez spécifier les packages d’applications au niveau du pool et des tâches. Lorsque vous spécifiez des packages d’applications au niveau du pool, l’application est déployée sur tous les nœuds du pool. Lorsque vous spécifiez des packages d’applications au niveau des tâches, l’application est déployée uniquement sur les nœuds programmés pour exécuter au moins une des tâches du travail, juste avant l’exécution de la ligne de commande de la tâche.

Batch gère les détails de l’utilisation d’Azure Storage en arrière-plan pour stocker vos packages d’applications et les déployer sur les nœuds de calcul, de manière à permettre de simplifier votre code et vos frais de gestion.

Pour en savoir plus sur la fonctionnalité packages d’applications, consultez [Déployer des applications sur les nœuds avec des packages d’applications Batch](batch-application-packages.md).

> [!NOTE]
> Si vous ajoutez des packages de d’applications au niveau du pool à un pool *existant* , vous devez redémarrer ses nœuds de calcul afin que les packages d’applications soient déployés sur les nœuds.
>
>

## <a name="pool-and-compute-node-lifetime"></a>Durée de vie de nœud de pool et de calcul
Lorsque vous créez votre solution Azure Batch, vous devez prendre une décision de conception relative à la procédure et au moment de la création des pools, et à la durée pendant laquelle les nœuds de calcul de ces pools restent disponibles.

D’un côté, vous pouvez créer un pool pour chaque travail que vous soumettez et supprimer le pool dès la fin de l’exécution des tâches associées. Cela permet d’optimiser l’utilisation, car les nœuds sont seulement alloués lorsqu’ils sont requis et sont arrêtés dès qu’ils sont inactifs. Cela signifie que le travail doit attendre que les nœuds soient alloués, mais il est important de noter que l’exécution des tâches est planifiée dès que les nœuds sont individuellement disponibles, alloués, et que la tâche de démarrage est terminée. Batch n’attend *pas* que tous les nœuds d’un pool soient disponibles avant d’affecter des tâches aux nœuds. Cela garantit l’utilisation maximale de tous les nœuds disponibles.

À l’opposé, si la priorité absolue consiste à démarrer immédiatement des travaux, vous pouvez créer un pool avant l’heure et mettre ses nœuds à disposition avant la soumission des travaux. Dans ce scénario, les tâches peuvent démarrer immédiatement, mais il se peut que les nœuds restent inactifs en attendant que les tâches soient affectées.

Une approche combinée est généralement utilisée pour la gestion d’une charge variable, mais continue. Vous pouvez disposer d’un pool auquel plusieurs travaux sont soumis, mais vous pouvez augmenter ou réduire le nombre de nœuds en fonction de la charge de travail (consultez [Mise à l’échelle des ressources de calcul](#scaling-compute-resources) dans la section suivante). Vous pouvez procéder en réaction, en fonction de la charge actuelle, ou en amont, si la charge peut être prédite.

## <a name="virtual-network-vnet-and-firewall-configuration"></a>Configuration du pare-feu et du réseau virtuel (VNet) 

Lorsque vous configurez un pool de nœuds de calcul dans Azure Batch, vous pouvez associer le pool au sous-réseau d’un [réseau virtuel (VNet)](../virtual-network/virtual-networks-overview.md) Azure. Pour en savoir plus sur la création d’un réseau virtuel avec des sous-réseaux, consultez la section [Créer un réseau virtuel Azure comprenant plusieurs sous-réseaux](../virtual-network/virtual-networks-create-vnet-arm-pportal.md). 

 * Le réseau virtuel associé à un pool doit être :

   * Dans la même **région** Azure que le compte Azure Batch.
   * Dans le même **abonnement** que le compte Azure Batch.

* Le type de réseau virtuel pris en charge dépend de la façon dont les pools sont alloués pour le compte Batch :

    - Si le mode d’allocation de pool de votre compte Batch est défini sur le mode Service Batch, vous pouvez alors assigner un réseau virtuel uniquement aux pools créés avec la **Configuration Cloud Services**. En outre, le réseau virtuel spécifié doit être créé suivant le modèle de déploiement classique. Les réseaux virtuels créés avec le modèle de déploiement Azure Resource Manager ne sont pas pris en charge.
 
    - Si le mode d’allocation de pool de votre compte Batch est défini sur le mode Abonnement utilisateur, vous pouvez alors assigner un réseau virtuel uniquement aux pools créés avec la **Configuration de machines virtuelles**. Les pools créés avec la **Configuration du service cloud** ne sont pas pris en charge. Un réseau virtuel associé peut être créé suivant le modèle de déploiement Azure Resource Manager ou le modèle de déploiement classique.

    Pour obtenir un tableau résumant la prise en charge d’un réseau virtuel suivant le mode d’allocation de pool, consultez la section [Mode d’allocation de pool](#pool-allocation-mode).

* Si le mode d’allocation de pool de votre compte Batch est défini sur le mode Service Batch, vous devez alors fournir les autorisations permettant au principal du service Batch d’accéder au réseau virtuel. Le réseau virtuel doit assigner au principal du service Batch le rôle de [contrôle d’accès en fonction du rôle (RBAC) Collaborateur de machine virtuelle classique](https://azure.microsoft.com/documentation/articles/role-based-access-built-in-roles/#classic-virtual-machine-contributor). Si le rôle RBAC spécifié n’est pas fourni, le service Batch renvoie une erreur 400 (Demande incorrecte). Pour ajouter le rôle à partir du portail Azure :

    1. Sélectionnez le **réseau virtuel**, puis **Contrôle d’accès (IAM)** > **Rôles** > **Collaborateur de machine virtuelle classique** > **Ajouter**.
    2. Sur le panneau **Ajouter des autorisations**, sélectionnez le rôle **Collaborateur de machine virtuelle**.
    3. Dans le panneau **Ajouter des autorisations**, recherchez l’API Batch. Recherchez chacune de ces chaînes, jusqu’à ce que vous trouviez l’API :
        1. **MicrosoftAzureBatch**.
        2. **Microsoft Azure Batch**. Les locataires Azure AD les plus récents peuvent utiliser ce nom.
        3. La chaîne **ddbf3205-c6bd-46ae-8127-60eb93363864** correspond à l’ID de l’API Batch. 
    3. Sélectionnez le principal du service d’API Batch. 
    4. Cliquez sur **Enregistrer**.

        ![Assignez le rôle de collaborateur de machine virtuelle au principal du service Batch](./media/batch-api-basics/iam-add-role.png)


* Le sous-réseau spécifié doit avoir suffisamment **d’adresses IP** disponibles pour prendre en compte le nombre total de nœuds cibles ; autrement dit, la somme des propriétés `targetDedicatedNodes` et `targetLowPriorityNodes` du pool. Si le sous-réseau n’a pas suffisamment d’adresses IP disponibles, le service Batch alloue partiellement les nœuds de calcul dans le pool et renvoie une erreur de redimensionnement.

* Le sous-réseau spécifié doit autoriser les communications à partir du service Batch pour pouvoir planifier des tâches sur les nœuds de calcul. Si la communication vers les nœuds de calcul est refusée par un **groupe de sécurité réseau (NSG)** associé au réseau virtuel, le service Batch définit l’état des nœuds de calcul comme **inutilisable**.

* Si le réseau virtuel spécifié possède des **groupes de sécurité réseau** associés et/ou un **pare-feu**, quelques ports système réservés doivent être activés pour les communications entrantes :

- Pour les pools créés avec une configuration de machine virtuelle, activez les ports 29876 et 29877, ainsi que le port 22 pour Linux et le port 3389 pour Windows. 
- Pour les pools créés avec une configuration de service cloud, activez les ports 10100, 20100 et 30100. 
- Activez les connexions sortantes vers Stockage Azure sur le port 443. Aussi, assurez-vous que votre point de terminaison de Stockage Azure peut être résolu par tous les serveurs DNS personnalisés qui traitent votre réseau virtuel. Plus précisément, une URL sous la forme `<account>.table.core.windows.net` doit pouvoir être résolue.

    La table suivante décrit les ports entrants que vous devez activer pour les pools créés avec la configuration de machines virtuelles :

    |    Port(s) de destination    |    Adresse IP source      |    Azure Batch ajoute-t-il des NSG ?    |    Élément requis pour permettre l’utilisation des machines virtuelles ?    |    Action que l’utilisateur doit effectuer   |
    |---------------------------|---------------------------|----------------------------|-------------------------------------|-----------------------|
    |    <ul><li>Pour les pools créés avec la configuration de machines virtuelles : 29876, 29877</li><li>Pour les pools créés avec une configuration de service cloud : 10100, 20100, 30100</li></ul>         |    Adresses IP du rôle de service Batch uniquement |    Oui. Azure Batch ajoute des NSG au niveau des cartes réseau jointes aux machines virtuelles. Ces NSG autorisent le trafic uniquement à partir d’adresses IP du rôle de service Batch. Même si vous ouvrez ces ports au web tout entier, le trafic sera bloqué au niveau de la carte réseau. |    Oui  |  Vous n’avez pas besoin de spécifier un NSG, car Azure Batch autorise uniquement les adresses IP Batch. <br /><br /> Toutefois, si vous ne spécifiez pas de NSG, assurez-vous que ces ports sont ouverts pour le trafic entrant. <br /><br /> Si vous spécifiez le caractère * en tant qu’adresse IP source de votre NSG, Batch ajoute des NSG au niveau des cartes réseau attachées aux machines virtuelles. |
    |    3389, 22               |    Ordinateurs de l’utilisateur, utilisés à des fins de débogage, afin que vous puissiez accéder à distance aux machines virtuelles.    |    Non                                    |    Non                     |    Ajoutez des NSG si vous souhaitez autoriser les utilisateurs à accéder à distance aux machines virtuelles (via RDP/SSH).   |                 

    Le tableau suivant décrit le port de sortie que vous devez activer pour autoriser l’accès au stockage Azure :

    |    Port(s) sortant(s)    |    Destination    |    Azure Batch ajoute-t-il des NSG ?    |    Élément requis pour permettre l’utilisation des machines virtuelles ?    |    Action que l’utilisateur doit effectuer    |
    |------------------------|-------------------|----------------------------|-------------------------------------|------------------------|
    |    443    |    Azure Storage    |    Non    |    Oui    |    Si vous ajoutez des NSG, vérifiez que ce port est ouvert pour le trafic sortant.    |


## <a name="scaling-compute-resources"></a>Mise à l’échelle des ressources de calcul
Avec la [mise à l’échelle automatique](batch-automatic-scaling.md), le service Batch peut ajuster de manière dynamique le nombre de nœuds de calcul d’un pool en fonction de la charge de travail actuelle et de l’utilisation des ressources de votre scénario de calcul. Cela vous permet de réduire le coût global d’exécution de votre application en utilisant uniquement les ressources dont vous avez besoin et en libérant les autres.

Pour activer la mise à l’échelle automatique, écrivez une [formule de mise à l’échelle automatique](batch-automatic-scaling.md#automatic-scaling-formulas) et associez-la à un pool. Le service Batch utilise la formule pour déterminer le nombre cible de nœuds dans le pool pour le prochain intervalle de mise à l’échelle (intervalle que vous pouvez configurer). Vous pouvez spécifier les paramètres de mise à l’échelle automatique pour un pool lorsque vous le créez ou activez la mise à l’échelle sur un pool ultérieurement. Vous pouvez également mettre à jour les paramètres de mise à l’échelle sur un pool compatible avec la mise à l’échelle.

Par exemple, il se peut qu’un travail exige que vous envoyiez un grand nombre de tâches devant être exécutées. Vous pouvez attribuer au pool une formule de mise à l’échelle qui règle le nombre de nœuds du pool en fonction du nombre actuel de tâches en file d’attente et du degré d’achèvement des tâches dans le travail. Le service Batch évalue régulièrement la formule et redimensionne le pool en fonction de la charge de travail et des autres paramètres de votre formule. Le service ajoute des nœuds selon les besoins lorsqu’il existe un grand nombre de tâches en file d’attente, et supprime des nœuds lorsqu’aucune tâche n’est en file d’attente ni en cours d’exécution.

Une formule de mise à l’échelle peut être basée sur les mesures suivantes :

* **mesures temporelles** sont basées sur les statistiques collectées toutes les cinq minutes dans le nombre d’heures spécifié.
* **mesures de ressources** sont basées sur l’utilisation du processeur, de la bande passante et de la mémoire, et sur le nombre de nœuds.
* Les **mesures de tâches** sont basées sur l’état de la tâche, tel que *Active* (en file d’attente), *En cours d’exécution* ou *Terminée*.

Lorsque la mise à l’échelle automatique diminue le nombre de nœuds de calcul dans un pool, vous devez réfléchir aux méthodes pour gérer les tâches s’exécutant au moment de cette opération de réduction. Pour ce faire, Batch fournit une *option de désallocation de nœud* que vous pouvez inclure dans vos formules. Par exemple, vous pouvez spécifier d’arrêter immédiatement les tâches en cours, de les arrêter immédiatement, puis les remettre en file d’attente pour une exécution sur un autre nœud, ou les autoriser à terminer avant la suppression du nœud du pool.

Pour plus d’informations sur la mise à l’échelle automatique d’une application, consultez la section [Mettre automatiquement à l’échelle les nœuds de calcul dans un pool Azure Batch](batch-automatic-scaling.md).

> [!TIP]
> Pour optimiser l’utilisation des ressources de calcul, définissez à zéro le nombre cible de nœuds à la fin d’un travail tout en autorisant les tâches en cours à s’achever.
>
>

## <a name="security-with-certificates"></a>Sécurité avec certificats
En principe, vous devez utiliser des certificats lorsque vous chiffrez ou déchiffrez des informations sensibles pour les tâches, comme la clé d’un [compte Stockage Azure][azure_storage]. Pour ce faire, vous pouvez installer des certificats sur les nœuds. Les secrets chiffrés sont transmis aux tâches dans les paramètres de ligne de commande ou incorporés dans l’une des ressources et les certificats installés peuvent être utilisés pour les déchiffrer.

Pour ajouter un certificat à un compte Batch, vous utilisez l’opération [Ajouter le certificat][rest_add_cert] (REST Batch) ou la méthode [CertificateOperations.CreateCertificate][net_create_cert] (.NET Batch). Vous pouvez ensuite associer le certificat à un pool existant ou nouveau. Lorsqu’un certificat est associé à un pool, le service Batch installe le certificat sur chaque nœud du pool. Le service Batch installe les certificats appropriés au démarrage du nœud, avant de lancer une tâche quelconque (notamment les tâches de démarrage et celles du gestionnaire de travaux).

Si vous ajoutez des certificats à un pool *existant* , vous devez redémarrer ses nœuds de calcul afin que les certificats soient appliqués aux nœuds.

## <a name="error-handling"></a>Gestion des erreurs
Il peut s’avérer utile de gérer les échecs de tâche et d’application au sein de votre solution Batch.

### <a name="task-failure-handling"></a>Gestion des échecs de tâche
Les échecs de tâche peuvent être classés suivant les catégories suivantes :

* **Échecs de prétraitement**

    Si une tâche ne parvient pas à démarrer, une erreur de prétraitement est définie pour la tâche.  

    Des erreurs de prétraitement peuvent se produire si des fichiers de ressources de la tâche ont été déplacés, si le compte Stockage n’est plus disponible ou si un autre problème ayant empêché la copie des fichiers sur le nœud est survenu.

* **Échecs de chargement de fichier**

    Si le chargement des fichiers qui sont spécifiés pour une tâche échoue pour une raison quelconque, une erreur de chargement est définie pour la tâche.

    Des erreurs de chargement de fichier peuvent se produire si la SAP permettant d’accéder au Stockage Azure n’est pas valide ou n’accorde pas d’autorisations d’écriture, si le compte de stockage n’est plus disponible ou si un autre problème ayant empêché la copie des fichiers sur le nœud est survenu.    

* **Échecs d’application**

    Le processus spécifié par la ligne de commande de la tâche peut également échouer. Il est considéré comme ayant échoué lorsqu’un code de sortie différent de zéro est renvoyé par le processus exécuté par la tâche (voir *Codes de sortie de tâche* dans la section ci-après).

    Pour les échecs d’application, vous pouvez configurer Batch pour relancer automatiquement la tâche autant de fois que vous l’aurez spécifié.

* **Échecs de contrainte**

    Vous pouvez définir une contrainte qui spécifie la durée maximale d’exécution d’un travail ou d’une tâche, le *maxWallClockTime*. Cette opération peut se révéler utile pour terminer les tâches dont la progression échoue.

    Lorsque la durée maximale est dépassée, la tâche est marquée comme *terminée*, mais le code de sortie est défini sur `0xC000013A` et le champ *schedulingError* est marqué comme `{ category:"ServerError", code="TaskEnded"}`.

### <a name="debugging-application-failures"></a>Débogage des échecs d’application
* `stderr` et `stdout`

    Pendant l’exécution, une application peut produire des diagnostics qui vous permettent de résoudre les problèmes. Comme mentionné dans la section plus haut [Fichiers et répertoires](#files-and-directories), le service Batch écrit des sorties et des sorties d’erreur standard dans des fichiers `stdout.txt` et `stderr.txt` du répertoire de tâche sur le nœud de calcul. Vous pouvez utiliser le portail Azure ou l’un des Kits de développement logiciel (SDK) Batch pour télécharger ces fichiers. Par exemple, vous pouvez récupérer ces fichiers et d’autres à des fins de résolution des problèmes en utilisant [ComputeNode.GetNodeFile][net_getfile_node] et [CloudTask.GetNodeFile][net_getfile_task] dans la bibliothèque .NET Batch.

* **Codes de sortie de tâche**

    Comme mentionné précédemment, une tâche est marquée comme ayant échoué par le service Batch si le processus exécuté par la tâche retourne un code de sortie différent de zéro. Lorsqu’une tâche exécute un processus, Batch remplit la propriété de code de sortie de la tâche avec le *code de retour du processus*. Il est important de noter que le code de sortie d’une tâche **n’est pas** déterminé par le service Batch, mais par le processus proprement dit ou par le système d’exploitation sur lequel le processus est exécuté.

### <a name="accounting-for-task-failures-or-interruptions"></a>Prise en compte des échecs ou des interruptions de tâche
Les tâches peuvent parfois échouer ou être interrompues. L’application de la tâche elle-même peut échouer, le nœud sur lequel elle s’exécute peut être redémarré, voire supprimé du pool pendant le redimensionnement de ce dernier si la stratégie de désallocation du pool définie prévoit la suppression immédiate des nœuds, sans attendre la fin des tâches. Dans tous les cas, la tâche peut être automatiquement remise en file d’attente par Batch pour être exécutée sur un autre nœud.

Un problème intermittent peut également provoquer la suspension d’une tâche ou ralentir son exécution. Vous pouvez définir l’intervalle d’exécution maximal d’une tâche. Si l’intervalle d’exécution maximal est dépassé, le service Batch interrompt l’application de la tâche.

### <a name="connecting-to-compute-nodes"></a>Se connecter aux nœuds de calcul
Vous pouvez effectuer des actions supplémentaires de débogage et de résolution des problèmes en vous connectant à un nœud de calcul à distance. Vous pouvez utiliser le portail Azure pour télécharger un fichier RDP pour les nœuds Windows et obtenir des informations de connexion SSH pour les nœuds Linux. Vous pouvez également effectuer cette opération à l’aide des API Batch, par exemple [.NET Batch][net_rdpfile] ou [Python Batch](batch-linux-nodes.md#connect-to-linux-nodes-using-ssh).

> [!IMPORTANT]
> Pour vous connecter à un nœud via RDP ou SSH, vous devez d’abord créer un utilisateur sur le nœud. Pour ce faire, vous pouvez utiliser le Portail Azure, [ajouter un compte d’utilisateur à un nœud][rest_create_user] en utilisant l’API REST Batch, appeler la méthode [ComputeNode.CreateComputeNodeUser][net_create_user] dans .NET Batch ou appeler la méthode [add_user][py_add_user] dans le module Python de Batch.
>
>

### <a name="troubleshooting-problematic-compute-nodes"></a>Résolution des problèmes liés aux nœuds de calcul
Quand certaines de vos tâches échouent, votre application cliente Batch ou un service peut examiner les métadonnées des tâches en échec pour identifier un nœud présentant un dysfonctionnement. Chaque nœud d’un pool se voit attribuer un ID unique et le nœud sur lequel s’exécute une tâche est inclus dans les métadonnées de la tâche. Une fois que vous avez identifié le nœud présentant un problème, vous pouvez effectuer les actions suivantes :

* **Redémarrer le nœud** ([REST][rest_reboot] | [.NET][net_reboot])

    Le fait de redémarrer le nœud peut parfois résoudre des problèmes latents comme des processus bloqués ou défaillants. Notez que si votre pool utilise une tâche de démarrage ou si votre travail utilise une tâche de préparation, ces deux éléments s’exécutent au redémarrage du nœud.
* **Réinitialiser le nœud** ([REST][rest_reimage] | [.NET][net_reimage])

    Cette opération réinstalle le système d’exploitation sur le nœud. Comme avec le redémarrage d’un nœud, les tâches de démarrage et celles de préparation d’un travail sont relancées une fois le nœud réinitialisé.
* **Supprimer le nœud du pool** ([REST][rest_remove] | [.NET][net_remove])

    Il est parfois nécessaire de supprimer entièrement le nœud à partir du pool.
* **Désactiver la planification des tâches sur le nœud** ([REST][rest_offline] | [.NET][net_offline])

    Cette opération met le nœud hors connexion, de sorte qu’aucune tâche supplémentaire ne peut lui être affectée. Toutefois, le nœud est autorisé à poursuivre son exécution et à rester dans le pool. Cela vous permet de faire une recherche approfondie sur la cause des échecs sans perdre les données de la tâche en échec et sans que le nœud n’occasionne d’autres échecs de tâche supplémentaires. Par exemple, vous pouvez désactiver la planification des tâches sur le nœud, puis vous [connecter à distance](#connecting-to-compute-nodes) pour examiner les journaux des événements de ce nœud ou encore résoudre d’autres problèmes. Après avoir terminé votre recherche, vous pouvez remettre le nœud en ligne en activant la planification des tâches ([REST][rest_online] | [.NET][net_online]), ou exécuter l’une des autres actions indiquées précédemment.

> [!IMPORTANT]
> Pour chaque action décrite dans cette section (redémarrer, réinitialiser, supprimer, et désactiver la planification des tâches), vous pouvez indiquer la manière dont les tâches en cours d’exécution sur le nœud sont gérées lorsque vous effectuez l’action. Par exemple, lorsque vous désactivez la planification des tâches sur un nœud à l’aide de la bibliothèque client .NET Batch, vous pouvez spécifier une valeur d’énumération [DisableComputeNodeSchedulingOption][net_offline_option] pour préciser s’il faut **terminer** les tâches en cours d’exécution, les **remettre en file d’attente** pour les planifier sur d’autres nœuds ou finaliser les tâches en cours avant d’exécuter l’action (**TaskCompletion**).
>
>

## <a name="next-steps"></a>Étapes suivantes
* Découvrez les [outils et API Batch](batch-apis-tools.md) disponibles pour créer des solutions Batch.
* Passez en revue un exemple d’application Batch détaillée dans [Prise en main de la bibliothèque Azure Batch pour .NET](batch-dotnet-get-started.md). Il existe également une [version Python](batch-python-tutorial.md) du didacticiel qui exécute une charge de travail sur des nœuds de calcul Linux.
* Téléchargez et créez l’exemple de projet [Batch Explorer][github_batchexplorer] à utiliser lors du développement de vos solutions Batch. En utilisant l’explorateur Batch, vous pouvez effectuer ce qui suit, et bien plus encore :

  * Analysez et manipulez les pools, les travaux et les tâches au sein de votre compte Batch
  * Téléchargez `stdout.txt`, `stderr.txt` et d’autres fichiers à partir des nœuds
  * Créez des utilisateurs sur les nœuds et téléchargez les fichiers RDP pour la connexion à distance
* Découvrez comment [créer des pools de nœuds de calcul Linux](batch-linux-nodes.md).
* Consultez le [forum Azure Batch][batch_forum] sur MSDN. Le forum est parfait pour poser des questions, que vous soyez débutant ou expert dans l’utilisation du service Batch.

[1]: ./media/batch-api-basics/node-folder-structure.png

[azure_storage]: https://azure.microsoft.com/services/storage/
[batch_forum]: https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurebatch
[cloud_service_sizes]: ../cloud-services/cloud-services-sizes-specs.md
[msmpi]: https://msdn.microsoft.com/library/bb524831.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_sample_taskdeps]:  https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/TaskDependencies
[github_batchexplorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch_net_api]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[msdn_env_vars]: https://msdn.microsoft.com/library/azure/mt743623.aspx
[net_cloudjob_jobmanagertask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobmanagertask.aspx
[net_cloudjob_priority]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.priority.aspx
[net_cloudpool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_cloudtask_env]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.environmentsettings.aspx
[net_create_cert]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificateoperations.createcertificate.aspx
[net_create_user]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.createcomputenodeuser.aspx
[net_getfile_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.getnodefile.aspx
[net_getfile_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.getnodefile.aspx
[net_job_env]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.commonenvironmentsettings.aspx
[net_multiinstancesettings]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.aspx
[net_onalltaskscomplete]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.onalltaskscomplete.aspx
[net_rdp]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.getrdpfile.aspx
[net_reboot]: https://msdn.microsoft.com/library/azure/mt631495.aspx
[net_reimage]: https://msdn.microsoft.com/library/azure/mt631496.aspx
[net_remove]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.removefrompoolasync.aspx
[net_offline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.disableschedulingasync.aspx
[net_online]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.enableschedulingasync.aspx
[net_offline_option]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.disablecomputenodeschedulingoption.aspx
[net_rdpfile]: https://msdn.microsoft.com/library/azure/Mt272127.aspx
[vnet]: https://msdn.microsoft.com/library/azure/dn820174.aspx#bk_netconf

[py_add_user]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.ComputeNodeOperations.add_user

[batch_rest_api]: https://msdn.microsoft.com/library/azure/Dn820158.aspx
[rest_add_job]: https://msdn.microsoft.com/library/azure/mt282178.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[rest_add_cert]: https://msdn.microsoft.com/library/azure/dn820169.aspx
[rest_add_task]: https://msdn.microsoft.com/library/azure/dn820105.aspx
[rest_create_user]: https://msdn.microsoft.com/library/azure/dn820137.aspx
[rest_get_task_info]: https://msdn.microsoft.com/library/azure/dn820133.aspx
[rest_job_schedules]: https://msdn.microsoft.com/library/azure/mt282179.aspx
[rest_multiinstance]: https://msdn.microsoft.com/library/azure/mt637905.aspx
[rest_multiinstancesettings]: https://msdn.microsoft.com/library/azure/dn820105.aspx#multiInstanceSettings
[rest_update_job]: https://msdn.microsoft.com/library/azure/dn820162.aspx
[rest_rdp]: https://msdn.microsoft.com/library/azure/dn820120.aspx
[rest_reboot]: https://msdn.microsoft.com/library/azure/dn820171.aspx
[rest_reimage]: https://msdn.microsoft.com/library/azure/dn820157.aspx
[rest_remove]: https://msdn.microsoft.com/library/azure/dn820194.aspx
[rest_offline]: https://msdn.microsoft.com/library/azure/mt637904.aspx
[rest_online]: https://msdn.microsoft.com/library/azure/mt637907.aspx

[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/
