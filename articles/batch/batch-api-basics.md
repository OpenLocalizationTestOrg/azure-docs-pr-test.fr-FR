---
title: "aaaOverview de traitement par lots Azure pour les développeurs | Documents Microsoft"
description: "Découvrez les fonctionnalités de hello du service de traitement par lots hello et ses API à partir d’un point de vue du développement."
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
ms.openlocfilehash: 3da9d82572b28d05d1923166bd08c26725ca3316
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-large-scale-parallel-compute-solutions-with-batch"></a>Développer des solutions de calcul parallèles à grande échelle avec Batch

Dans cette vue d’ensemble des composants hello Hello service Azure Batch, nous présentent les fonctionnalités de service principal hello et que les développeurs de lot peuvent utiliser toobuild des parallèles à grande échelle des ressources de calcul des solutions.

Si vous développez une application distribuée de calcul ou de service qui émet direct [API REST] [ batch_rest_api] appels ou si vous utilisez l’un de hello [kits de développement logiciel lot](batch-apis-tools.md#azure-accounts-for-batch-development), vous allez utiliser la plupart des ressources de hello et les fonctionnalités abordées dans cet article.

> [!TIP]
> Pour une présentation plus haut niveau toohello service Batch, consultez [principes de base d’Azure Batch](batch-technical-overview.md).
>
>

## <a name="batch-service-workflow"></a>Flux de travail du service Batch
Bonjour les flux de travail de niveau supérieur suivant sont typique de presque toutes les applications et services qui utilisent le service de traitement par lots hello pour le traitement des charges de travail parallèles :

1. Télécharger hello **des fichiers de données** que vous souhaitez tooprocess tooan [Azure Storage] [ azure_storage] compte. Traitement par lots inclut la prise en charge intégrée pour accéder au stockage d’objets Blob Azure et vos tâches peuvent télécharger ces fichiers trop[nœuds de calcul](#compute-node) lors de l’exécution des tâches hello.
2. Télécharger hello **fichiers d’application** fonctionnant à vos tâches. Ces fichiers peuvent être des fichiers binaires ou de scripts et de leurs dépendances et sont exécutées par des tâches hello dans vos tâches. Les tâches peuvent télécharger ces fichiers à partir de votre compte de stockage, ou vous pouvez utiliser hello [les packages d’applications](#application-packages) la fonctionnalité de traitement par lots pour le déploiement et la gestion des applications.
3. Créez un [pool](#pool) de nœuds de calcul. Lorsque vous créez un pool, vous spécifiez le nombre de hello de nœuds de calcul pour le pool de hello, leur taille et le système d’exploitation de hello. Lors de chaque tâche dans votre tâche s’exécute, elle est assignée tooexecute sur l’un des nœuds hello dans le pool.
4. Créez un [travail](#job). Un travail gère une collection de tâches. Vous associez chaque pool travail tooa spécifique où les tâches de ce travail seront exécutera.
5. Ajouter [tâches](#task) toohello travail. Chaque tâche exécute l’application hello ou un script que vous avez téléchargé les fichiers de données hello tooprocess qu'il télécharge à partir de votre compte de stockage. Comme chaque tâche se termine, il peut télécharger ses tooAzure sortie stockage.
6. Surveiller la progression du travail et récupérer le résultat de la tâche hello depuis le stockage Azure.

Bonjour les sections suivantes décrivent ces et hello d’autres ressources de traitement par lots qui permettent de votre scénario.

> [!NOTE]
> Vous avez besoin une [compte Batch](#account) toouse hello service Batch. La plupart des solutions Batch utilisent aussi un compte [Stockage Azure][azure_storage], afin de stocker et récupérer un fichier. Traitement par lots prend actuellement en charge uniquement hello **à usage général** type de compte de stockage, comme décrit à l’étape 5 de [créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account) dans [comptes de stockage sur Azure](../storage/common/storage-create-storage-account.md).
>
>

## <a name="batch-service-resources"></a>Ressources du service Batch
Hello suivant des ressources--comptes, certains nœuds, les pools, les travaux et les tâches--sont requis par toutes les solutions qui utilisent le service de traitement par lots hello de calcul. D’autres, telles que les planifications de travaux et les packages d’applications, sont utiles, mais facultatives.

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
Un compte de traitement par lots est une entité identifiée de façon unique au sein de hello service Batch. Tout le traitement s’effectue via un compte Batch.

Vous pouvez créer un compte Azure Batch hello [portail Azure](batch-account-create-portal.md) ou par programme, comme avec hello [bibliothèque de Batch Management .NET](batch-management-dotnet.md). Lorsque vous créez un compte de hello, vous pouvez associer un compte de stockage Azure.

### <a name="pool-allocation-mode"></a>Mode d’allocation de pool

Lorsque vous créez un compte Batch, vous pouvez spécifier la manière dont les [pools](#pool) de nœuds de calcul sont alloués. Vous pouvez choisir les pools de tooallocate de nœuds de calcul dans un abonnement géré par le traitement par lots Azure, ou vous pouvez les allouer dans votre propre abonnement. Hello *mode d’allocation de pool* propriété pour le compte de hello détermine où les pools sont alloués. 

Tenez compte des toodecide qui toouse du mode de répartition, du pool qui répond le mieux à votre scénario :

* **Service de traitement par lots**: Service de traitement par lots est le mode d’allocation de pool par défaut hello, dans lequel les pools sont alloués coulisses de hello dans les abonnements de géré par Azure. Gardez à l’esprit ces points clés sur le mode d’allocation de pool hello Service Batch :

    - mode d’allocation de pool Hello Service Batch prend en charge les pools de Service Cloud et de Machine virtuelle.
    - Hello mode d’allocation de pool Service Batch prend en charge les deux authentification shared key ou [l’authentification Azure Active Directory](batch-aad-auth.md) (Azure AD). 
    - Vous pouvez utiliser soit nœuds de calcul dédié ou à faible priorité dans les pools alloués avec mode d’allocation de pool hello Service Batch.
    - N’utilisez pas le mode d’allocation de pool Service Batch hello si vous envisagez de pools de machine virtuelle Azure toocreate à partir d’images de machine virtuelle personnalisées, ou si vous envisagez de toouse un réseau virtuel. Créer votre compte avec le mode d’allocation de pool hello abonnement de l’utilisateur à la place.
    - Pools d’ordinateur virtuel configurés dans un compte créé avec le mode d’allocation de pool hello Service Batch doivent être créés à partir de [Azure Marketplace de Machines virtuelles] [ vm_marketplace] images.

* **Abonnement de l’utilisateur**: avec mode d’allocation de pool hello abonnement de l’utilisateur, les pools de lot sont alloués à hello abonnement Azure où le compte de hello est créé. Gardez à l’esprit ces points clés sur le mode d’allocation de pool hello abonnement de l’utilisateur :
     
    - mode d’allocation de pool Hello abonnement utilisateur prend en charge uniquement les pools de Machine virtuelle. elle ne gère pas les pools de services cloud.
    - pools de Machine virtuelle toocreate de personnalisés des images de machine virtuelle ou toouse un réseau virtuel avec les pools d’ordinateur virtuel, vous devez utiliser le mode d’allocation de pool hello abonnement de l’utilisateur.  
    - Vous devez utiliser [l’authentification Azure Active Directory](batch-aad-auth.md) avec les pools sont alloués à l’abonnement d’utilisateur hello. 
    - Vous devez configurer un coffre de clés Azure pour votre compte de traitement par lots si le mode d’allocation de pool hello a la valeur tooUser abonnement. 
    - Vous pouvez utiliser des nœuds de calcul dédié uniquement dans les pools d’un compte créé avec le mode d’allocation de pool hello abonnement de l’utilisateur. Les nœuds à faible priorité ne sont pas pris en charge.
    - Pools d’ordinateur virtuel configurés dans un compte avec le mode d’allocation de pool hello abonnement utilisateur peuvent être créés à partir de [Azure Marketplace de Machines virtuelles] [ vm_marketplace] images, ou de personnaliser les images que vous avez fournir.

Hello tableau suivant compare les modes de répartition pool Service Batch et d’abonnement de l’utilisateur des hello.

| **Mode d’allocation de pool**                 | **Service Batch**                                                                                       | **Abonnement utilisateur**                                                              |
|-------------------------------------------|---------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------|
| **Les pools sont alloués dans**               | Un abonnement Azure géré                                                                           | abonnement d’utilisateur Hello dans le lot hello compte est créé.                        |
| **Configurations prises en charge**             | <ul><li>Configuration service cloud</li><li>Configuration de machines virtuelles (Linux et Windows)</li></ul> | <ul><li>Configuration de machines virtuelles (Linux et Windows)</li></ul>                |
| **Images de machine virtuelle prises en charge**                  | <ul><li>Images de la Place de marché Azure</li></ul>                                                              | <ul><li>Images de la Place de marché Azure</li><li>Images personnalisées</li></ul>                   |
| **Types de nœuds de calcul pris en charge**         | <ul><li>Nœuds dédiés</li><li>Nœuds de faible priorité</li></ul>                                            | <ul><li>Nœuds dédiés</li></ul>                                                  |
| **Authentification prise en charge**             | <ul><li>Clé partagée</li><li>Azure AD</li></ul>                                                           | <ul><li>Azure AD</li></ul>                                                         |
| **Azure Key Vault requis**             | Non                                                                                                      | Oui                                                                                |
| **Quota de cœurs**                           | Déterminé par le quota de cœurs Batch                                                                          | Déterminé par le quota de cœurs Batch                                              |
| **Support réseau virtuel Azure (Vnet)** | Pools créés avec hello Configuration de Service Cloud                                                      | Pools créés avec hello Configuration d’ordinateur virtuel                               |
| **Modèle de déploiement de réseau virtuel pris en charge**      | Vnets créés avec un modèle de déploiement classique                                                             | Réseaux virtuels créés avec le modèle de déploiement classique hello ou d’Azure Resource Manager |

## <a name="azure-storage-account"></a>Compte de Stockage Azure

La plupart des solutions Batch utilisent Stockage Azure pour stocker les fichiers de ressources et les fichiers de sortie.  

Traitement par lots prend en charge actuellement seul type de compte de stockage à usage général hello, comme décrit à l’étape 5 de [créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account) dans [comptes de stockage sur Azure](../storage/common/storage-create-storage-account.md). Vos tâches Batch (y compris les tâches standard, de démarrage, de préparation des travaux et de validation des travaux) doivent spécifier des fichiers de ressources se trouvant dans les comptes de stockage à usage général.


## <a name="compute-node"></a>Nœud de calcul
Un nœud de calcul est une machine virtuelle Azure (VM) ou un service de cloud machine virtuelle qui est dédié tooprocessing une partie de la charge de travail de votre application. taille Hello d’un nœud détermine le nombre hello de cœurs du processeur, la capacité de mémoire et taille de système de fichiers local allouée toohello nœud. Vous pouvez créer des pools de nœuds Windows ou Linux à l’aide d’Azure Cloud Services, les images à partir de hello [Azure Marketplace de Machines virtuelles][vm_marketplace], ou des images personnalisées que vous avez préparé. Voir hello [Pool](#pool) section pour plus d’informations sur ces options.

Nœuds peuvent exécuter un fichier exécutable ou un script qui est pris en charge par l’environnement de système d’exploitation hello du nœud de hello. Cela inclut les scripts \*.exe, \*.cmd, \*.bat et PowerShell pour Windows, les fichiers binaires, ainsi que les scripts shell et Python pour Linux.

Tous les nœuds de calcul Batch incluent également les éléments suivants :

* Une [structure de dossiers](#files-and-directories) standard et des [variables d’environnement](#environment-settings-for-tasks) associées pouvant être référencées par les tâches.
* **Pare-feu** paramètres qui sont configurés toocontrol accès.
* [Accès à distance](#connecting-to-compute-nodes) tooboth Windows (protocole RDP (Remote Desktop)) et des nœuds Linux (Secure Shell (SSH)).

## <a name="pool"></a>pool
Un pool est une collection de nœuds sur lesquels votre application s’exécute. pool de Hello peut être créé manuellement par vous, ou automatiquement par le service Batch de hello lorsque vous spécifiez hello toobe de travail terminé. Vous pouvez créer et gérer un pool qui répond aux besoins en ressources de votre application hello. Un pool peut être utilisé uniquement par le compte de traitement par lots hello dans lequel il a été créé. Un compte Batch peut avoir plusieurs pools.

Les pools de traitement par lots Azure de build sur la plateforme de calcul Azure hello principale. Ils fournissent à grande échelle d’allocation, installation de l’application, la distribution des données, contrôle d’intégrité et flexible ajustement du nombre de hello de nœuds de calcul dans un pool ([mise à l’échelle](#scaling-compute-resources)).

Chaque nœud est ajouté tooa pool est attribué un nom unique et une adresse IP. Lorsqu’un nœud est supprimé d’un pool, les modifications apportées au système d’exploitation de toohello ou les fichiers sont perdues, et son nom et l’adresse IP sont libérées à un usage ultérieur. Lorsqu’un nœud quitte un pool, sa durée de vie est terminée.

Lorsque vous créez un pool, vous pouvez spécifier hello suivant des attributs. Certains paramètres sont différents, selon le mode d’allocation de pool hello Hello lot [compte](#account):

- Système d’exploitation et version de nœud de calcul
- Type de nœud de calcul et nombre cible de nœuds
- Taille des nœuds de calcul hello
- Stratégie de mise à l’échelle
- Stratégie de planification des tâches
- État de communication des nœuds de calcul
- Tâches de démarrage des nœuds de calcul
- packages d’application
- Configuration réseau

Chacun de ces paramètres est décrite plus en détail dans les sections suivantes de hello.

> [!IMPORTANT]
> Comptes de lots créés avec le mode d’allocation de pool Service Batch hello ont un quota par défaut qui limite le nombre de hello de cœurs dans un compte de traitement par lots. nombre de Hello de cœurs correspond nombre toohello de nœuds de calcul. Vous trouverez les quotas par défaut hello et obtenir des instructions sur la façon de trop[un quota de](batch-quota-limit.md#increase-a-quota) dans [Quotas et limites pour hello service Azure Batch](batch-quota-limit.md). Si votre pool n’a pas obtenu son nombre cible de nœuds, quota de cœurs hello peut-être la raison de hello.
>
>Comptes de lots créés avec le mode d’allocation de pool hello abonnement de l’utilisateur ne respectent pas les quotas de service de traitement par lots hello. Au lieu de cela, ils partagent Bonjour quota principal pour hello spécifié d’abonnement. Pour en savoir plus, consultez le paragraphe [Limites de machines virtuelles](../azure-subscription-service-limits.md#virtual-machines-limits) de la section [Abonnement Azure et limites, quotas et contraintes de service](../azure-subscription-service-limits.md).
>
>

### <a name="compute-node-operating-system-and-version"></a>Système d’exploitation et version de nœud de calcul

Lorsque vous créez un pool de traitement par lots, vous pouvez spécifier la configuration de machine virtuelle Azure hello et de type hello de souhaité toorun sur chaque nœud de calcul dans le pool de hello de système d’exploitation. Hello deux types de configurations disponibles dans le lot sont :

- Hello **Configuration d’ordinateur virtuel**, qui spécifie ce pool hello est composée de machines virtuelles. Ces machines virtuelles peuvent être créées à partir d’images Linux ou Windows. 

    Lorsque vous créez un pool en fonction de hello Configuration d’ordinateur virtuel, vous devez spécifier non seulement hello de nœuds de hello et hello de hello images utilisées toocreate les, mais également hello **référence d’image de machine virtuelle** et hello Lot **agent du nœud référence (SKU)** toobe installé sur les nœuds hello. Pour plus d’informations sur la spécification des propriétés de pool, voir [Configurer des nœuds de calcul Linux dans des pools Azure Batch](batch-linux-nodes.md).

- Hello **Configuration des Services Cloud**, qui spécifie ce pool hello est composé de nœuds de Services de cloud computing Azure. Ce dernier fournit *uniquement* des nœuds de calcul Windows.

    Les systèmes d’exploitation disponibles pour les pools de Configuration des Services Cloud sont répertoriés dans hello [versions de système d’exploitation invité de Azure et matrice de compatibilité SDK](../cloud-services/cloud-services-guestos-update-matrix.md). Lorsque vous créez un pool qui contient les nœuds des Services de cloud computing, vous avez besoin de taille du nœud toospecify hello et son *famille de système d’exploitation*. Services de cloud computing sont déployé tooAzure plus rapidement que les machines virtuelles exécutant Windows. Si vous souhaitez créer des nœuds de calcul Windows, vous pouvez constater que Cloud Services propose un délai de déploiement moins important.

    * Hello *famille de système d’exploitation* détermine également les versions de .NET sont installées avec hello du système d’exploitation.
    * Comme avec les rôles de travail dans les Services de cloud computing, vous pouvez spécifier une *Version du système d’exploitation* (pour plus d’informations sur les rôles de travail, consultez hello [en savoir plus sur les services de cloud computing](../cloud-services/cloud-services-choose-me.md#tell-me-about-cloud-services) section Bonjour [Services de cloud computing vue d’ensemble](../cloud-services/cloud-services-choose-me.md)).
    * Comme avec les rôles de travail, nous vous recommandons de spécifier `*` pour hello *Version du système d’exploitation* afin que les nœuds hello sont mis à niveau automatiquement, et il n’existe aucun toocater travail requis toonewly publié versions. Hello est principalement utilisé pour la sélection d’une version du système d’exploitation spécifique tooensure compatibilité des applications, ce qui permet la compatibilité descendante toobe test effectué avant d’autoriser hello version toobe est mis à jour. Après la validation, hello *Version du système d’exploitation* pour le pool de hello peut être mis à jour et la nouvelle image de système d’exploitation hello peut être installé--toutes les tâches en cours d’exécution sont interrompus et remis.

Lorsque vous créez un pool, vous devez tooselect hello approprié **nodeAgentSkuId**, en fonction de hello du système d’exploitation de l’image de base hello de votre disque dur virtuel. Vous pouvez obtenir un mappage de nœud disponible agent ID de référence (SKU) tootheir les références d’Image de système d’exploitation en appelant hello [références de l’Agent de nœud pris en charge liste](https://docs.microsoft.com/rest/api/batchservice/list-supported-node-agent-skus) opération.

Consultez hello [compte](#account) section pour plus d’informations sur la configuration de mode d’allocation de pool hello lorsque vous créez un compte Batch.

#### <a name="custom-images-for-virtual-machine-pools"></a>Images personnalisées pour les pools de machines virtuelles

toouse un pools de Machine virtuelle tooprovision image personnalisée, créer votre compte Batch avec mode d’allocation de pool hello abonnement de l’utilisateur. Avec ce mode, les pools de lot sont allouées en abonnement hello dans laquelle réside hello compte. Consultez hello [compte](#account) section pour plus d’informations sur la configuration de mode d’allocation de pool hello lorsque vous créez un compte Batch.

toouse une image personnalisée, vous devez image de hello tooprepare en la généralisant. Pour plus d’informations sur la préparation d’images Linux personnalisées à partir de machines virtuelles Azure, consultez [capturer un toouse de machine virtuelle de Azure Linux en tant que modèle](../virtual-machines/linux/capture-image-nodejs.md). Pour plus d’informations sur la préparation d’images Windows personnalisées à partir de machines virtuelles Azure, consultez la section [Créer une image personnalisée d’une machine virtuelle Azure à l’aide de PowerShell](../virtual-machines/windows/tutorial-custom-images.md). 

> [!IMPORTANT]
> Lorsque vous préparez votre image personnalisée, gardez suivante de hello l’esprit :
> - Vérifiez cette image de système d’exploitation à base de hello, vous utilisez tooprovision vos pools de lot est n’a pas un préalable installé des extensions Azure, comme extension de Script personnalisé hello. Si l’image de hello contient une extension préinstallée, Azure peut rencontrer des problèmes de la déployer hello machine virtuelle.
> - Assurez-vous que cette image du système d’exploitation de base de hello que vous fournir utilise hello lecteur temp de la valeur par défaut, comme hello agent de nœud de lot actuellement attend lecteur temp de hello par défaut.
>
>

toocreate un pool de Configuration d’ordinateur virtuel à l’aide d’une image personnalisée, vous aurez besoin d’un ou de vos images de disque dur virtuel personnalisés toostore des comptes de stockage de Azure plus standard. Les images personnalisées sont stockées en tant que blobs. tooreference vos images lorsque vous créez un pool, spécifiez hello URI d’objets BLOB de disque dur virtuel d’image personnalisée hello pour hello [osDisk](https://docs.microsoft.com/rest/api/batchservice/add-a-pool-to-an-account#bk_osdisk) propriété Hello [virtualMachineConfiguration](https://docs.microsoft.com/rest/api/batchservice/add-a-pool-to-an-account#bk_vmconf) propriété.

Assurez-vous que vos comptes de stockage répondent à hello suivant des critères :   

- les comptes de stockage Hello BLOB de disque dur virtuel contenant hello image personnalisée doivent toobe dans hello même abonnement que hello du compte Batch (abonnement d’utilisateur hello).
- Hello spécifié de comptes de stockage doivent toobe Bonjour même région que hello compte Batch.
- Actuellement, seuls les comptes de stockage standards sont pris en charge. Stockage Azure Premium prendra en charge Bonjour futures.
- Vous pouvez spécifier un compte de stockage avec plusieurs blobs VHD personnalisés, ou plusieurs comptes de stockage incluant un seul blob. Nous vous recommandons toouse stockage plusieurs comptes tooget de meilleures performances.
- Un objet blob de disque dur virtuel image personnalisée unique peut prendre en charge les too40 que Linux VM instances ou 20 instances de machine virtuelle Windows. Vous devez les copies de toocreate des pools de toocreate de blob de disque dur virtuel hello avec davantage d’ordinateurs virtuels. Par exemple, un pool avec les machines virtuelles Windows 200 nécessite 10 objets BLOB VHD unique spécifié pour hello **osDisk** propriété.

toocreate un regroupement à partir d’une image personnalisée à l’aide de hello portail Azure :

1. Accédez à tooyour du compte Batch Bonjour portail Azure.
2. Sur hello **paramètres** panneau, sélectionnez hello **Pools** élément de menu.
3. Sur hello **Pools** panneau, sélectionnez hello **ajouter** commande ; hello **ajouter un pool** panneau s’affiche.
4. Sélectionnez **l’Image personnalisée (Linux/Windows)** de hello **le Type d’Image** liste déroulante. portail de Hello affiche hello **Image personnalisée** sélecteur. Choisissez un ou plusieurs disques durs virtuels hello même hello de conteneur et cliquez sur **sélectionnez** bouton. 
    Prise en charge de plusieurs disques durs virtuels à partir de différents comptes de stockage et de différents conteneurs sera ajoutée dans hello futures.
5. Sélectionnez hello correct **Publisher offre/référence (SKU)** pour vos disques durs virtuels personnalisés, sélectionnez hello souhaité **mise en cache** mode, puis renseignez tous hello autres paramètres pour le pool de hello.
6. toocheck si un pool est basé sur une image personnalisée, consultez hello **système d’exploitation** propriété dans la section Résumé de ressource hello Hello **Pool** panneau. Hello la valeur de cette propriété doit être **image d’ordinateur virtuel personnalisé**.
7. Tous les disques durs virtuels personnalisés associés à un pool sont affichés sur du pool hello **propriétés** panneau.

### <a name="compute-node-type-and-target-number-of-nodes"></a>Type de nœud de calcul et nombre cible de nœuds

Lorsque vous créez un pool, vous pouvez spécifier les types de nœuds de calcul et de hello nombre cible pour chacun. Hello deux des types de nœuds de calcul sont :

- **Nœuds de calcul dédiés.** Les nœuds de calcul dédiés sont réservés à vos charges de travail. Ils sont plus coûteuses que les nœuds de faible priorité, mais il est garanti toonever être interrompu.

- **Nœuds de calcul à faible priorité.** Nœuds de faible priorité tirer parti d’une capacité excédentaire dans Azure toorun vos charges de travail de traitement par lots. Le coût horaire des nœuds à faible priorité est moins élevé que celui des nœuds dédiés. Par ailleurs, ces nœuds activent des charges de travail nécessitant une importante puissance de calcul. Pour plus d’informations, consultez [Utiliser des machines virtuelles à faible priorité avec Batch](batch-low-pri-vms.md).

    Les nœuds de calcul à faible priorité peuvent être reportés lorsque Azure n’a pas suffisamment de capacité excédentaire. Si un nœud est interrompu lors de l’exécution des tâches, les tâches de hello sont remis et exécutez à nouveau une fois qu’un nœud de calcul est à nouveau disponible. Les nœuds de faible priorité sont une bonne option pour les charges de travail où heure d’achèvement de tâche de hello est flexible et charge de travail hello est répartie sur plusieurs nœuds. Avant de décider des nœuds de faible priorité toouse pour votre scénario, assurez-vous que tout travail perdu en raison toopreemption sera toorecreate minimal et simple.

    Nœuds de calcul de priorité faible sont disponibles uniquement pour les comptes de traitement par lots créés avec le mode d’allocation de pool hello défini trop**Service Batch**.

Vous pouvez avoir deux nœuds de calcul dédié et de priorité basse dans hello même pool. Chaque type de nœud &mdash; dédié et de faible priorité &mdash; a son propre paramètre de cible pour lequel vous pouvez spécifier le nombre souhaité de hello de nœuds. 
    
nombre de nœuds de calcul Hello est tooas auxquels un *cible* car dans certaines situations, votre pool ne peut pas atteindre nombre hello souhaité de nœuds. Par exemple, un pool risque de ne pas atteindre cible de hello pour s’il atteint hello [quota de cœurs](batch-quota-limit.md) compte tout d’abord de votre lot. Ou, dans le pool de hello ne peut pas atteindre cible de hello si vous avez appliqué une montée en puissance automatique pool toohello formule qui limite le nombre maximal de hello de nœuds.

Pour obtenir les informations de tarification des nœuds de calcul dédiés et à faible priorité, consultez [Tarification du service Batch](https://azure.microsoft.com/pricing/details/batch/).

### <a name="size-of-hello-compute-nodes"></a>Taille des nœuds de calcul hello

**Configuration de Cloud Services** sont répertoriées dans [Tailles de services cloud](../cloud-services/cloud-services-sizes-specs.md). Le service Batch prend en charge l’ensemble des tailles de services cloud, à l’exception de `ExtraSmall`, `STANDARD_A1_V2` et `STANDARD_A2_V2`.

Les tailles de nœud de calcul de la **configuration de machines virtuelles** sont répertoriées dans [Tailles des machines virtuelles dans Azure](../virtual-machines/linux/sizes.md) (Linux) et [Tailles des machines virtuelles dans Azure](../virtual-machines/windows/sizes.md) (Windows). Le service Batch prend en charge l’ensemble des tailles de machine virtuelle Azure, à l’exception de `STANDARD_A0` et de celles comprises dans Premium Storage (série `STANDARD_GS`, `STANDARD_DS`, et `STANDARD_DSV2`).

Lorsque vous sélectionnez une taille de nœud de calcul, considérez les caractéristiques de hello et exigences des applications hello que vous allez exécuter sur les nœuds hello. Aspects comme si l’application hello est multithread et de la quantité de mémoire qu’elle consomme peut aider à déterminent la taille de l’hello plus économique et plus approprié du nœud. Il est classique tooselect une taille de nœud en supposant qu’une seule tâche s’exécutera sur un nœud à la fois. Toutefois, il est possible de toohave plusieurs tâches (et par conséquent, plusieurs instances d’application) [s’exécuter en parallèle](batch-parallel-node-tasks.md) sur les nœuds de calcul lors de l’exécution du travail. Dans ce cas, il est commun toochoose une plus grande nœud taille tooaccommodate hello augmenté à la demande d’exécution des tâches parallèles. Pour plus d’informations, consultez la section [Stratégie de planification de tâches](#task-scheduling-policy).

Tous les nœuds hello dans un pool sont hello même taille. Si vous envisagez d’applications toorun ayant des spécifications différentes système et/ou des niveaux de charge, nous vous recommandons d’utiliser des pools séparés.

### <a name="scaling-policy"></a>Stratégie de mise à l’échelle

Pour les charges de travail dynamiques, vous pouvez écrire et appliquer un [formule de mise à l’échelle](#scaling-compute-resources) tooa pool. Hello service Batch évalue votre formule régulièrement et ajuste le nombre de hello de nœuds dans le pool de hello en fonction des différents pool de travail et les paramètres de tâche que vous pouvez spécifier.

### <a name="task-scheduling-policy"></a>Stratégie de planification des tâches

Hello [nombre maximum de tâches par nœud](batch-parallel-node-tasks.md) option de configuration détermine le nombre maximal de hello de tâches qui peuvent être exécutés en parallèle sur chaque nœud de calcul dans le pool de hello.

configuration par défaut de Hello Spécifie qu’une tâche à la fois s’exécute sur un nœud, mais il existe des scénarios où il est bénéfique toohave deux ou plusieurs tâches exécutées simultanément sur un nœud. Consultez hello [exemple de scénario](batch-parallel-node-tasks.md#example-scenario) Bonjour [les tâches simultanées nœud](batch-parallel-node-tasks.md) toosee article comment vous pouvez bénéficier de plusieurs tâches par nœud.

Vous pouvez également spécifier un *type de remplissage* qui détermine si lot répartit les tâches de hello uniformément entre tous les nœuds dans un pool ou packs de chaque nœud avec un nombre maximal de tâches hello avant de lui assigner nœud tooanother de tâches.

### <a name="communication-status-for-compute-nodes"></a>État de communication des nœuds de calcul

Dans la plupart des scénarios, les tâches fonctionnent indépendamment et n’avez pas besoin de toocommunicate avec l’autre. Cependant, il existe des applications dans lesquelles les tâches doivent communiquer, par exemple les [scénarios impliquant des applications MPI](batch-mpi.md).

Vous pouvez configurer un pool tooallow **communication entre les nœuds**, de sorte que les nœuds au sein d’un pool peuvent communiquer lors de l’exécution. Lorsque la communication entre les nœuds est activée, les nœuds des pools Configuration de Cloud Services peuvent communiquer entre eux sur les ports supérieurs à 1100, et les pools Configuration de la machine virtuelle ne limitent pas le trafic sur les ports.

Notez que l’activation de communication entre les nœuds également a un impact sur la sélection élective hello de nœuds hello au sein des clusters et peut limiter le nombre maximal de hello de nœuds dans un pool en raison des restrictions de déploiement. Si votre application ne requiert pas de communication entre les nœuds, hello service Batch peut allouer un nombre potentiellement important de nœuds toohello pool à partir de nombreux différents clusters et tooenable de centres de données a augmenté de puissance de traitement parallèle.

### <a name="start-tasks-for-compute-nodes"></a>Tâches de démarrage des nœuds de calcul

Hello facultatif *démarrer la tâche* s’exécute sur chaque nœud de ce nœud rejoint le pool de hello, chaque fois qu’un nœud est redémarré ou réinitialisé. tâche de démarrage Hello est particulièrement utile pour la préparation des nœuds de calcul pour une exécution de tâches, telles que l’installation d’applications de hello vos tâches s’exécutent sur les nœuds de calcul hello hello.

### <a name="application-packages"></a>packages d’application

Vous pouvez spécifier [les packages d’applications](#application-packages) toodeploy toohello nœuds de calcul dans le pool de hello. Les packages d’applications fournissent simplifié le déploiement et la gestion des versions des applications hello qui exécutent des tâches. Les packages d’applications que vous spécifiez pour un pool sont installés sur chaque nœud qui rejoint le pool, et à chaque fois qu’un nœud est redémarré ou réinitialisé.

> [!NOTE]
> Les packages d’applications sont pris en charge sur tous les pools Batch créés après le 5 juillet 2017. Elles sont prises en charge sur les pools de traitement par lots créés entre 10 mars 2016 et 5 juillet 2017 uniquement si le pool de hello a été créé à l’aide d’une configuration de Service Cloud. Les pools de lot créés too10 préalable mars 2016 ne gèrent pas les packages d’applications. Pour plus d’informations sur l’application à l’aide de packages toodeploy vos nœuds de traitement par lots tooyour applications, consultez [déployer des nœuds de toocompute d’applications avec des packages d’application de lot](batch-application-packages.md).
>
>

### <a name="network-configuration"></a>Configuration réseau

Vous pouvez spécifier le sous-réseau Azure hello [réseau virtuel (VNet)](../virtual-network/virtual-networks-overview.md) dans le calcul de quel pool hello nœuds doivent être créés. Consultez hello [configuration réseau du Pool](#pool-network-configuration) section pour plus d’informations.


## <a name="job"></a>Travail
Un travail est une collection de tâches. Il gère la façon dont le calcul est effectué par ses tâches sur des nœuds de calcul hello dans un pool.

* travail de Hello spécifie hello **pool** dans quels hello est toobe exécuter. Vous pouvez créer un nouveau pool pour chaque tâche, ou utiliser un pool pour plusieurs travaux. Vous pouvez créer un pool pour chaque travail associé à une planification de travail, ou pour tous les travaux associés à une planification de travail.
* Une **priorité de travail**facultative peut être spécifiée. Lorsqu’un travail est envoyé avec une priorité plus élevée que les travaux qui sont actuellement en cours d’exécution, tâches hello pour le travail de priorité plus élevée hello sont insérées dans la file d’attente hello avant les tâches pour les travaux de faible priorité hello. Les tâches des travaux de priorité inférieure qui sont déjà en cours d’exécution ne sont pas reportées.
* Vous pouvez utiliser la tâche **contraintes** toospecify certaines limites pour vos travaux :

    Vous pouvez définir un **wallclock maximale temps**, de sorte que si une tâche s’exécute pendant plus de temps maximale wallclock hello qui est spécifié, le travail de hello et toutes ses tâches sont terminées.

    Le service Batch peut détecter, puis relancer des tâches ayant échoué. Vous pouvez spécifier hello **nombre maximal de tentatives de tâche** en tant que contrainte, y compris si une tâche est *toujours* ou *jamais* retentée. Reprise d’une tâche signifie que cette tâche hello est remis toobe, exécutez à nouveau.
* Votre application cliente peut ajouter le travail de tooa de tâches, ou vous pouvez spécifier un [tâche du gestionnaire](#job-manager-task). Une tâche du Gestionnaire contient des informations hello toocreate nécessaire des tâches de hello requis pour un travail, avec hello tâche du gestionnaire en cours d’exécution sur l’un des hello nœuds de calcul dans le pool de hello. Hello tâche du gestionnaire est gérée par lot--il est en file d’attente dès que la tâche de hello est créé et est redémarré en cas d’échec. Une tâche du gestionnaire est *requis* pour les travaux qui est créés par un [planification du travail](#scheduled-jobs) , car il est hello uniquement moyen toodefine hello les tâches avant l’instanciation de travail de hello.
* Par défaut, les travaux restent dans un état actif de hello lorsque toutes les tâches au sein de la tâche de hello sont terminées. Vous pouvez modifier ce comportement afin que hello travail est automatiquement arrêté une fois toutes les tâches hello travail terminées. La tâche de jeu hello **onAllTasksComplete** propriété ([OnAllTasksComplete] [ net_onalltaskscomplete] dans .NET de lot) trop*terminatejob* tooautomatically arrêter le travail de hello lorsque toutes les tâches sont en état de hello s’est terminée.

    Notez que le service de traitement par lots hello tient compte un travail avec *aucun* toohave tâches toutes ses tâches terminées. C’est la raison pour laquelle cette option est généralement utilisée avec une [tâche de gestionnaire de travaux](#job-manager-task). Si vous souhaitez arrêt automatique d’un travail de toouse sans un gestionnaire de travaux, vous devez définir initialement d’un nouveau travail **onAllTasksComplete** propriété trop*noaction*, puis définissez-la trop*terminatejob* uniquement une fois que vous avez terminé d’ajouter des travaux toohello de tâches.

### <a name="job-priority"></a>priorité de travail
Vous pouvez affecter un toojobs de priorité que vous créez dans le lot. Hello service Batch utilise la valeur de priorité de hello de commande de hello toodetermine hello travail de planification des tâches dans un compte (ce n’est pas toobe peut être confondue avec un [tâche planifiée](#scheduled-jobs)). les valeurs de priorité de Hello comprises entre -1000 too1000, avec-1 000 étant la priorité la plus basse hello et 1000 hello plus élevé. priorité de hello tooupdate d’une tâche, l’appel hello [hello des propriétés d’une tâche de mise à jour] [ rest_update_job] opération (lot reste), ou modifier hello [CloudJob.Priority] [ net_cloudjob_priority] propriété (lot .NET).

Au sein de hello même compte, présentant une priorité plus élevée travaux ont une priorité de planification sur les tâches de priorité plus faible. Un travail à priorité supérieure dans un compte n’est pas prioritaire en termes de planification sur un autre travail à priorité inférieure dans un autre compte.

La planification de travail entre pools est indépendante. Entre des pools différents, un travail à priorité supérieure n’est pas systématiquement planifié en premier si le pool auquel il est associé n’a pas suffisamment de nœuds inactifs. Bonjour même pool, des travaux par hello même niveau de priorité ont autant de chance d’être planifié.

### <a name="scheduled-jobs"></a>Scheduled jobs
[Les planifications du travail] [ rest_job_schedules] vous activer toocreate les travaux récurrents dans hello service Batch. Une planification de travail spécifie quand toorun des travaux et inclut les spécifications de hello de toobe de travaux hello exécuter. Vous pouvez spécifier la durée durée hello de planification de hello--lorsque hello planification est en vigueur--et la fréquence à laquelle les travaux sont créés au cours de hello planifiée période.

## <a name="task"></a>Task
Une tâche est une unité de calcul associée à un travail. Elle s’exécute sur un nœud. Tâches affectées nœud tooa pour l’exécution ou en file d’attente jusqu'à ce qu’un nœud devienne disponible. En réalité, une tâche exécute un ou plusieurs programmes ou scripts sur un calcul nœud tooperform hello travail que vous devez effectue.

Lorsque vous créez une tâche, vous pouvez spécifier les éléments suivants :

* Hello **ligne de commande** pour la tâche hello. Il s’agit de ligne de commande hello qui exécute votre application ou le script sur le nœud de calcul hello.

    Il est important de toonote qui hello de ligne de commande ne s’exécute pas sous un interpréteur de commandes. Par conséquent, il ne peut pas en mode natif bénéficier des fonctionnalités du shell comme [variable d’environnement](#environment-settings-for-tasks) expansion (Cela inclut hello `PATH`). tootake parti de ces fonctionnalités, vous devez appeler shell hello dans la ligne de commande hello--par exemple, en lançant `cmd.exe` sur les nœuds Windows ou `/bin/sh` sur Linux :

    `cmd /c MyTaskApplication.exe %MY_ENV_VAR%`

    `/bin/sh -c MyTaskApplication $MY_ENV_VAR`

    Si vos tâches doivent toorun une application ou un script qui n’est pas hello du nœud `PATH` ou référencer des variables d’environnement, appelez la fonctionnalité interpréteur de commandes hello explicitement dans la ligne de commande de tâche hello.
* **Fichiers de ressources** qui contiennent hello toobe de données traitée. Ces fichiers sont nœud toohello automatiquement copiée à partir du stockage d’objets Blob dans un compte de stockage Azure à usage général avant l’exécution de ligne de commande de la tâche hello. Pour plus d’informations, consultez les sections hello [tâche de démarrage](#start-task) et [fichiers et répertoires](#files-and-directories).
* Hello **variables d’environnement** qui sont requises par votre application. Pour plus d’informations, consultez hello [paramètres d’environnement pour les tâches](#environment-settings-for-tasks) section.
* Hello **contraintes** sous le hello tâche doit s’exécuter. Par exemple, les contraintes incluent la durée maximale de hello cette tâche hello est autorisée toorun, nombre maximal de hello de tentatives d’une tâche ayant échoué doit être, et l’heure maximum de hello les fichiers dans le répertoire de travail de la tâche hello sont conservés.
* **Les packages d’applications** toodeploy toohello sur le hello tâche est planifiée toorun de nœud de calcul. [Les packages d’applications](#application-packages) fournissent un déploiement simplifié et le contrôle de version des applications hello qui exécutent des tâches. Les packages d’applications de niveau de la tâche sont particulièrement utiles dans les environnements de pool partagé, où différentes tâches sont exécutées sur un pool et pool de hello n’est pas supprimé lorsqu’un travail est terminé. Si votre travail comporte moins de tâches que les nœuds dans le pool de hello, packages d’applications de tâche peuvent réduire le transfert de données depuis votre application est déployée toohello uniquement les nœuds qui exécutent des tâches.

En outre tootasks vous définissez tooperform calcul sur un nœud, hello tâches spéciales suivantes est également fourni par le service de traitement par lots hello :

* [Tâche de démarrage](#start-task)
* [Tâche du gestionnaire de travaux](#job-manager-task)
* [Tâches de préparation et lancement](#job-preparation-and-release-tasks)
* [Tâches multi-instances (MPI)](#multi-instance-tasks)
* [Dépendances de la tâche](#task-dependencies)

### <a name="start-task"></a>Tâche de démarrage
En associant un **démarrer la tâche** avec un pool, vous pouvez préparer hello système d’exploitation de ses nœuds. Par exemple, vous pouvez effectuer des actions telles que l’installation d’applications hello qui exécutent des tâches ou de lancer des processus en arrière-plan. tâche de démarrage Hello s’exécute chaque fois qu’un nœud démarre, pour tant qu’il reste dans le pool de hello, y compris lorsque le nœud hello est ajouté en premier toohello pool et lorsqu’il est redémarré ou réinitialisé.

Le principal avantage de la tâche de démarrage hello est qu’il peut contenir toutes les informations hello sont nécessaire tooconfigure un nœud de calcul et installer des applications hello qui sont requises pour l’exécution de la tâche. Par conséquent, il est aussi simple que la spécification du nombre de nœud cible nouveaux hello d’augmenter le nombre hello de nœuds dans un pool. tâche de démarrage Hello fournit hello lot service hello informations nécessaires tooconfigure hello nouveaux nœuds et les préparer pour l’acceptation de tâches.

Comme avec toutes les tâches de traitement par lots Azure, vous pouvez spécifier une liste de **les fichiers de ressources** dans [Azure Storage][azure_storage], en outre tooa **ligne de commande** toobe exécutée. service de traitement par lots Hello tout d’abord copie le nœud de toohello de fichiers de ressources hello depuis le stockage Azure et exécute ensuite la ligne de commande hello. Pour une tâche de démarrage pool, liste des fichiers hello contient généralement hello tâche application et ses dépendances.

Toutefois, tâche de démarrage hello peut aussi inclure toobe de données de référence utilisé par toutes les tâches qui sont exécutent sur le nœud de calcul hello. Par exemple, la ligne de commande d’une tâche de démarrage peut effectuer un `robocopy` opération toocopy fichiers d’application (qui ont été spécifiées en tant que fichiers de ressources et téléchargé toohello nœud) à partir de hello démarrer la tâche [répertoire de travail](#files-and-directories) toohello [dossier partagé](#files-and-directories), puis exécutez un fichier MSI ou `setup.exe`.

Il est généralement souhaitable hello lot service toowait pour toocomplete de tâche de démarrage hello avant de considérer hello tâches toobe prêt attribué de nœud, mais vous pouvez la configurer.

Si une tâche de démarrage échoue sur un nœud de calcul, puis hello l’état du nœud de hello est mise à jour tooreflect hello échec et nœud de hello ne possède pas toutes les tâches. Une tâche de démarrage peut échouer s’il existe un problème de copie de ses fichiers de ressources de stockage, ou si le processus de hello exécuté par sa ligne de commande retourne un code de sortie différent de zéro.

Si vous ajoutez ou mettez à jour de la tâche de démarrage hello pour un pool existant, vous devez redémarrer ses nœuds de calcul pour les nœuds de toohello hello début tâche toobe appliqué.

>[!NOTE]
> Hello taille totale d’une tâche de démarrage doit être inférieur ou égal too32768 caractères, y compris les fichiers de ressources et les variables d’environnement. tooensure que votre tâche de démarrage répond à cette exigence, vous pouvez utiliser une des deux approches :
>
> 1. Vous pouvez utiliser l’application packages toodistribute applications ou des données sur chaque nœud de votre pool de traitement par lots. Pour plus d’informations sur les packages d’applications, consultez [déployer des nœuds de toocompute d’applications avec des packages d’application de lot](batch-application-packages.md).
> 2. Vous pouvez créer manuellement une archive au format ZIP contenant vos fichiers d’applications. Télécharger votre stockage de tooAzure archive compressé comme un objet blob. Spécifiez les archive hello compressé comme un fichier de ressources pour votre tâche de démarrage. Avant l’exécution de la ligne de commande hello pour votre tâche de démarrage décompressez l’archive hello à partir de la ligne de commande hello. 
>
>    archive de hello toounzip, vous pouvez utiliser hello d’archivage de l’outil de votre choix. Vous devez tooinclude hello outil que vous archive de hello toounzip comme fichier de ressources pour la tâche de démarrage hello.
>
>

### <a name="job-manager-task"></a>Tâche du gestionnaire de travaux
Vous utilisez généralement un **tâche du gestionnaire** toocontrol et/ou d’analyse de la tâche d’exécution--par exemple, toocreate et soumettre des tâches hello pour un travail, déterminer les tâches supplémentaires toorun et déterminer quand le travail est terminé. Toutefois, une tâche du gestionnaire n’est pas restreinte toothese activités. Il s’agit d’une tâche chevronnée que peut effectuer toutes les actions qui sont requises pour la tâche de hello. Par exemple, une tâche du gestionnaire peut télécharger un fichier qui est spécifié en tant que paramètre, analyser le contenu hello de ce fichier et soumettre des tâches supplémentaires basées sur ce contenu.

Une tâche du gestionnaire de travaux est lancée avant toutes les autres tâches. Il fournit hello suivant de fonctionnalités :

* Il est automatiquement envoyé sous la forme d’une tâche par hello service Batch lors de la création du travail de hello.
* Elle est planifiée tooexecute hello avant d’autres tâches dans un projet.
* Son nœud associé est hello dernière toobe est supprimé d’un pool, lorsque le pool de hello est en cours downsized.
* La résiliation peut être arrêt toohello liée de toutes les tâches dans la tâche de hello.
* Une tâche du gestionnaire est prioritée hello plus élevée quand il a besoin toobe redémarré. Si un nœud inactif n’est pas disponible, hello service Batch peut mettre fin à une Hello autres tâches en cours d’exécution dans la salle de toomake pool hello pour hello travail manager tâche toorun.
* Une tâche du gestionnaire dans un travail n’a pas priorité sur des tâches hello d’autres tâches. Parmi les travaux, seules les priorités au niveau du travail sont observées.

### <a name="job-preparation-and-release-tasks"></a>Tâches de préparation et lancement
Batch fournit des tâches de préparation des travaux pour la configuration de l’exécution des travaux préliminaire. Les tâches de validation des travaux sont destinées à la maintenance ou au nettoyage postérieurs aux travaux.

* **Tâche de préparation**: une tâche de préparation du travail s’exécute sur tous les nœuds de calcul qui sont des tâches planifiées toorun, avant tout hello autres tâches sont exécutées. Vous pouvez utiliser les données de toocopy de tâches préparation du travail qui est partagée par toutes les tâches, mais toohello unique tâche, par exemple.
* **Tâche de mise en production**: lorsqu’un travail est terminé, une tâche de mise en production de travail s’exécute sur chaque nœud dans le pool de hello exécutée au moins une tâche. Vous pouvez utiliser une version tâche toodelete données de la tâche sont copiée par la tâche de préparation du travail hello ou toocompress et téléchargement de données de journal diagnostic, par exemple.

Préparation à la fois la tâche et les tâches de mise en production vous toospecify un toorun de ligne de commande lorsque la tâche hello est appelée. Elles offrent des fonctionnalités telles que le téléchargement de fichiers, une exécution élevée, des variables d’environnement personnalisées, une durée d’exécution maximale, le nombre de tentatives et la durée de rétention des fichiers.

Pour plus d’informations sur les tâches de préparation de travail et de validation, consultez [Exécuter les tâches de préparation de travail et de validation sur les nœuds de calcul Azure Batch](batch-job-prep-release.md).

### <a name="multi-instance-task"></a>Tâche multi-instance
A [tâche d’instances multiples](batch-mpi.md) est une tâche qui est configuré toorun sur plusieurs nœuds de calcul simultanément. Avec les tâches de plusieurs instances, vous pouvez activer la haute performance des scénarios informatiques qui nécessitent un groupe de nœuds de calcul qui sont alloués ensemble tooprocess une charge de travail unique (comme Interface MPI (Message Passing)).

Pour plus d’informations sur l’exécution des travaux MPI dans le lot à l’aide de bibliothèque de lot .NET hello, passez en revue [multi-instance utilisez tâches toorun les applications d’Interface MPI (Message Passing) dans Azure Batch](batch-mpi.md).

### <a name="task-dependencies"></a>Dépendances de la tâche
[Dépendances de tâches](batch-task-dependencies.md), en tant que hello nom l’indique, vous permettre de toospecify qui dépend de la tâche à la fin de hello d’autres tâches avant son exécution. Cette fonctionnalité prend en charge pour les situations dans lesquelles une tâche « en aval » consomme sortie hello d’une tâche « en amont », ou lorsqu’une tâche en amont effectue une initialisation requise par une tâche en aval. toouse cette fonctionnalité, vous devez première interdépendances activer sur le traitement par lots. Ensuite, pour chaque tâche qui dépend d’un autre (ou bien d’autres), vous spécifiez les tâches hello qui dépend de cette tâche.

Avec des dépendances de tâche, vous pouvez configurer des scénarios, par exemple hello suivantes :

* *taskB* dépend de *taskA* (l’exécution de *taskB* ne commence pas tant que celle de *taskA* n’est pas terminée).
* *taskC* dépend de *taskA* et de *taskB*.
* *taskD* dépend d’une plage de tâches, notamment des tâches *1* à *10* avant de pouvoir s’exécuter.

Extraire [interdépendances dans Azure Batch](batch-task-dependencies.md) et hello [TaskDependencies] [ github_sample_taskdeps] exemple de code dans hello [exemples de traitement par lots azure] [ github_samples] Référentiel GitHub pour plus d’informations détaillées sur cette fonctionnalité.

## <a name="environment-settings-for-tasks"></a>Paramètres d’environnement des tâches
Chaque tâche exécutée par hello service Batch a variables tooenvironment accès qu’il définit sur les nœuds de calcul. Cela inclut des variables d’environnement définies par hello service Batch ([défini par le service][msdn_env_vars]) et les variables d’environnement personnalisées que vous pouvez définir pour vos tâches. applications de Hello et des scripts de le qu'exécution de vos tâches ont accès les variables d’environnement toothese pendant l’exécution.

Vous pouvez définir des variables d’environnement personnalisées au niveau de tâche ou travail hello en remplissant hello *paramètres d’environnement* propriété pour ces entités. Par exemple, consultez hello [ajouter une tâche de tooa] [ rest_add_task] opération (API REST de traitement par lots), ou hello [CloudTask.EnvironmentSettings] [ net_cloudtask_env] et [ CloudJob.CommonEnvironmentSettings] [ net_job_env] propriétés dans le lot .NET.

Votre application cliente ou le service peut obtenir variables d’environnement d’une tâche, défini par le service et personnalisés, à l’aide de hello [obtenir des informations sur une tâche] [ rest_get_task_info] opération (lot reste) ou en accédant à Hello [CloudTask.EnvironmentSettings] [ net_cloudtask_env] propriété (lot .NET). Processus qui s’exécutent sur un nœud de calcul peuvent y accéder, et d’autres variables d’environnement sur le nœud hello, par exemple, à l’aide de hello familier `%VARIABLE_NAME%` (Windows) ou `$VARIABLE_NAME` syntaxe (Linux).

Vous trouverez la liste complète des variables d’environnement définies par le service dans l’article [Compute node environment variables][msdn_env_vars] (Variables d’environnement de nœud de calcul).

## <a name="files-and-directories"></a>Fichiers et répertoires
Chaque tâche possède un *répertoire de travail* sous lequel elle crée zéro ou plusieurs fichiers et répertoires. Ce répertoire de travail peut être utilisé pour stocker un programme hello qui est exécuté par la tâche hello, données hello qu’il traite, et hello de sortie de traitement hello qu'il effectue. Tous les fichiers et répertoires d’une tâche sont détenus par l’utilisateur de la tâche hello.

Hello service Batch expose une partie du système de fichiers hello sur un nœud en tant que hello *répertoire racine*. Puissent y accéder répertoire hello en référençant hello `AZ_BATCH_NODE_ROOT_DIR` variable d’environnement. Pour plus d’informations sur l’utilisation de variables d’environnement, consultez la section [Paramètres d’environnement des tâches](#environment-settings-for-tasks).

répertoire racine de Hello contient hello suivant la structure de répertoires :

![Structure de répertoire du nœud de calcul][1]

* **partagé**: ce répertoire fournit l’accès en lecture/écriture trop*tous les* tâches qui s’exécutent sur un nœud. Toute tâche qui s’exécute sur le nœud de hello permettre créer, lire, mettre à jour et supprimer des fichiers dans ce répertoire. Les tâches peuvent accéder au répertoire en référençant hello `AZ_BATCH_NODE_SHARED_DIR` variable d’environnement.
* **Démarrage**: ce répertoire est utilisé par une tâche de démarrage en tant que répertoire de travail. Tous les fichiers de hello sont nœud toohello téléchargé par la tâche de démarrage hello sont stockées ici. tâche de démarrage Hello permettre créer, lire, mettre à jour et supprimer des fichiers sous ce répertoire. Les tâches peuvent accéder au répertoire en référençant hello `AZ_BATCH_NODE_STARTUP_DIR` variable d’environnement.
* **Tâches**: un répertoire est créé pour chaque tâche qui s’exécute sur le nœud de hello. Il est accessible en référençant hello `AZ_BATCH_TASK_DIR` variable d’environnement.

    Dans chaque répertoire de tâche, hello service Batch crée un répertoire de travail (`wd`) dont le chemin unique est spécifié par hello `AZ_BATCH_TASK_WORKING_DIR` variable d’environnement. Ce répertoire fournit la tâche toohello d’accès en lecture/écriture. tâche Hello permettre créer, lire, mettre à jour et supprimer des fichiers sous ce répertoire. Ce répertoire est conservé en fonction de hello *RetentionTime* contrainte qui est spécifié pour la tâche hello.

    `stdout.txt`et `stderr.txt`: ces fichiers sont écrits de dossier de tâches toohello pendant l’exécution de hello de tâche hello.

> [!IMPORTANT]
> Lorsqu’un nœud est supprimé de pool de hello, *tous les* de hello les fichiers qui sont stockés sur le nœud de hello sont supprimés.
>
>

## <a name="application-packages"></a>packages d’application
Hello [des packages d’application](batch-application-packages.md) fonctionnalité fournit une gestion plus simple et le déploiement d’applications toohello les nœuds de calcul dans les pools. Vous pouvez télécharger et gérer plusieurs versions de hello applications exécutées par vos tâches, y compris les fichiers binaires et les fichiers de support. Ensuite, vous pouvez déployer automatiquement une ou plusieurs de ces applications toohello nœuds de calcul dans votre pool de.

Vous pouvez spécifier les packages d’applications au niveau de pool et la tâche hello. Lorsque vous spécifiez des packages d’application pool, application hello est nœud tooevery déployé dans le pool de hello. Lorsque vous spécifiez des packages d’applications Office, application hello est déployé toonodes uniquement qui sont planifiée toorun au moins une des tâches du travail hello, juste avant hello d’exécuter la ligne de commande de la tâche.

Handles de lot hello détails d’utilisation de stockage Azure toostore vos packages d’application et les déploiement toocompute nœuds, afin de la charge de votre code et la gestion peut être simplifiée.

toofind plus d’informations sur la fonctionnalité de package d’application hello, extraire [déployer des nœuds de toocompute d’applications avec des packages d’application de lot](batch-application-packages.md).

> [!NOTE]
> Si vous ajoutez le pool application packages tooan *existant* pool, vous devez redémarrer les nœuds de calcul pour application hello packages des nœuds de toohello toobe déployé.
>
>

## <a name="pool-and-compute-node-lifetime"></a>Durée de vie de nœud de pool et de calcul
Lorsque vous concevez votre solution de traitement par lots Azure, vous disposez toomake une décision de conception sur la façon et pools sont créés et la durée de calcul nœuds au sein de ces pools restent disponibles.

Sur l’extrémité du spectre de hello, vous pouvez créer un pool pour chaque tâche que vous envoyez et supprimer le pool de hello dès que ses tâches de fin d’exécution. Cela permet d’optimiser l’utilisation, car les nœuds hello sont alloués seulement lorsque nécessaire et arrêter dès qu’ils sont inactifs. Bien que cela signifie que le travail de hello doit attendre toobe de nœuds hello alloué, il est important toonote tâches planifiées pour l’exécution de nœuds sont disponibles individuellement, alloué, dès qu’et hello tâche de démarrage est terminée. Traitement par lots est *pas* patienter jusqu'à ce que tous les nœuds au sein d’un pool sont disponibles avant d’attribuer des tâches toohello nœuds. Cela garantit l’utilisation maximale de tous les nœuds disponibles.

À hello autre extrémité du spectre hello si travaux démarrer immédiatement est priorité la plus élevée de hello, vous pouvez créer un pool à l’avance et disposition de ses nœuds avant l’envoi des travaux. Dans ce scénario, les tâches peuvent démarrer immédiatement, mais les nœuds peuvent inactif en attendant les toobe attribué.

Une approche combinée est généralement utilisée pour la gestion d’une charge variable, mais continue. Vous pouvez avoir un pool que plusieurs tâches sont soumises à, mais peuvent évoluer nombre hello de nœuds vers le haut ou vers le bas selon la charge de travail toohello (consultez [mise à l’échelle des ressources de calcul](#scaling-compute-resources) Bonjour suivant la section). Vous pouvez procéder en réaction, en fonction de la charge actuelle, ou en amont, si la charge peut être prédite.

## <a name="virtual-network-vnet-and-firewall-configuration"></a>Configuration du pare-feu et du réseau virtuel (VNet) 

Lorsque vous configurez un pool de nœuds de calcul dans Azure Batch, vous pouvez associer le pool de hello à un sous-réseau de Azure [réseau virtuel (VNet)](../virtual-network/virtual-networks-overview.md). toolearn savoir plus sur la création d’un réseau virtuel avec des sous-réseaux, consultez [créer un réseau virtuel Azure avec des sous-réseaux](../virtual-network/virtual-networks-create-vnet-arm-pportal.md). 

 * Hello réseau virtuel associé à un pool doit être :

   * Dans hello Azure même **région** comme hello compte Azure Batch.
   * Dans hello même **abonnement** comme hello compte Azure Batch.

* type Hello de réseau virtuel pris en charge dépend de comment les pools sont en cours allouées pour hello compte Batch :

    - Si le mode d’allocation de pool hello pour votre compte Batch a la valeur tooBatch Service, puis vous pouvez affecter un toopools seul réseau virtuel créé par hello **Configuration des Services Cloud**. En outre, hello spécifié le que réseau virtuel doit être créé avec le modèle de déploiement classique hello. Réseaux virtuels créés avec le modèle de déploiement du Gestionnaire de ressources Azure hello ne sont pas pris en charge.
 
    - Si le mode d’allocation de pool hello pour votre compte Batch a la valeur tooUser abonnement, puis vous pouvez affecter un toopools seul réseau virtuel créé par hello **Configuration d’ordinateur virtuel**. Les pools créés avec hello **Configuration du Service Cloud** ne sont pas pris en charge. Hello que réseau virtuel associé peut être créée avec le modèle de déploiement du Gestionnaire de ressources Azure hello ou de modèle de déploiement classique hello.

    Pour une table de résumé de prise en charge du réseau virtuel selon le mode d’allocation toopool, consultez hello [mode d’allocation de Pool](#pool-allocation-mode) section.

* Si mode d’allocation de pool hello pour votre compte de traitement par lots est tooBatch Service, vous devez fournir les autorisations pour hello tooaccess principal de service de traitement par lots hello réseau virtuel. Hello réseau virtuel doit affecter hello [Classic Virtual Machine Contributor Role-Based contrôle d’accès (RBAC)](https://azure.microsoft.com/documentation/articles/role-based-access-built-in-roles/#classic-virtual-machine-contributor) principal du service de rôle toohello lot. Si hello spécifié n’est pas fourni de rôle RBAC, service de traitement par lots hello retourne 400 (demande incorrecte). rôle de hello tooadd Bonjour portail Azure :

    1. Sélectionnez hello **réseau virtuel**, puis **(IAM) de contrôle d’accès** > **rôles** > **contributeur de l’ordinateur virtuel**  >  **Ajouter**.
    2. Sur hello **ajouter des autorisations** panneau, sélectionnez hello **contributeur de l’ordinateur virtuel** rôle.
    3. Sur hello **ajouter des autorisations** panneau, recherchez hello API de lot. Rechercher pour chacune de ces chaînes, à son tour jusqu'à ce que vous trouviez hello API :
        1. **MicrosoftAzureBatch**.
        2. **Microsoft Azure Batch**. Les locataires Azure AD les plus récents peuvent utiliser ce nom.
        3. **ddbf3205-c6bd-46AE-8127-60eb93363864** ID de hello pour hello API de lot. 
    3. Sélectionnez hello principal du service API de lot. 
    4. Cliquez sur **Enregistrer**.

        ![Affecter des collaborateurs de machine virtuelle rôle tooBatch service principal](./media/batch-api-basics/iam-add-role.png)


* Hello spécifiée de sous-réseau doit avoir suffisamment libre **des adresses IP** tooaccommodate hello nombre total de nœuds cibles ; autrement dit, hello somme de hello `targetDedicatedNodes` et `targetLowPriorityNodes` propriétés d’un pool hello. Si le sous-réseau de hello n’a pas suffisamment d’adresses IP libres, hello service Batch partiellement alloue des nœuds de calcul hello dans le pool de hello et renvoie une erreur de redimensionnement.

* Hello spécifié sous-réseau doive autoriser la communication à partir de hello lot service toobe tooschedule en mesure de tâches sur les nœuds de calcul hello. Si les nœuds de calcul toohello de communication est refusé par un **groupe de sécurité réseau (NSG)** associé hello réseau virtuel, puis hello service Batch définit état hello hello de nœuds de calcul trop**inutilisable**.

* Si hello spécifié est associé à des réseaux **groupes de sécurité réseau (NSG)** et/ou un **pare-feu**, puis quelques ports système réservé doivent être activés pour les communications entrantes :

- Pour les pools créés avec une configuration de machine virtuelle, activez les ports 29876 et 29877, ainsi que le port 22 pour Linux et le port 3389 pour Windows. 
- Pour les pools créés avec une configuration de service cloud, activez les ports 10100, 20100 et 30100. 
- Activer les connexions sortantes tooAzure stockage sur le port 443. Aussi, assurez-vous que votre point de terminaison de Stockage Azure peut être résolu par tous les serveurs DNS personnalisés qui traitent votre réseau virtuel. Plus précisément, une URL sous forme de hello `<account>.table.core.windows.net` doit pouvoir être résolu.

    Hello tableau suivant décrit hello ports dont vous avez besoin de tooenable pour les pools que vous avez créé avec la configuration d’ordinateur virtuel hello d’entrée :

    |    Port(s) de destination    |    Adresse IP source      |    Azure Batch ajoute-t-il des NSG ?    |    Requis pour toobe VM utilisable ?    |    Action que l’utilisateur doit effectuer   |
    |---------------------------|---------------------------|----------------------------|-------------------------------------|-----------------------|
    |    <ul><li>Pour des pools créés avec la configuration d’ordinateur virtuel hello : 29876, 29877</li><li>Pour des pools créés avec la configuration du service cloud hello : 10100, 20100 30100</li></ul>         |    Adresses IP du rôle de service Batch uniquement |    Oui. Lot ajoute des groupes de sécurité réseau au niveau de hello de réseau interfaces (NIC) connectées tooVMs. Ces NSG autorisent le trafic uniquement à partir d’adresses IP du rôle de service Batch. Même si vous ouvrez ces ports pour tout site web de hello, du trafic de hello doit obtenir bloqué à hello carte réseau. |    Oui  |  Vous n’avez pas besoin de toospecify un groupe de sécurité réseau, car seules les adresses IP de traitement par lots permet de lot. <br /><br /> Toutefois, si vous ne spécifiez pas de NSG, assurez-vous que ces ports sont ouverts pour le trafic entrant. <br /><br /> Si vous spécifiez * comme hello IP source dans votre groupe de sécurité réseau, lot ajoute toujours les groupes de sécurité réseau au niveau de hello de carte réseau attachée tooVMs. |
    |    3389, 22               |    Ordinateurs de l’utilisateur, utilisées pour le débogage, afin que vous pouvez accéder à distance hello machine virtuelle.    |    Non                                    |    Non                     |    Ajouter des groupes de sécurité réseau toohello d’accès à distance (RDP/SSH) toopermit machine virtuelle.   |                 

    Hello tableau suivant décrit le port sortant hello que vous avez besoin de tooenable toopermit accès tooAzure stockage :

    |    Port(s) sortant(s)    |    Destination    |    Azure Batch ajoute-t-il des NSG ?    |    Requis pour toobe VM utilisable ?    |    Action que l’utilisateur doit effectuer    |
    |------------------------|-------------------|----------------------------|-------------------------------------|------------------------|
    |    443    |    Azure Storage    |    Non    |    Oui    |    Si vous ajoutez des groupes de sécurité réseau, puis vérifiez que ce port est ouvert toooutbound trafic.    |


## <a name="scaling-compute-resources"></a>Mise à l’échelle des ressources de calcul
Avec [mise à l’échelle automatique](batch-automatic-scaling.md), vous pouvez avoir service de traitement par lots hello ajuster dynamiquement le nombre de hello de nœuds de calcul dans un pool en fonction de toohello utilisation actuelle de la charge de travail et des ressources de votre scénario de calcul. Cela vous permet de toolower hello coût global de l’exécution de votre application en utilisant uniquement les ressources hello que vous avez besoin, et celles libération vous n’avez pas besoin.

Pour activer la mise à l’échelle automatique, écrivez une [formule de mise à l’échelle automatique](batch-automatic-scaling.md#automatic-scaling-formulas) et associez-la à un pool. Hello service Batch utilise hello toodetermine formule hello cible différents nœuds dans le pool de hello pour l’intervalle de mise à l’échelle suivant hello (intervalle que vous pouvez configurer). Vous pouvez spécifier les paramètres de mise à l’échelle automatique hello pour un pool lorsque vous créez ou activez la mise à l’échelle sur un pool de versions ultérieures. Vous pouvez également mettre à jour hello mise à l’échelle des paramètres sur un pool activée à la mise à l’échelle.

Par exemple, peut-être un travail nécessite que vous envoyez un très grand nombre de toobe de tâches exécutée. Vous pouvez affecter un pool toohello formule mise à l’échelle qui s’adapte nombre hello de nœuds dans le pool de hello basée sur le nombre actuel de hello de tâches en file d’attente et le taux d’achèvement hello de tâches hello travail de hello. Hello service Batch régulièrement évalue la formule de hello et peut être redimensionné pool hello, en fonction de la charge de travail et d’autres paramètres de formule. Hello service ajoute des nœuds si nécessaire lorsqu’il existe un grand nombre de tâches en file d’attente et supprime les nœuds lorsqu’il n’y a aucune tâche en file d’attente ou en cours d’exécution.

Une formule de mise à l’échelle peut être basée sur hello suivant des métriques :

* **Métriques temporelles** basées sur les statistiques collectées toutes les cinq minutes dans hello spécifié nombre d’heures.
* **mesures de ressources** sont basées sur l’utilisation du processeur, de la bande passante et de la mémoire, et sur le nombre de nœuds.
* Les **mesures de tâches** sont basées sur l’état de la tâche, tel que *Active* (en file d’attente), *En cours d’exécution* ou *Terminée*.

Lors de la mise à l’échelle automatique de diminue le nombre de hello de nœuds de calcul dans un pool, vous devez considérer comment toohandle les tâches qui sont en cours d’exécution au moment de hello Hello diminuer opération. tooaccommodate, lot fournit un *option désallocation de nœud* que vous pouvez inclure dans vos formules. Par exemple, vous pouvez spécifier que les tâches en cours d’exécution sont arrêtés immédiatement, arrêtés immédiatement et puis remis pour l’exécution sur un autre nœud ou autorisés toofinish avant le nœud de hello est supprimée hello pool.

Pour plus d’informations sur la mise à l’échelle automatique d’une application, consultez la section [Mettre automatiquement à l’échelle les nœuds de calcul dans un pool Azure Batch](batch-automatic-scaling.md).

> [!TIP]
> toomaximize l’utilisation des ressources de calcul, définir le nombre de cibles de hello de nœuds toozero à fin hello d’un travail, mais autoriser toofinish de tâches en cours d’exécution.
>
>

## <a name="security-with-certificates"></a>Sécurité avec certificats
En règle générale, vous devez toouse certificats lorsque vous chiffrez ou déchiffrer des informations sensibles pour les tâches, comme la clé hello pour un [compte de stockage Azure][azure_storage]. toosupport, vous pouvez installer des certificats sur les nœuds. Les secrets chiffrés sont passées de tootasks via des paramètres de ligne de commande ou incorporés dans une des ressources de la tâche hello et les certificats de hello installé peuvent être utilisé toodecrypt les.

Vous utilisez hello [ajouter un certificat] [ rest_add_cert] opération (lot reste) ou [CertificateOperations.CreateCertificate] [ net_create_cert] (méthode) (lot .NET) tooadd un tooa de certificat du compte Batch. Vous pouvez ensuite associer hello certificat un pool existant ou nouveau. Lorsqu’un certificat est associé à un pool, hello service Batch installe le certificat de hello sur chaque nœud dans le pool de hello. Hello service Batch certificats hello appropriée au démarrage de nœud de hello, avant de lancer des tâches (y compris la tâche de démarrage hello et la tâche du gestionnaire).

Si vous ajoutez des certificats tooan *existant* pool, vous devez redémarrer les nœuds de calcul de hello certificats toobe appliqué toohello nœuds.

## <a name="error-handling"></a>Gestion des erreurs
Il peut s’avérer nécessaire toohandle les échecs de tâche et application dans votre solution de traitement par lots.

### <a name="task-failure-handling"></a>Gestion des échecs de tâche
Les échecs de tâche peuvent être classés suivant les catégories suivantes :

* **Échecs de prétraitement**

    Si une tâche échoue toostart, une erreur de prétraitement est définie pour la tâche hello.  

    Erreurs de pré-traitement peut se produire si les fichiers de ressources de la tâche hello ont déplacé, hello compte de stockage n’est plus disponible ou un autre problème a été rencontré que hello empêché réussie copie des fichiers toohello nœud.

* **Échecs de chargement de fichier**

    Si le téléchargement de fichiers qui sont spécifiés pour une tâche échoue pour une raison quelconque, une erreur de téléchargement de fichier est définie pour la tâche hello.

    Erreurs peuvent se produire si hello SAS fournis pour accéder à un stockage Azure n’est pas valide ou ne fournit pas d’autorisations en écriture, si le compte de stockage hello n’est plus disponible, ou si un autre problème a été rencontré et qu’il a empêché hello réussie de copie de fichiers à partir de téléchargement de fichier nœud de Hello.    

* **Échecs d’application**

    Hello spécifié par la ligne de commande de la tâche hello peut également échouer. Hello processus est considéré comme toohave a échoué lors d’un code de sortie différent de zéro est retourné par le processus de hello est exécutée par la tâche hello (consultez *les codes de sortie de tâche* dans la section suivante de hello).

    Pour les défaillances d’application, vous pouvez configurer le lot tâche hello tooa tooautomatically réessayer un nombre spécifié de fois.

* **Échecs de contrainte**

    Vous pouvez définir une contrainte qui spécifie durée maximale d’exécution de hello pour un travail ou une tâche, hello *maxWallClockTime*. Cela peut être utile pour les tâches non tooprogress conformes à la fin d’exécution.

    Lorsque la durée maximale hello a été dépassée, la tâche hello est marqué comme *terminé*, mais le code de sortie hello est défini trop`0xC000013A` et hello *schedulingError* champ est marqué comme `{ category:"ServerError", code="TaskEnded"}`.

### <a name="debugging-application-failures"></a>Débogage des échecs d’application
* `stderr` et `stdout`

    Pendant l’exécution, une application risque de produire une sortie de diagnostic que vous pouvez utiliser tootroubleshoot problèmes. Comme mentionné dans hello à la section précédente [fichiers et répertoires](#files-and-directories), hello service Batch écrit la sortie standard et l’erreur standard de sortie trop`stdout.txt` et `stderr.txt` nœud de calcul des fichiers dans le répertoire de tâche hello sur hello. Vous pouvez utiliser hello portail Azure ou l’un des toodownload de kits de développement logiciel lot hello ces fichiers. Par exemple, vous pouvez récupérer ces autres fichiers et à des fins de dépannage à l’aide de [ComputeNode.GetNodeFile] [ net_getfile_node] et [CloudTask.GetNodeFile] [ net_getfile_task] dans la bibliothèque de lot .NET hello.

* **Codes de sortie de tâche**

    Comme mentionné précédemment, une tâche est marquée comme ayant échoué par le service de traitement par lots hello si les processus hello qui sont exécutée par la tâche hello retourne un code de sortie différent de zéro. Lorsqu’une tâche exécute un processus, lot remplit la propriété de code de sortie de la tâche hello avec hello *renvoie le code d’un processus de hello*. Il est important toonote que le code de sortie d’une tâche est **pas** déterminé par hello service Batch. Le code de sortie d’une tâche est déterminé par les processus hello lui-même ou système d’exploitation de hello sur les processus hello exécuté.

### <a name="accounting-for-task-failures-or-interruptions"></a>Prise en compte des échecs ou des interruptions de tâche
Les tâches peuvent parfois échouer ou être interrompues. Hello tâche application lui-même peut échouer, nœud hello sur quel hello tâche est en cours d’exécution peut être redémarré ou hello nœud peut être supprimé à partir du pool de hello pendant une opération de redimensionnement si hello stratégie de désallocation du pool est ensemble des nœuds de tooremove immédiatement sans attendre toofinish de tâches. Dans tous les cas, tâche hello permettre être automatiquement remis par lot pour l’exécution sur un autre nœud.

Il est également possible pour un problème intermittent de toocause un toohang de tâche ou prendre tooexecute trop long. Vous pouvez définir l’intervalle d’exécution maximale hello pour une tâche. Si l’intervalle de salutation d’exécution maximale est dépassée, hello service Batch interrompt l’application de tâche hello.

### <a name="connecting-toocompute-nodes"></a>Connexion toocompute nœuds
Vous pouvez effectuer la résolution des problèmes en vous connectant à distance tooa de nœud de calcul et de débogage supplémentaires. Vous pouvez utiliser hello toodownload portail Azure un fichier de protocole RDP (Remote Desktop) pour les nœuds de Windows et obtenir des informations de connexion Secure Shell (SSH) pour des nœuds Linux. Également procéder à l’aide de hello API de lot--par exemple, avec [Batch .NET] [ net_rdpfile] ou [lot Python](batch-linux-nodes.md#connect-to-linux-nodes-using-ssh).

> [!IMPORTANT]
> nœud de tooa tooconnect via RDP ou SSH, vous devez d’abord créer un utilisateur sur le nœud de hello. toodo, vous pouvez utiliser le portail Azure, de hello [ajouter un nœud tooa du compte utilisateur] [ rest_create_user] hello API REST de traitement par lots, d’appeler hello [ComputeNode.CreateComputeNodeUser] [ net_create_user] méthode en lot .NET ou appel hello [ajouter un utilisateur] [ py_add_user] méthode dans le module de traitement par lots Python hello.
>
>

### <a name="troubleshooting-problematic-compute-nodes"></a>Résolution des problèmes liés aux nœuds de calcul
Dans les cas où certaines tâches échouent, votre application cliente de lot ou d’un service peut examiner des métadonnées de hello de hello échoué des tâches tooidentify un nœud d’un dysfonctionnement. Chaque nœud dans un pool est donnée à un ID unique, et nœud hello sur lequel s’exécute une tâche est inclus dans les métadonnées de tâche hello. Une fois que vous avez identifié le nœud présentant un problème, vous pouvez effectuer les actions suivantes :

* **Redémarrer le nœud de hello** ([reste][rest_reboot] | [.NET][net_reboot])

    Nœud de hello redémarrage peut parfois effacer latentes problèmes tels que les processus bloqués ou bloqués. Notez que si votre pool utilise une tâche de démarrage ou de votre projet utilise une tâche de préparation du projet, elles sont exécutées lorsque le nœud de hello redémarre.
* **Créer une nouvelle image de nœud de hello** ([reste][rest_reimage] | [.NET][net_reimage])

    Cela réinstalle le système d’exploitation de hello sur le nœud de hello. Comme avec un nœud en cours de redémarrage, démarrer des tâches et les tâches de préparation de travail sont réexécutés après que le nœud de hello a été réinitialisée.
* **Supprimer un nœud de hello à partir du pool de hello** ([reste][rest_remove] | [.NET][net_remove])

    Il est parfois nécessaire toocompletely supprimer un nœud à partir du pool de hello hello.
* **Désactiver la planification des tâches sur le nœud de hello** ([reste][rest_offline] | [.NET][net_offline])

    Cela efficacement prend hello nœud hors connexion afin qu’aucune autre tâche assignés tooit, mais permet l’exécution de tooremain hello nœud et dans le pool de hello. Ainsi, vous tooperform une analyse approfondie à cause de hello d’échecs de hello sans perte de données de la tâche ayant échoué hello et sans nœud hello à l’origine des échecs des tâches supplémentaires. Par exemple, vous pouvez désactiver la planification des tâches sur le nœud de hello, puis [se connecter à distance](#connecting-to-compute-nodes) tooexamine hello des journaux des événements du nœud ou autres résolution des problèmes. Une fois que vous avez terminé votre examen, vous remettez en ligne les nœud hello en activant la planification des tâches ([reste][rest_online] | [.NET] [ net_online]), ou un des hello effectuer d’autres actions abordées précédemment.

> [!IMPORTANT]
> Avec chaque action qui est décrite dans cette section--redémarrer, réinitialisation, supprimer et désactiver la planification des tâches--vous êtes en mesure de toospecify comment sont gérées les tâches en cours d’exécution sur le nœud de hello lorsque vous exécutez hello action. Par exemple, lorsque vous désactivez planification des tâches sur un nœud à l’aide de la bibliothèque cliente .NET de la lot hello, vous pouvez spécifier un [DisableComputeNodeSchedulingOption] [ net_offline_option] toospecify valeur d’énumération si trop**Terminate** en cours d’exécution des tâches, **replacez** pour la planification sur d’autres nœuds, ou autoriser toocomplete de tâches en cours d’exécution avant d’effectuer l’action de hello (**TaskCompletion**).
>
>

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur hello [outils et API de lot](batch-apis-tools.md) disponibles pour la création de solutions de traitement par lots.
* Parcourir une application de traitement par lots exemple étape par étape, [prise en main hello bibliothèque Azure Batch pour .NET](batch-dotnet-get-started.md). Il existe également un [version Python](batch-python-tutorial.md) de didacticiel hello qui exécute une charge de travail sur Linux des nœuds de calcul.
* Télécharger et générer hello [lot Explorer] [ github_batchexplorer] exemple de projet pour une utilisation lors du développement de vos solutions de traitement par lots. Hello Explorer de lot, vous pouvez d’effectuer hello suivante et bien plus encore :

  * Analysez et manipulez les pools, les travaux et les tâches au sein de votre compte Batch
  * Téléchargez `stdout.txt`, `stderr.txt` et d’autres fichiers à partir des nœuds
  * Créez des utilisateurs sur les nœuds et téléchargez les fichiers RDP pour la connexion à distance
* Découvrez comment trop[créer des pools de nœuds de calcul Linux](batch-linux-nodes.md).
* Visitez hello [forum d’Azure Batch] [ batch_forum] sur MSDN. forum de Hello est une bonne placer tooask questions, si vous apprenez simplement ou que vous êtes un expert dans à l’aide du traitement par lots.

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
