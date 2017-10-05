---
title: "Résolution des problèmes liés à Azure Data Factory"
description: "Découvrez comment résoudre les problèmes liés à l'utilisation de Azure Data Factory."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 38fd14c1-5bb7-4eef-a9f5-b289ff9a6942
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: spelluru
ms.openlocfilehash: 953a2703db7c8991f580a7c963d6cbd94265c213
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-data-factory-issues"></a><span data-ttu-id="b07f6-103">Résolution des problèmes liés à Data Factory</span><span class="sxs-lookup"><span data-stu-id="b07f6-103">Troubleshoot Data Factory issues</span></span>
<span data-ttu-id="b07f6-104">Cet article propose des conseils pour la résolution des problèmes d'utilisation d'Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b07f6-104">This article provides troubleshooting tips for issues when using Azure Data Factory.</span></span> <span data-ttu-id="b07f6-105">Cet article ne répertorie pas tous les problèmes possibles lors de l'utilisation du service, mais il aborde certains problèmes ainsi que des conseils de résolution généraux.</span><span class="sxs-lookup"><span data-stu-id="b07f6-105">This article does not list all the possible issues when using the service, but it covers some issues and general troubleshooting tips.</span></span>   

## <a name="troubleshooting-tips"></a><span data-ttu-id="b07f6-106">Conseils de dépannage</span><span class="sxs-lookup"><span data-stu-id="b07f6-106">Troubleshooting tips</span></span>
### <a name="error-the-subscription-is-not-registered-to-use-namespace-microsoftdatafactory"></a><span data-ttu-id="b07f6-107">Erreur : The subscription is not registered to use namespace ’Microsoft.DataFactory’ (L'abonnement n'est pas enregistré pour utiliser l'espace de noms « Microsoft.DataFactory »)</span><span class="sxs-lookup"><span data-stu-id="b07f6-107">Error: The subscription is not registered to use namespace 'Microsoft.DataFactory'</span></span>
<span data-ttu-id="b07f6-108">Si vous recevez cette erreur, cela signifie que le fournisseur de ressources Azure Data Factory n'a pas été enregistré sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="b07f6-108">If you receive this error, the Azure Data Factory resource provider has not been registered on your machine.</span></span> <span data-ttu-id="b07f6-109">Effectuez les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="b07f6-109">Do the following:</span></span>

