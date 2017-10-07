---
title: aaaGet main de PowerShell pour Azure Batch | Documents Microsoft
description: "Une brève introduction toohello applets de commande PowerShell de Azure vous pouvez utiliser les ressources de traitement par lots toomanage."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: f9ad62c5-27bf-4e6b-a5bf-c5f5914e6199
ms.service: batch
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: powershell
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3e4d12e9c1e52a5b2db2dd44346edda93b7ef92b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-resources-with-powershell-cmdlets"></a>Gérer les ressources Batch avec les applets de commande PowerShell

Avec hello applets de commande PowerShell de traitement par lots Azure, vous pouvez effectuer et script nombreux hello mêmes tâches mener avec hello API de lot, hello portail Azure et hello Azure Interface de ligne de commande (CLI). Il s’agit d’un applets de commande brève introduction toohello, vous pouvez utiliser toomanage vos comptes de lot et travailler avec vos ressources de traitement par lots telles que les pools, les travaux et les tâches.

Pour obtenir une liste complète des applets de commande de lot et la syntaxe de l’applet de commande détaillées, consultez hello [référence d’applet de commande Azure Batch](/powershell/module/azurerm.batch/#batch).

Cet article est basé sur les applets de commande d’Azure PowerShell version 3.0.0. Nous recommandons de mettre votre Azure PowerShell fréquemment tootake parti du service mises à jour et améliorations.

## <a name="prerequisites"></a>Composants requis
Effectuer hello suivant operations toouse Azure PowerShell toomanage vos ressources de traitement par lots.

* [Installation et configuration d'Azure PowerShell](/powershell/azure/overview)
* Exécutez hello **AzureRmAccount de connexion** applet de commande tooconnect tooyour abonnement (hello ship applets de commande de traitement par lots Azure dans le module du Gestionnaire de ressources Azure hello) :
  
    `Login-AzureRmAccount`
* **Inscrire auprès d’espace de noms hello lot fournisseur**. Cette opération ne doit toobe effectuée **une fois par abonnement**.
  
    `Register-AzureRMResourceProvider -ProviderNamespace Microsoft.Batch`

## <a name="manage-batch-accounts-and-keys"></a>Gestion des clés et des comptes Batch
### <a name="create-a-batch-account"></a>Création d’un compte Batch
**New-AzureBatchAccount** crée un compte Batch dans un groupe de ressources spécifié. Si vous n’avez pas déjà un groupe de ressources, créez-le en exécutant hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) applet de commande. Spécifiez l’une des hello Azure régions Bonjour **emplacement** paramètre, comme « Centre des États-Unis ». Par exemple :

    New-AzureRmResourceGroup –Name MyBatchResourceGroup –location "Central US"

Ensuite, créez un compte de traitement par lots dans le groupe de ressources hello, en spécifiant un nom de compte hello dans <*account_name*> hello emplacement et au nom de votre groupe de ressources. Création du compte Batch hello peut prendre quelques toocomplete de temps. Par exemple :

    New-AzureRmBatchAccount –AccountName <account_name> –Location "Central US" –ResourceGroupName <res_group_name>

> [!NOTE]
> compte de traitement par lots Hello nom doit être unique toohello région Azure pour le groupe de ressources hello, contenir entre 3 et 24 caractères et utiliser des lettres minuscules et chiffres uniquement.
> 
> 

### <a name="get-account-access-keys"></a>Obtenir les clés d'accès au compte
**Get-AzureRmBatchAccountKeys** affiche hello les clés d’accès associés à un compte Azure Batch. Par exemple, exécutez hello suivant tooget hello principal et secondaire les clés du compte hello créé.

    $Account = Get-AzureRmBatchAccountKeys –AccountName <account_name>

    $Account.PrimaryAccountKey

    $Account.SecondaryAccountKey

### <a name="generate-a-new-access-key"></a>Générer une nouvelle clé d'accès
**New-AzureRmBatchAccountKey** génère une nouvelle clé de compte primaire ou secondaire pour un compte Azure Batch. Par exemple, toogenerate une nouvelle clé primaire pour votre compte Batch, tapez :

    New-AzureRmBatchAccountKey -AccountName <account_name> -KeyType Primary

> [!NOTE]
> toogenerate une nouvelle clé secondaire, spécifiez « Base de données secondaire » pour hello **KeyType** paramètre. Vous avez des clés primaires et secondaires du hello tooregenerate séparément.
> 
> 

### <a name="delete-a-batch-account"></a>Suppression d’un compte Batch
**Remove-AzureRmBatchAccount** supprime un compte Batch. Par exemple :

    Remove-AzureRmBatchAccount -AccountName <account_name>

Lorsque vous y êtes invité, confirmez que tooremove hello compte. La suppression du compte peut prendre quelques toocomplete de temps.

## <a name="create-a-batchaccountcontext-object"></a>Créer un objet BatchAccountContext
à l’aide de tooauthenticate hello les applets de commande PowerShell de lot lorsque vous créez et gérez des pools de lot, travaux, tâches, et d’autres ressources, d’abord créer un toostore d’objet BatchAccountContext votre nom de compte et les clés :

    $context = Get-AzureRmBatchAccountKeys -AccountName <account_name>

Vous passez l’objet de BatchAccountContext de hello dans les applets de commande que hello utilisation **BatchContext** paramètre.

> [!NOTE]
> Par défaut, les clé primaire du compte hello sont utilisé pour l’authentification, mais vous pouvez sélectionner explicitement les toouse clé hello en modifiant l’objet BatchAccountContext **KeyInUse** propriété : `$context.KeyInUse = "Secondary"`.
> 
> 

## <a name="create-and-modify-batch-resources"></a>Créer et modifier les ressources Batch
Utilisez les applets de commande telles que **New-AzureBatchPool**, **New-AzureBatchJob**, et **New-AzureBatchTask** ressources toocreate sous un compte de traitement par lots. Des correspondants **Get -** et **Set -** propriétés de hello tooupdate applets de commande de ressources existants, et **Remove -** applets de commande des ressources de tooremove sous un compte de traitement par lots.

Lorsque vous utilisez la plupart de ces applets de commande dans Ajout toopassing un objet BatchContext, vous devez toocreate ou passez les objets qui contiennent des paramètres de ressource détaillées, comme illustré dans hello l’exemple suivant. Consultez hello détaillées aide pour chaque applet de commande pour obtenir des exemples supplémentaires.

### <a name="create-a-batch-pool"></a>Créer un pool Batch
Lors de la création ou de mise à jour d’un pool de traitement par lots, sélectionnez configuration du service cloud hello ou configuration d’ordinateur virtuel hello pour hello système d’exploitation sur hello nœuds de calcul (consultez [vue d’ensemble de lot](batch-api-basics.md#pool)). Si vous spécifiez la configuration du service cloud hello, vos nœuds de calcul sont une image avec l’un des hello [mises à jour de système d’exploitation invité de Azure](../cloud-services/cloud-services-guestos-update-matrix.md#releases). Si vous spécifiez la configuration d’ordinateur virtuel hello, vous pouvez spécifier un Hello pris en charge de Linux ou hello répertorié dans l’image de machine virtuelle Windows [Azure Marketplace de Machines virtuelles][vm_marketplace], ou fournissez un personnalisé image que vous avez préparé.

Lorsque vous exécutez **New-AzureBatchPool**, passer des paramètres de système d’exploitation hello dans un objet PSCloudServiceConfiguration ou PSVirtualMachineConfiguration. Par exemple, hello applet de commande suivante crée un nouveau pool de traitement par lots avec les nœuds de calcul de petite taille dans la configuration du service cloud hello, une image avec la dernière version de système d’exploitation hello de famille 3 (Windows Server 2012). Ici, hello **CloudServiceConfiguration** paramètre spécifie hello *$configuration* variable en tant qu’objet PSCloudServiceConfiguration hello. Hello **BatchContext** paramètre spécifie une variable précédemment définie *$context* en tant qu’objet BatchAccountContext hello.

    $configuration = New-Object -TypeName "Microsoft.Azure.Commands.Batch.Models.PSCloudServiceConfiguration" -ArgumentList @(4,"*")

    New-AzureBatchPool -Id "AutoScalePool" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -AutoScaleFormula '$TargetDedicated=4;' -BatchContext $context

nombre de cible de Hello de nœuds de calcul dans un nouveau pool de hello est déterminé par une formule de l’échelle automatique. Dans ce cas, la formule de hello est simplement **$TargetDedicated = 4**, indiquant le nombre de hello de nœuds de calcul dans le pool de hello est au maximum de 4.

## <a name="query-for-pools-jobs-tasks-and-other-details"></a>Requête relative aux pools, aux travaux, aux tâches et autres détails
Utilisez les applets de commande telles que **Get-AzureBatchPool**, **Get-AzureBatchJob**, et **Get-AzureBatchTask** tooquery pour les entités créées sous un compte Batch.

### <a name="query-for-data"></a>Interrogation des données
Par exemple, utilisez **Get-AzureBatchPools** toofind vos pools. Par défaut il interroge pour tous les pools sous votre compte, en supposant que vous déjà stockée objet hello BatchAccountContext *$context*:

    Get-AzureBatchPool -BatchContext $context

### <a name="use-an-odata-filter"></a>Utilisation d’un filtre OData
Vous pouvez fournir un filtre OData à l’aide de hello **filtre** paramètre toofind hello uniquement les objets qui vous intéressent. Par exemple, vous pouvez rechercher tous les pools dont l’identificateur commence par « myPool » :

    $filter = "startswith(id,'myPool')"

    Get-AzureBatchPool -Filter $filter -BatchContext $context

Cette méthode n'est pas aussi flexible que l'utilisation de « Where-Object » dans un pipeline local. Toutefois, les requêtes hello sont envoyées toohello service Batch directement afin que tout le filtrage se produit côté serveur de hello, l’enregistrement de la bande passante Internet.

### <a name="use-hello-id-parameter"></a>Utilisez le paramètre d’Id hello
Un filtre d’OData autre tooan est toouse hello **Id** paramètre. tooquery pour un pool spécifique avec l’id « monpool » :

    Get-AzureBatchPool -Id "myPool" -BatchContext $context

Hello **Id** paramètre prend en charge uniquement intégral-id recherche, pas les caractères génériques ou les filtres OData-style.

### <a name="use-hello-maxcount-parameter"></a>Utilisez le paramètre MaxCount de hello
Par défaut, chaque applet de commande retourne un maximum de 1 000 objets. Si vous atteignez cette limite, affinez votre toobring filtre précédent moins d’objets, ou définir explicitement la valeur maximale à l’aide de hello **MaxCount** paramètre. Par exemple :

    Get-AzureBatchTask -MaxCount 2500 -BatchContext $context

limite supérieure de hello tooremove, définissez **MaxCount** too0 ou moins.

### <a name="use-hello-powershell-pipeline"></a>Utiliser le pipeline de PowerShell hello
Applets de commande de traitement par lots peut tirer parti des données de toosend hello PowerShell pipeline entre applets de commande. Cela a hello même effet que la spécification d’un paramètre, mais facilite l’utilisation avec plusieurs entités plus facile.

Par exemple, recherchez et affichez toutes les tâches sous votre compte :

    Get-AzureBatchJob -BatchContext $context | Get-AzureBatchTask -BatchContext $context

Redémarrez chaque nœud de calcul dans un pool :

    Get-AzureBatchComputeNode -PoolId "myPool" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

## <a name="application-package-management"></a>Gestion des packages d’application
Les packages d’applications permettent simplifié toodeploy applications toohello nœuds de calcul dans les pools. Avec hello applets de commande PowerShell de lot, vous pouvez télécharger et gérer des packages d’application dans votre compte Batch et déployer des nœuds de toocompute de versions de package.

**Créez** une application :

    New-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

**Ajoutez** un package d’application :

    New-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0" -Format zip -FilePath package001.zip

Ensemble hello **version par défaut** pour l’application hello :

    Set-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -DefaultVersion "1.0"

**Répertorier** les packages d’une application

    $application = Get-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

    $application.ApplicationPackages

**Supprimer** un package d’application

    Remove-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0"

**Supprimer** une application

    Remove-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

> [!NOTE]
> Vous devez supprimer toutes les versions de package d’application d’une application avant de supprimer application hello. Vous recevez une erreur « Conflit » si vous essayez de toodelete une application qui possède actuellement des packages d’applications.
> 
> 

### <a name="deploy-an-application-package"></a>Déployer un package d’application
Vous pouvez spécifier un ou plusieurs packages d’application pour le déploiement lorsque vous créez un pool. Lorsque vous spécifiez un package au moment de la création du pool, il est déployé tooeach nœud en tant que pool de jointures de nœud hello. Les packages sont également déployés lorsqu’un nœud est redémarré ou réinitialisé.

Spécifiez hello `-ApplicationPackageReference` option lors de la création des nœuds d’un package toohello du pool d’applications un toodeploy pool dès qu’ils rejoignent le pool de hello. Commencez par créer un **PSApplicationPackageReference** de l’objet et configurez-le avec hello Id et le package de version de l’application vous souhaitez que les nœuds de calcul du pool toodeploy toohello :

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "1.0"

Maintenant créer le pool de hello et spécifiez l’objet de référence de package hello comme hello argument toohello `ApplicationPackageReferences` option :

    New-AzureBatchPool -Id "PoolWithAppPackage" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -BatchContext $context -ApplicationPackageReferences $appPackageReference

Vous trouverez plus d’informations sur les packages d’applications dans [déployer des nœuds de toocompute d’applications avec des packages d’application de lot](batch-application-packages.md).

> [!IMPORTANT]
> Vous devez [lier un compte de stockage Azure](#linked-storage-account-autostorage) tooyour lot compte toouse des packages d’applications.
> 
> 

### <a name="update-a-pools-application-packages"></a>Mise à jour des packages d’applications d’un pool
les applications de hello tooupdate affectées tooan pool existant, d’abord créer un objet PSApplicationPackageReference avec les propriétés de hello souhaitée (version Id et le package d’application) :

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "2.0"

Ensuite, obtenir le pool de hello de lot, effacer tout package existant, ajoutez notre nouvelle référence de package et mettre à jour le service de traitement par lots hello avec de nouveaux paramètres de pool hello :

    $pool = Get-AzureBatchPool -BatchContext $context -Id "PoolWithAppPackage"

    $pool.ApplicationPackageReferences.Clear()

    $pool.ApplicationPackageReferences.Add($appPackageReference)

    Set-AzureBatchPool -BatchContext $context -Pool $pool

Vous avez maintenant mis à jour les propriétés du pool hello dans le service de traitement par lots hello. tooactually déployer hello nouveau package toocompute nœuds d’application dans le pool de hello, toutefois, vous devez redémarrer ou réinitialiser ces nœuds. Vous pouvez redémarrer tous les nœuds dans un pool avec la commande suivante :

    Get-AzureBatchComputeNode -PoolId "PoolWithAppPackage" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

> [!TIP]
> Vous pouvez déployer plusieurs applications packages toohello nœuds de calcul un pool. Si vous souhaitez que trop*ajouter* un package d’application au lieu de remplacer les packages hello actuellement déployé, omettez hello `$pool.ApplicationPackageReferences.Clear()` ligne ci-dessus.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
* Pour connaître la syntaxe détaillée des applets de commande et obtenir des exemples, consultez les [informations de référence sur les applets de commande Azure Batch](/powershell/module/azurerm.batch/#batch).
* Pour plus d’informations sur les applications et packages d’applications de traitement par lots, consultez [déployer des nœuds de toocompute d’applications avec des packages d’application de lot](batch-application-packages.md).

[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/