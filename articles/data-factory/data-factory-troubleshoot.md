---
title: "problèmes d’Azure Data Factory aaaTroubleshoot"
description: "Découvrez comment tootroubleshoot problèmes à l’aide d’Azure Data Factory."
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
ms.openlocfilehash: cf65bcf3e1c3f061d3ac1dbf32e99cc7b014f9dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-data-factory-issues"></a><span data-ttu-id="21731-103">Résolution des problèmes liés à Data Factory</span><span class="sxs-lookup"><span data-stu-id="21731-103">Troubleshoot Data Factory issues</span></span>
<span data-ttu-id="21731-104">Cet article propose des conseils pour la résolution des problèmes d'utilisation d'Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="21731-104">This article provides troubleshooting tips for issues when using Azure Data Factory.</span></span> <span data-ttu-id="21731-105">Cet article ne répertorie pas tous les problèmes possibles hello lors de l’utilisation du service de hello, mais elle traite de certains problèmes et les conseils de dépannage générales.</span><span class="sxs-lookup"><span data-stu-id="21731-105">This article does not list all hello possible issues when using hello service, but it covers some issues and general troubleshooting tips.</span></span>   

## <a name="troubleshooting-tips"></a><span data-ttu-id="21731-106">Conseils de dépannage</span><span class="sxs-lookup"><span data-stu-id="21731-106">Troubleshooting tips</span></span>
### <a name="error-hello-subscription-is-not-registered-toouse-namespace-microsoftdatafactory"></a><span data-ttu-id="21731-107">Erreur : l’abonnement de hello n’est pas inscrit toouse, espace de noms 'Microsoft.DataFactory'</span><span class="sxs-lookup"><span data-stu-id="21731-107">Error: hello subscription is not registered toouse namespace 'Microsoft.DataFactory'</span></span>
<span data-ttu-id="21731-108">Si vous recevez cette erreur, fournisseur de ressources Azure Data Factory hello n’a pas été inscrit sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="21731-108">If you receive this error, hello Azure Data Factory resource provider has not been registered on your machine.</span></span> <span data-ttu-id="21731-109">Hello suivant :</span><span class="sxs-lookup"><span data-stu-id="21731-109">Do hello following:</span></span>