1. <span data-ttu-id="b07f6-110">Lancez Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b07f6-110">Launch Azure PowerShell.</span></span>
2. <span data-ttu-id="b07f6-111">Connectez-vous à votre compte Azure à l’aide de la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="b07f6-111">Log in to your Azure account using the following command.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="b07f6-112">Exécutez la commande suivante pour enregistrer le fournisseur Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b07f6-112">Run the following command to register the Azure Data Factory provider.</span></span>

    ```powershell        
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

### <a name="problem-unauthorized-error-when-running-a-data-factory-cmdlet"></a><span data-ttu-id="b07f6-113">Problème : erreur non autorisée lors de l’exécution d’une applet de commande Data Factory</span><span class="sxs-lookup"><span data-stu-id="b07f6-113">Problem: Unauthorized error when running a Data Factory cmdlet</span></span>
<span data-ttu-id="b07f6-114">Vous n’utilisez probablement pas le compte ou l’abonnement Azure correct pour Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b07f6-114">You are probably not using the right Azure account or subscription with the Azure PowerShell.</span></span> <span data-ttu-id="b07f6-115">Utilisez les applets de commande suivantes pour sélectionner le compte et l’abonnement Azure corrects à utiliser avec Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b07f6-115">Use the following cmdlets to select the right Azure account and subscription to use with the Azure PowerShell.</span></span>

1. <span data-ttu-id="b07f6-116">Login-AzureRmAccount - Utilisez l’ID d’utilisateur et le mot de passe corrects.</span><span class="sxs-lookup"><span data-stu-id="b07f6-116">Login-AzureRmAccount - Use the right user ID and password</span></span>
2. <span data-ttu-id="b07f6-117">Get-AzureRmSubscription : affichez tous les abonnements du compte.</span><span class="sxs-lookup"><span data-stu-id="b07f6-117">Get-AzureRmSubscription - View all the subscriptions for the account.</span></span>
3. <span data-ttu-id="b07f6-118">Select-AzureRmSubscription &lt;nom de l’abonnement&gt; - Sélectionnez l’abonnement correct.</span><span class="sxs-lookup"><span data-stu-id="b07f6-118">Select-AzureRmSubscription &lt;subscription name&gt; - Select the right subscription.</span></span> <span data-ttu-id="b07f6-119">Utilisez le même que celui que vous utilisez pour créer une fabrique de données sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b07f6-119">Use the same one you use to create a data factory on the Azure portal.</span></span>

### <a name="problem-fail-to-launch-data-management-gateway-express-setup-from-azure-portal"></a><span data-ttu-id="b07f6-120">Problème : échec du lancement de l’installation rapide de la passerelle de gestion des données à partir du portail Azure</span><span class="sxs-lookup"><span data-stu-id="b07f6-120">Problem: Fail to launch Data Management Gateway Express Setup from Azure portal</span></span>
<span data-ttu-id="b07f6-121">L’installation rapide de la passerelle de gestion des données nécessite Internet Explorer ou un navigateur web compatible avec Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="b07f6-121">The Express setup for the Data Management Gateway requires Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span> <span data-ttu-id="b07f6-122">Si le programme d'installation rapide ne démarre pas, effectuez l'une des opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="b07f6-122">If the Express Setup fails to start, do one of the following:</span></span>

* <span data-ttu-id="b07f6-123">Utilisez Internet Explorer ou un navigateur web compatible Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="b07f6-123">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>

    <span data-ttu-id="b07f6-124">Si vous utilisez Chrome, accédez au [Chrome Web Store](https://chrome.google.com/webstore/), faites une recherche sur le mot-clé « ClickOnce », choisissez l’une des extensions ClickOnce, puis installez-la.</span><span class="sxs-lookup"><span data-stu-id="b07f6-124">If you are using Chrome, go to the [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>

    <span data-ttu-id="b07f6-125">Faites de même pour Firefox (installez un complément).</span><span class="sxs-lookup"><span data-stu-id="b07f6-125">Do the same for Firefox (install add-in).</span></span> <span data-ttu-id="b07f6-126">Cliquez sur le bouton du menu dans la barre d’outils (trois lignes horizontales en haut à droite), cliquez sur Modules complémentaires, effectuez une recherche avec le mot-clé « ClickOnce », choisissez l’une des extensions de ClickOnce et installez le programme.</span><span class="sxs-lookup"><span data-stu-id="b07f6-126">Click Open Menu button on the toolbar (three horizontal lines in the top-right corner), click Add-ons, search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>
* <span data-ttu-id="b07f6-127">Utilisez le lien **Configuration manuelle** qui s’affiche dans le même panneau sur le portail.</span><span class="sxs-lookup"><span data-stu-id="b07f6-127">Use the **Manual Setup** link shown on the same blade in the portal.</span></span> <span data-ttu-id="b07f6-128">Cette approche vous permet de télécharger le fichier d’installation et de l’exécuter manuellement.</span><span class="sxs-lookup"><span data-stu-id="b07f6-128">You use this approach to download installation file and run it manually.</span></span> <span data-ttu-id="b07f6-129">Une fois l'installation effectuée, vous verrez s’afficher la boîte de dialogue Configuration de la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="b07f6-129">After the installation is successful, you see the Data Management Gateway Configuration dialog box.</span></span> <span data-ttu-id="b07f6-130">Copiez la **clé** sur l’écran du portail et utilisez-la dans le gestionnaire de configuration pour enregistrer manuellement la passerelle auprès du service.</span><span class="sxs-lookup"><span data-stu-id="b07f6-130">Copy the **key** from the portal screen and use it in the configuration manager to manually register the gateway with the service.</span></span>  

### <a name="problem-fail-to-connect-to-on-premises-sql-server"></a><span data-ttu-id="b07f6-131">Problème : échec de la connexion à un serveur SQL local</span><span class="sxs-lookup"><span data-stu-id="b07f6-131">Problem: Fail to connect to on-premises SQL Server</span></span>
<span data-ttu-id="b07f6-132">Lancez le **Gestionnaire de configuration de la passerelle de gestion des données** sur l’ordinateur passerelle et utilisez l’onglet **Résolution des problèmes** pour tester la connexion à SQL Server à partir de l’ordinateur passerelle.</span><span class="sxs-lookup"><span data-stu-id="b07f6-132">Launch **Data Management Gateway Configuration Manager** on the gateway machine and use the **Troubleshooting** tab to test the connection to SQL Server from the gateway machine.</span></span> <span data-ttu-id="b07f6-133">Consultez [Résolution des problèmes de passerelle](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) pour obtenir des conseils sur la résolution des problèmes de connexion/passerelle.</span><span class="sxs-lookup"><span data-stu-id="b07f6-133">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>   

### <a name="problem-input-slices-are-in-waiting-state-for-ever"></a><span data-ttu-id="b07f6-134">Problème : l’état des tranches d’entrée est En attente depuis longtemps</span><span class="sxs-lookup"><span data-stu-id="b07f6-134">Problem: Input slices are in Waiting state for ever</span></span>
<span data-ttu-id="b07f6-135">Les tranches peuvent avoir l’état **En attente** pour diverses raisons.</span><span class="sxs-lookup"><span data-stu-id="b07f6-135">The slices could be in **Waiting** state due to various reasons.</span></span> <span data-ttu-id="b07f6-136">Une des raisons courantes est que la propriété **external** n’est pas définie sur **true**.</span><span class="sxs-lookup"><span data-stu-id="b07f6-136">One of the common reasons is that the **external** property is not set to **true**.</span></span> <span data-ttu-id="b07f6-137">Tout jeu de données généré en dehors de l’étendue d’Azure Data Factory doit être marqué avec la propriété **external** .</span><span class="sxs-lookup"><span data-stu-id="b07f6-137">Any dataset that is produced outside the scope of Azure Data Factory should be marked with **external** property.</span></span> <span data-ttu-id="b07f6-138">Cette propriété indique que les données sont externes et qu’elles ne sont prises en charge par aucun pipeline dans la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="b07f6-138">This property indicates that the data is external and not backed by any pipelines within the data factory.</span></span> <span data-ttu-id="b07f6-139">Les tranches de données sont marquées comme prêtes ( **Ready** ) une fois que les données sont disponibles dans le magasin respectif.</span><span class="sxs-lookup"><span data-stu-id="b07f6-139">The data slices are marked as **Ready** once the data is available in the respective store.</span></span>

<span data-ttu-id="b07f6-140">Consultez l’exemple suivant pour l’utilisation de la propriété **external** .</span><span class="sxs-lookup"><span data-stu-id="b07f6-140">See the following example for the usage of the **external** property.</span></span> <span data-ttu-id="b07f6-141">Vous pouvez éventuellement spécifier **externalData*** quand vous affectez à la propriété external la valeur true.</span><span class="sxs-lookup"><span data-stu-id="b07f6-141">You can optionally specify **externalData*** when you set external to true.</span></span>

<span data-ttu-id="b07f6-142">Consultez l’article [Jeux de données](data-factory-create-datasets.md) pour plus d’informations sur cette propriété.</span><span class="sxs-lookup"><span data-stu-id="b07f6-142">See [Datasets](data-factory-create-datasets.md) article for more details about this property.</span></span>

```json
{
  "name": "CustomerTable",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "MyLinkedService",
    "typeProperties": {
      "folderPath": "MyContainer/MySubFolder/",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      }
    }
  }
}
```

<span data-ttu-id="b07f6-143">Pour résoudre l’erreur, ajoutez la propriété **external** et la section **externalData** facultative à la définition JSON de la table d’entrée, puis recréez la table.</span><span class="sxs-lookup"><span data-stu-id="b07f6-143">To resolve the error, add the **external** property and the optional **externalData** section to the JSON definition of the input table and recreate the table.</span></span>

### <a name="problem-hybrid-copy-operation-fails"></a><span data-ttu-id="b07f6-144">Problème : échec de l’opération de copie hybride</span><span class="sxs-lookup"><span data-stu-id="b07f6-144">Problem: Hybrid copy operation fails</span></span>
<span data-ttu-id="b07f6-145">Consultez la page [Résolution des problèmes de passerelle](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) pour savoir comment résoudre les problèmes de copie depuis/vers un magasin de données local avec la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="b07f6-145">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for steps to troubleshoot issues with copying to/from an on-premises data store using the Data Management Gateway.</span></span>

### <a name="problem-on-demand-hdinsight-provisioning-fails"></a><span data-ttu-id="b07f6-146">Problème : échec de l’approvisionnement HDInsight à la demande</span><span class="sxs-lookup"><span data-stu-id="b07f6-146">Problem: On-demand HDInsight provisioning fails</span></span>
<span data-ttu-id="b07f6-147">Lorsque vous utilisez un service lié de type HDInsightOnDemand, vous devez spécifier un linkedServiceName qui pointe vers un stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="b07f6-147">When using a linked service of type HDInsightOnDemand, you need to specify a linkedServiceName that points to an Azure Blob Storage.</span></span> <span data-ttu-id="b07f6-148">Le service Data Factory utilise ce stockage pour stocker les journaux et les fichiers d’accompagnement pour votre cluster HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="b07f6-148">Data Factory service uses this storage to store logs and supporting files for your on-demand HDInsight cluster.</span></span>  <span data-ttu-id="b07f6-149">Parfois, l’approvisionnement d'un cluster HDInsight à la demande échoue avec l'erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="b07f6-149">Sometimes provisioning of an on-demand HDInsight cluster fails with the following error:</span></span>

```
Failed to create cluster. Exception: Unable to complete the cluster create operation. Operation failed with code '400'. Cluster left behind state: 'Error'. Message: 'StorageAccountNotColocated'.
```

<span data-ttu-id="b07f6-150">Cette erreur indique généralement que l’emplacement du compte de stockage spécifié dans linkedServiceName ne se trouve pas dans l’emplacement de centre de données dans lequel l’approvisionnement de HDInsight est effectué.</span><span class="sxs-lookup"><span data-stu-id="b07f6-150">This error usually indicates that the location of the storage account specified in the linkedServiceName is not in the same data center location where the HDInsight provisioning is happening.</span></span> <span data-ttu-id="b07f6-151">Exemple : si votre fabrique de données se trouve dans l’ouest des États-Unis et que le stockage Azure est dans l’est des États-Unis, l’approvisionnement à la demande échoue dans l’ouest des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="b07f6-151">Example: if your data factory is in West US and the Azure storage is in East US, the on-demand provisioning fails in West US.</span></span>

<span data-ttu-id="b07f6-152">En outre, il existe une seconde propriété JSON additionalLinkedServiceNames avec laquelle les comptes de stockage supplémentaires peuvent être spécifiés dans HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="b07f6-152">Additionally, there is a second JSON property additionalLinkedServiceNames where additional storage accounts may be specified in on-demand HDInsight.</span></span> <span data-ttu-id="b07f6-153">Ces comptes de stockage supplémentaires liés doivent avoir le même emplacement que le cluster HDInsight, ou l’approvisionnement échoue avec la même erreur.</span><span class="sxs-lookup"><span data-stu-id="b07f6-153">Those additional linked storage accounts should be in the same location as the HDInsight cluster, or it fails with the same error.</span></span>

### <a name="problem-custom-net-activity-fails"></a><span data-ttu-id="b07f6-154">Problème : échec de l’activité .NET personnalisée</span><span class="sxs-lookup"><span data-stu-id="b07f6-154">Problem: Custom .NET activity fails</span></span>
<span data-ttu-id="b07f6-155">Consultez la page [Déboguer un pipeline avec une activité personnalisée](data-factory-use-custom-activities.md#troubleshoot-failures) pour obtenir des instructions détaillées.</span><span class="sxs-lookup"><span data-stu-id="b07f6-155">See [Debug a pipeline with custom activity](data-factory-use-custom-activities.md#troubleshoot-failures) for detailed steps.</span></span>

## <a name="use-azure-portal-to-troubleshoot"></a><span data-ttu-id="b07f6-156">Utilisation du portail Azure pour résoudre les problèmes</span><span class="sxs-lookup"><span data-stu-id="b07f6-156">Use Azure portal to troubleshoot</span></span>
### <a name="using-portal-blades"></a><span data-ttu-id="b07f6-157">Utilisation des panneaux du portail</span><span class="sxs-lookup"><span data-stu-id="b07f6-157">Using portal blades</span></span>
<span data-ttu-id="b07f6-158">Consultez la page [Surveiller le pipeline](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) pour obtenir la procédure.</span><span class="sxs-lookup"><span data-stu-id="b07f6-158">See [Monitor pipeline](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) for steps.</span></span>

### <a name="using-monitor-and-manage-app"></a><span data-ttu-id="b07f6-159">Utilisation de l’application Surveillance et gestion</span><span class="sxs-lookup"><span data-stu-id="b07f6-159">Using Monitor and Manage App</span></span>
<span data-ttu-id="b07f6-160">Consultez [Surveiller et gérer les pipelines Data Factory à l’aide de l’application Surveillance et gestion](data-factory-monitor-manage-app.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="b07f6-160">See [Monitor and manage data factory pipelines using Monitor and Manage App](data-factory-monitor-manage-app.md) for details.</span></span>

## <a name="use-azure-powershell-to-troubleshoot"></a><span data-ttu-id="b07f6-161">Utiliser Azure PowerShell pour résoudre les problèmes</span><span class="sxs-lookup"><span data-stu-id="b07f6-161">Use Azure PowerShell to troubleshoot</span></span>
### <a name="use-azure-powershell-to-troubleshoot-an-error"></a><span data-ttu-id="b07f6-162">Utiliser Azure PowerShell pour résoudre une erreur</span><span class="sxs-lookup"><span data-stu-id="b07f6-162">Use Azure PowerShell to troubleshoot an error</span></span>
<span data-ttu-id="b07f6-163">Consultez la page [Surveiller les pipelines Data Factory à l’aide d’Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="b07f6-163">See [Monitor Data Factory pipelines using Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) for details.</span></span>

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456
[json-scripting-reference]: http://go.microsoft.com/fwlink/?LinkId=516971

[azure-portal]: https://portal.azure.com/

[image-data-factory-troubleshoot-with-error-link]: ./media/data-factory-troubleshoot/DataFactoryWithErrorLink.png

[image-data-factory-troubleshoot-datasets-with-errors-blade]: ./media/data-factory-troubleshoot/DatasetsWithErrorsBlade.png

[image-data-factory-troubleshoot-table-blade-with-problem-slices]: ./media/data-factory-troubleshoot/TableBladeWithProblemSlices.png

[image-data-factory-troubleshoot-activity-run-with-error]: ./media/data-factory-troubleshoot/ActivityRunDetailsWithError.png

[image-data-factory-troubleshoot-dataslice-blade-with-active-runs]: ./media/data-factory-troubleshoot/DataSliceBladeWithActivityRuns.png

[image-data-factory-troubleshoot-walkthrough2-with-errors-link]: ./media/data-factory-troubleshoot/Walkthrough2WithErrorsLink.png

[image-data-factory-troubleshoot-walkthrough2-datasets-with-errors]: ./media/data-factory-troubleshoot/Walkthrough2DataSetsWithErrors.png

[image-data-factory-troubleshoot-walkthrough2-table-with-problem-slices]: ./media/data-factory-troubleshoot/Walkthrough2TableProblemSlices.png

[image-data-factory-troubleshoot-walkthrough2-slice-activity-runs]: ./media/data-factory-troubleshoot/Walkthrough2DataSliceActivityRuns.png

[image-data-factory-troubleshoot-activity-run-details]: ./media/data-factory-troubleshoot/Walkthrough2ActivityRunDetails.png