1. <span data-ttu-id="21731-110">Lancez Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="21731-110">Launch Azure PowerShell.</span></span>
2. <span data-ttu-id="21731-111">Ouvrez une session dans tooyour compte Azure à l’aide de hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="21731-111">Log in tooyour Azure account using hello following command.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="21731-112">Exécutez hello suivant le fournisseur de commandes tooregister hello Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="21731-112">Run hello following command tooregister hello Azure Data Factory provider.</span></span>

    ```powershell        
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

### <a name="problem-unauthorized-error-when-running-a-data-factory-cmdlet"></a><span data-ttu-id="21731-113">Problème : erreur non autorisée lors de l’exécution d’une applet de commande Data Factory</span><span class="sxs-lookup"><span data-stu-id="21731-113">Problem: Unauthorized error when running a Data Factory cmdlet</span></span>
<span data-ttu-id="21731-114">Vous utilisez probablement pas le droit de hello compte Azure ou d’abonnement avec hello Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="21731-114">You are probably not using hello right Azure account or subscription with hello Azure PowerShell.</span></span> <span data-ttu-id="21731-115">Utilisez hello suivant d’applets de commande tooselect hello droite toouse de compte et votre abonnement Azure avec hello Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="21731-115">Use hello following cmdlets tooselect hello right Azure account and subscription toouse with hello Azure PowerShell.</span></span>

1. <span data-ttu-id="21731-116">Connexion AzureRmAccount - hello utiliser l’ID d’utilisateur et mot de passe</span><span class="sxs-lookup"><span data-stu-id="21731-116">Login-AzureRmAccount - Use hello right user ID and password</span></span>
2. <span data-ttu-id="21731-117">Get-AzureRmSubscription - afficher tous les hello d’abonnements pour le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="21731-117">Get-AzureRmSubscription - View all hello subscriptions for hello account.</span></span>
3. <span data-ttu-id="21731-118">Sélectionnez-AzureRmSubscription &lt;nom de l’abonnement&gt; -sélectionnez l’abonnement hello.</span><span class="sxs-lookup"><span data-stu-id="21731-118">Select-AzureRmSubscription &lt;subscription name&gt; - Select hello right subscription.</span></span> <span data-ttu-id="21731-119">Utilisez hello identique à celui vous utilisez toocreate une fabrique de données sur hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="21731-119">Use hello same one you use toocreate a data factory on hello Azure portal.</span></span>

### <a name="problem-fail-toolaunch-data-management-gateway-express-setup-from-azure-portal"></a><span data-ttu-id="21731-120">Problème : Ne parviennent pas toolaunch le programme d’installation Express du passerelle de gestion des données à partir du portail Azure</span><span class="sxs-lookup"><span data-stu-id="21731-120">Problem: Fail toolaunch Data Management Gateway Express Setup from Azure portal</span></span>
<span data-ttu-id="21731-121">le programme d’installation Express de Hello pour hello passerelle de gestion des données requiert Internet Explorer ou un navigateur web compatible de Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="21731-121">hello Express setup for hello Data Management Gateway requires Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span> <span data-ttu-id="21731-122">Si le programme d’installation Express de hello échoue toostart, effectuez l’une des suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="21731-122">If hello Express Setup fails toostart, do one of hello following:</span></span>

* <span data-ttu-id="21731-123">Utilisez Internet Explorer ou un navigateur web compatible Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="21731-123">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>

    <span data-ttu-id="21731-124">Si vous utilisez Chrome, accédez toohello [Boutique Chrome](https://chrome.google.com/webstore/), recherche avec « ClickOnce » (mot clé), choisissez une des extensions de ClickOnce hello et installez-le.</span><span class="sxs-lookup"><span data-stu-id="21731-124">If you are using Chrome, go toohello [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>

    <span data-ttu-id="21731-125">Hello même pour Firefox (complément installation).</span><span class="sxs-lookup"><span data-stu-id="21731-125">Do hello same for Firefox (install add-in).</span></span> <span data-ttu-id="21731-126">Cliquez sur le bouton de Menu Ouvrir dans la barre d’outils de hello (trois lignes horizontales dans l’angle supérieur droit de hello) sur les modules complémentaires, recherche avec « ClickOnce » (mot clé), choisissez une des extensions de ClickOnce hello et installez-le.</span><span class="sxs-lookup"><span data-stu-id="21731-126">Click Open Menu button on hello toolbar (three horizontal lines in hello top-right corner), click Add-ons, search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>
* <span data-ttu-id="21731-127">Hello d’utilisation **le programme d’installation manuelle** lien affiché sur hello même panneau dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="21731-127">Use hello **Manual Setup** link shown on hello same blade in hello portal.</span></span> <span data-ttu-id="21731-128">Vous utilisez ce fichier d’installation toodownload approche et l’exécutez manuellement.</span><span class="sxs-lookup"><span data-stu-id="21731-128">You use this approach toodownload installation file and run it manually.</span></span> <span data-ttu-id="21731-129">Une fois l’installation de hello réussie, vous voyez la boîte de dialogue de Configuration de gestion des données à l’aide de la passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="21731-129">After hello installation is successful, you see hello Data Management Gateway Configuration dialog box.</span></span> <span data-ttu-id="21731-130">Hello de copie **clé** à partir de l’écran de portail hello et utilisez dans hello configuration manager toomanually inscrire la passerelle de hello auprès du service de hello.</span><span class="sxs-lookup"><span data-stu-id="21731-130">Copy hello **key** from hello portal screen and use it in hello configuration manager toomanually register hello gateway with hello service.</span></span>  

### <a name="problem-fail-tooconnect-tooon-premises-sql-server"></a><span data-ttu-id="21731-131">Problème : Ne parviennent pas tooconnect tooon local SQL Server</span><span class="sxs-lookup"><span data-stu-id="21731-131">Problem: Fail tooconnect tooon-premises SQL Server</span></span>
<span data-ttu-id="21731-132">Lancez **Gestionnaire de Configuration de passerelle de gestion de données** hello ordinateur passerelle et utiliser hello **dépannage** onglet tootest hello connexion tooSQL Server à partir de l’ordinateur de passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="21731-132">Launch **Data Management Gateway Configuration Manager** on hello gateway machine and use hello **Troubleshooting** tab tootest hello connection tooSQL Server from hello gateway machine.</span></span> <span data-ttu-id="21731-133">Consultez [Résolution des problèmes de passerelle](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) pour obtenir des conseils sur la résolution des problèmes de connexion/passerelle.</span><span class="sxs-lookup"><span data-stu-id="21731-133">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>   

### <a name="problem-input-slices-are-in-waiting-state-for-ever"></a><span data-ttu-id="21731-134">Problème : l’état des tranches d’entrée est En attente depuis longtemps</span><span class="sxs-lookup"><span data-stu-id="21731-134">Problem: Input slices are in Waiting state for ever</span></span>
<span data-ttu-id="21731-135">les tranches Hello pourrait être **attente** état en raison des raisons de toovarious.</span><span class="sxs-lookup"><span data-stu-id="21731-135">hello slices could be in **Waiting** state due toovarious reasons.</span></span> <span data-ttu-id="21731-136">Une des raisons courantes de hello est que hello **externe** propriété n’est pas définie trop**true**.</span><span class="sxs-lookup"><span data-stu-id="21731-136">One of hello common reasons is that hello **external** property is not set too**true**.</span></span> <span data-ttu-id="21731-137">Tout jeu de données est l’étendue de produits hello en dehors d’Azure Data Factory doit être marquée avec **externe** propriété.</span><span class="sxs-lookup"><span data-stu-id="21731-137">Any dataset that is produced outside hello scope of Azure Data Factory should be marked with **external** property.</span></span> <span data-ttu-id="21731-138">Cette propriété indique que les données hello pas sauvegardés par les pipelines au sein de la fabrique de données hello et externes.</span><span class="sxs-lookup"><span data-stu-id="21731-138">This property indicates that hello data is external and not backed by any pipelines within hello data factory.</span></span> <span data-ttu-id="21731-139">tranches de données Hello sont marqués comme **prêt** une fois que les données de salutation ne sont disponibles dans le store respectif de hello.</span><span class="sxs-lookup"><span data-stu-id="21731-139">hello data slices are marked as **Ready** once hello data is available in hello respective store.</span></span>

<span data-ttu-id="21731-140">Consultez hello exemple pour l’utilisation de hello Hello suivant **externe** propriété.</span><span class="sxs-lookup"><span data-stu-id="21731-140">See hello following example for hello usage of hello **external** property.</span></span> <span data-ttu-id="21731-141">Vous pouvez éventuellement spécifier **externalData*** lorsque vous définissez tootrue externe.</span><span class="sxs-lookup"><span data-stu-id="21731-141">You can optionally specify **externalData*** when you set external tootrue.</span></span>

<span data-ttu-id="21731-142">Consultez l’article [Jeux de données](data-factory-create-datasets.md) pour plus d’informations sur cette propriété.</span><span class="sxs-lookup"><span data-stu-id="21731-142">See [Datasets](data-factory-create-datasets.md) article for more details about this property.</span></span>

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

<span data-ttu-id="21731-143">tooresolve hello erreur, ajoutez hello **externe** propriété et hello facultatif **externalData** section Définition JSON de toohello de table d’entrée de hello et recréer la table de hello.</span><span class="sxs-lookup"><span data-stu-id="21731-143">tooresolve hello error, add hello **external** property and hello optional **externalData** section toohello JSON definition of hello input table and recreate hello table.</span></span>

### <a name="problem-hybrid-copy-operation-fails"></a><span data-ttu-id="21731-144">Problème : échec de l’opération de copie hybride</span><span class="sxs-lookup"><span data-stu-id="21731-144">Problem: Hybrid copy operation fails</span></span>
<span data-ttu-id="21731-145">Consultez [résoudre les problèmes de passerelle](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) pour stocker les problèmes tootroubleshoot avec la copie vers/à partir de des données locales à l’aide des étapes hello passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="21731-145">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for steps tootroubleshoot issues with copying to/from an on-premises data store using hello Data Management Gateway.</span></span>

### <a name="problem-on-demand-hdinsight-provisioning-fails"></a><span data-ttu-id="21731-146">Problème : échec de l’approvisionnement HDInsight à la demande</span><span class="sxs-lookup"><span data-stu-id="21731-146">Problem: On-demand HDInsight provisioning fails</span></span>
<span data-ttu-id="21731-147">Lorsque vous utilisez un service lié de type HDInsightOnDemand, vous devez toospecify un linkedServiceName qui pointe tooan stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="21731-147">When using a linked service of type HDInsightOnDemand, you need toospecify a linkedServiceName that points tooan Azure Blob Storage.</span></span> <span data-ttu-id="21731-148">Service de fabrique de données utilise ce stockage toostore journaux et les fichiers de prise en charge pour votre cluster HDInsight de la demande.</span><span class="sxs-lookup"><span data-stu-id="21731-148">Data Factory service uses this storage toostore logs and supporting files for your on-demand HDInsight cluster.</span></span>  <span data-ttu-id="21731-149">Parfois, l’approvisionnement d’un cluster de HDInsight à la demande échoue avec hello l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="21731-149">Sometimes provisioning of an on-demand HDInsight cluster fails with hello following error:</span></span>

```
Failed toocreate cluster. Exception: Unable toocomplete hello cluster create operation. Operation failed with code '400'. Cluster left behind state: 'Error'. Message: 'StorageAccountNotColocated'.
```

<span data-ttu-id="21731-150">Cette erreur indique généralement que hello hello du compte de stockage spécifié dans hello linkedServiceName se trouve pas dans hello Datacenter même emplacement où l’approvisionnement HDInsight hello qui se passe.</span><span class="sxs-lookup"><span data-stu-id="21731-150">This error usually indicates that hello location of hello storage account specified in hello linkedServiceName is not in hello same data center location where hello HDInsight provisioning is happening.</span></span> <span data-ttu-id="21731-151">Exemple : Si votre fabrique de données est dans l’ouest des États-Unis et hello stockage Azure est est des États-Unis, hello à la demande de configuration échoue dans l’ouest des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="21731-151">Example: if your data factory is in West US and hello Azure storage is in East US, hello on-demand provisioning fails in West US.</span></span>

<span data-ttu-id="21731-152">En outre, il existe une seconde propriété JSON additionalLinkedServiceNames avec laquelle les comptes de stockage supplémentaires peuvent être spécifiés dans HDInsight à la demande.</span><span class="sxs-lookup"><span data-stu-id="21731-152">Additionally, there is a second JSON property additionalLinkedServiceNames where additional storage accounts may be specified in on-demand HDInsight.</span></span> <span data-ttu-id="21731-153">Ces comptes de stockage supplémentaire doivent être Bonjour même emplacement que le cluster HDInsight de hello, ou si elle échoue avec hello même message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="21731-153">Those additional linked storage accounts should be in hello same location as hello HDInsight cluster, or it fails with hello same error.</span></span>

### <a name="problem-custom-net-activity-fails"></a><span data-ttu-id="21731-154">Problème : échec de l’activité .NET personnalisée</span><span class="sxs-lookup"><span data-stu-id="21731-154">Problem: Custom .NET activity fails</span></span>
<span data-ttu-id="21731-155">Consultez la page [Déboguer un pipeline avec une activité personnalisée](data-factory-use-custom-activities.md#troubleshoot-failures) pour obtenir des instructions détaillées.</span><span class="sxs-lookup"><span data-stu-id="21731-155">See [Debug a pipeline with custom activity](data-factory-use-custom-activities.md#troubleshoot-failures) for detailed steps.</span></span>

## <a name="use-azure-portal-tootroubleshoot"></a><span data-ttu-id="21731-156">Utilisez tootroubleshoot portail Azure</span><span class="sxs-lookup"><span data-stu-id="21731-156">Use Azure portal tootroubleshoot</span></span>
### <a name="using-portal-blades"></a><span data-ttu-id="21731-157">Utilisation des panneaux du portail</span><span class="sxs-lookup"><span data-stu-id="21731-157">Using portal blades</span></span>
<span data-ttu-id="21731-158">Consultez la page [Surveiller le pipeline](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) pour obtenir la procédure.</span><span class="sxs-lookup"><span data-stu-id="21731-158">See [Monitor pipeline](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) for steps.</span></span>

### <a name="using-monitor-and-manage-app"></a><span data-ttu-id="21731-159">Utilisation de l’application Surveillance et gestion</span><span class="sxs-lookup"><span data-stu-id="21731-159">Using Monitor and Manage App</span></span>
<span data-ttu-id="21731-160">Consultez [Surveiller et gérer les pipelines Data Factory à l’aide de l’application Surveillance et gestion](data-factory-monitor-manage-app.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="21731-160">See [Monitor and manage data factory pipelines using Monitor and Manage App](data-factory-monitor-manage-app.md) for details.</span></span>

## <a name="use-azure-powershell-tootroubleshoot"></a><span data-ttu-id="21731-161">Utiliser Azure PowerShell tootroubleshoot</span><span class="sxs-lookup"><span data-stu-id="21731-161">Use Azure PowerShell tootroubleshoot</span></span>
### <a name="use-azure-powershell-tootroubleshoot-an-error"></a><span data-ttu-id="21731-162">Utiliser Azure PowerShell tootroubleshoot une erreur</span><span class="sxs-lookup"><span data-stu-id="21731-162">Use Azure PowerShell tootroubleshoot an error</span></span>
<span data-ttu-id="21731-163">Consultez la page [Surveiller les pipelines Data Factory à l’aide d’Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="21731-163">See [Monitor Data Factory pipelines using Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) for details.</span></span>

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
