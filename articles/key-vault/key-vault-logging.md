---
title: "Journalisation d’Azure Key Vault | Microsoft Docs"
description: "Utilisez ce didacticiel pour vous aider à vous familiariser avec la journalisation du coffre de clés."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 43f96a2b-3af8-4adc-9344-bc6041fface8
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: e9a4f16f048833dab49f7db79892fe47a5aeff37
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-key-vault-logging"></a><span data-ttu-id="ae9ab-103">Journalisation d’Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="ae9ab-103">Azure Key Vault Logging</span></span>
<span data-ttu-id="ae9ab-104">Azure Key Vault est disponible dans la plupart des régions.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="ae9ab-105">Pour plus d’informations, consultez la [page de tarification de Key Vault](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="ae9ab-105">For more information, see the [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="ae9ab-106">Introduction</span><span class="sxs-lookup"><span data-stu-id="ae9ab-106">Introduction</span></span>
<span data-ttu-id="ae9ab-107">Une fois que vous avez créé un ou plusieurs coffres de clés, vous voulez sans doute contrôler qui accède à ces derniers, par quel moyen et quand.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-107">After you have created one or more key vaults, you will likely want to monitor how and when your key vaults are accessed, and by whom.</span></span> <span data-ttu-id="ae9ab-108">Pour ce faire, vous pouvez activer la journalisation du coffre de clés, ce qui permet d’enregistrer les informations dans un compte de stockage Azure que vous fournissez.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-108">You can do this by enabling logging for Key Vault, which saves information in an Azure storage account that you provide.</span></span> <span data-ttu-id="ae9ab-109">Un nouveau conteneur nommé **insights-logs-auditevent** est automatiquement créé pour le compte de stockage spécifié, et vous pouvez utiliser ce même compte pour recueillir les journaux de plusieurs coffres de clés.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-109">A new container named **insights-logs-auditevent** is automatically created for your specified storage account, and you can use this same storage account for collecting logs for multiple key vaults.</span></span>

<span data-ttu-id="ae9ab-110">Vous pouvez accéder aux informations de journalisation au plus 10 minutes après l’opération sur le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-110">You can access your logging information at most, 10 minutes after the key vault operation.</span></span> <span data-ttu-id="ae9ab-111">Dans la plupart des cas, ce sera plus rapide.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-111">In most cases, it will be quicker than this.</span></span>  <span data-ttu-id="ae9ab-112">C’est à vous de gérer vos journaux dans votre compte de stockage :</span><span class="sxs-lookup"><span data-stu-id="ae9ab-112">It's up to you to manage your logs in your storage account:</span></span>

* <span data-ttu-id="ae9ab-113">Utilisez les méthodes de contrôle d’accès Azure standard pour assurer la sécurité de vos journaux en limitant l’accès à ces derniers.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-113">Use standard Azure access control methods to secure your logs by restricting who can access them.</span></span>
* <span data-ttu-id="ae9ab-114">Supprimez les journaux que vous ne souhaitez plus conserver dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-114">Delete logs that you no longer want to keep in your storage account.</span></span>

<span data-ttu-id="ae9ab-115">Utilisez ce didacticiel pour vous familiariser avec Azure Key Vault pour créer votre compte de stockage, activer la journalisation et interpréter les informations de journalisation collectées.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-115">Use this tutorial to help you get started with Azure Key Vault logging, to create your storage account, enable logging, and interpret the logging information collected.</span></span>  

> [!NOTE]
> <span data-ttu-id="ae9ab-116">Ce didacticiel n’inclut pas d’instructions pour créer des coffres de clés, des clés ou des clés secrètes.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-116">This tutorial does not include instructions for how to create key vaults, keys, or secrets.</span></span> <span data-ttu-id="ae9ab-117">Pour plus d’informations, consultez [Prise en main d’Azure Key Vault](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ae9ab-117">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span> <span data-ttu-id="ae9ab-118">Ou, pour obtenir des instructions de l'interface de ligne de commande interplateforme, consultez [ce didacticiel équivalent](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="ae9ab-118">Or, for Cross-Platform Command-Line Interface instructions, see [this equivalent tutorial](key-vault-manage-with-cli2.md).</span></span>
>
> <span data-ttu-id="ae9ab-119">Actuellement, vous ne pouvez pas configurer Azure Key Vault dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-119">Currently, you cannot configure Azure Key Vault in the Azure portal.</span></span> <span data-ttu-id="ae9ab-120">Au lieu de cela, vous devez suivre ces instructions Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-120">Instead, use these Azure PowerShell instructions.</span></span>
>
>

<span data-ttu-id="ae9ab-121">Pour plus d’informations générales sur Azure Key Vault, consultez la page [Présentation d’Azure Key Vault](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="ae9ab-121">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae9ab-122">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ae9ab-122">Prerequisites</span></span>
<span data-ttu-id="ae9ab-123">Pour suivre ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ae9ab-123">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="ae9ab-124">Un coffre de clés existant que vous utilisez déjà.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-124">An existing key vault that you have been using.</span></span>  
* <span data-ttu-id="ae9ab-125">Azure PowerShell, **version 1.0.1 minimum**.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-125">Azure PowerShell, **minimum version of 1.0.1**.</span></span> <span data-ttu-id="ae9ab-126">Pour installer Azure PowerShell et l’associer à votre abonnement Azure, consultez l’article [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ae9ab-126">To install Azure PowerShell and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="ae9ab-127">Si vous avez déjà installé Azure PowerShell et que vous ne connaissez pas la version que vous utilisez, à partir de la console Azure PowerShell, entrez `(Get-Module azure -ListAvailable).Version`.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-127">If you have already installed Azure PowerShell and do not know the version, from the Azure PowerShell console, type `(Get-Module azure -ListAvailable).Version`.</span></span>  
* <span data-ttu-id="ae9ab-128">Espace de stockage suffisant sur Azure pour vos journaux de coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-128">Sufficient storage on Azure for your Key Vault logs.</span></span>

## <span data-ttu-id="ae9ab-129"><a id="connect"></a>Se connecter à vos abonnements</span><span class="sxs-lookup"><span data-stu-id="ae9ab-129"><a id="connect"></a>Connect to your subscriptions</span></span>
<span data-ttu-id="ae9ab-130">Démarrez une session Azure PowerShell et connectez-vous à votre compte Azure avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ae9ab-130">Start an Azure PowerShell session and sign in to your Azure account with the following command:</span></span>  

    Login-AzureRmAccount

<span data-ttu-id="ae9ab-131">Dans la fenêtre contextuelle de votre navigateur, entrez votre nom d’utilisateur et votre mot de passe Azure.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-131">In the pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="ae9ab-132">Azure PowerShell obtient alors tous les abonnements associés à ce compte et utilise par défaut le premier.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-132">Azure PowerShell will get all the subscriptions that are associated with this account and by default, uses the first one.</span></span>

<span data-ttu-id="ae9ab-133">Si vous disposez de plusieurs abonnements, vous devrez peut-être en spécifier un en particulier, celui qui a été utilisé pour créer votre Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-133">If you have multiple subscriptions, you might have to specify a specific one that was used to create your Azure Key Vault.</span></span> <span data-ttu-id="ae9ab-134">Tapez la commande suivante pour afficher les abonnements de votre compte :</span><span class="sxs-lookup"><span data-stu-id="ae9ab-134">Type the following to see the subscriptions for your account:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="ae9ab-135">Ensuite, pour spécifier l’abonnement associé au coffre de clés que vous allez consigner, tapez :</span><span class="sxs-lookup"><span data-stu-id="ae9ab-135">Then, to specify the subscription that's associated with your key vault you will be logging, type:</span></span>

    Set-AzureRmContext -SubscriptionId <subscription ID>

> [!NOTE]
> <span data-ttu-id="ae9ab-136">Cette étape est importante et particulièrement utile si plusieurs abonnements sont associés à votre compte.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-136">This is an important step and especially helpful if you have multiple subscriptions associated with your account.</span></span> <span data-ttu-id="ae9ab-137">Vous risquez de recevoir une erreur d’inscription de Microsoft.Insights si vous ignorez cette étape.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-137">You may receive an error to register Microsoft.Insights if this step is skipped.</span></span>
>   
>

<span data-ttu-id="ae9ab-138">Pour plus d’informations sur la configuration d’Azure PowerShell, consultez la page [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ae9ab-138">For more information about configuring Azure PowerShell, see  [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <span data-ttu-id="ae9ab-139"><a id="storage"></a>Création d’un nouveau compte de stockage pour vos journaux</span><span class="sxs-lookup"><span data-stu-id="ae9ab-139"><a id="storage"></a>Create a new storage account for your logs</span></span>
<span data-ttu-id="ae9ab-140">Bien que vous puissiez utiliser un compte de stockage existant pour vos journaux, nous allons en créer un nouveau qui sera dédié à vos journaux de coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-140">Although you can use an existing storage account for your logs, we'll create a new storage account that will be dedicated to Key Vault logs.</span></span> <span data-ttu-id="ae9ab-141">Pour plus de commodité, en prévision du moment où vous devrez le spécifier par la suite, nous allons enregistrer les détails dans une variable nommée **sa**.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-141">For convenience for when we have to specify this later, we'll store the details into a variable named **sa**.</span></span>

<span data-ttu-id="ae9ab-142">Pour faciliter encore la gestion, nous allons utiliser le groupe de ressources qui contient votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-142">For additional ease of management, we'll also use the same resource group as the one that contains our key vault.</span></span> <span data-ttu-id="ae9ab-143">Dans le [didacticiel de mise en route](key-vault-get-started.md), ce groupe de ressources se nomme **ContosoResourceGroup** et nous allons continuer d’utiliser l’emplacement Asie orientale.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-143">From the [getting started tutorial](key-vault-get-started.md), this resource group is named **ContosoResourceGroup** and we'll continue to use the East Asia location.</span></span> <span data-ttu-id="ae9ab-144">Remplacez ces valeurs par les vôtres, selon le cas :</span><span class="sxs-lookup"><span data-stu-id="ae9ab-144">Substitute these values for your own, as applicable:</span></span>

    $sa = New-AzureRmStorageAccount -ResourceGroupName ContosoResourceGroup -Name contosokeyvaultlogs -Type Standard_LRS -Location 'East Asia'


> [!NOTE]
> <span data-ttu-id="ae9ab-145">Si vous décidez d’utiliser un compte de stockage existant, vous devez utiliser le même abonnement que pour votre coffre de clés, ainsi que le modèle de déploiement Resource Manager plutôt que le modèle de déploiement Classic.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-145">If you decide to use an existing storage account, it must use the same subscription as your key vault and it must use the Resource Manager deployment model, rather than the Classic deployment model.</span></span>
>
>

## <span data-ttu-id="ae9ab-146"><a id="identify"></a>Identification du coffre de clés pour vos journaux</span><span class="sxs-lookup"><span data-stu-id="ae9ab-146"><a id="identify"></a>Identify the key vault for your logs</span></span>
<span data-ttu-id="ae9ab-147">Dans notre didacticiel de prise en main, le nom de notre coffre de clés était **ContosoKeyVault**, donc nous allons continuer à utiliser ce nom et stocker les détails dans une variable nommée **kv** :</span><span class="sxs-lookup"><span data-stu-id="ae9ab-147">In our getting started tutorial, our key vault name was **ContosoKeyVault**, so we'll continue to use that name and store the details into a variable named **kv**:</span></span>

    $kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'


## <span data-ttu-id="ae9ab-148"><a id="enable"></a>Activation de la journalisation</span><span class="sxs-lookup"><span data-stu-id="ae9ab-148"><a id="enable"></a>Enable logging</span></span>
<span data-ttu-id="ae9ab-149">Pour activer la journalisation du coffre de clés, nous allons utiliser l’applet de commande Set-AzureRmDiagnosticSetting, ainsi que les variables que nous avons créées pour notre compte de stockage et notre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-149">To enable logging for Key Vault, we'll use the Set-AzureRmDiagnosticSetting cmdlet, together with the variables we created for our new storage account and our key vault.</span></span> <span data-ttu-id="ae9ab-150">Nous allons également définir l’indicateur **-Enabled** sur **$true** et la catégorie sur AuditEvent (la seule catégorie pour la journalisation de Key Vault) :</span><span class="sxs-lookup"><span data-stu-id="ae9ab-150">We'll also set the **-Enabled** flag to **$true** and set the category to AuditEvent (the only category for Key Vault logging), :</span></span>

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

<span data-ttu-id="ae9ab-151">Le résultat de l’opération inclut :</span><span class="sxs-lookup"><span data-stu-id="ae9ab-151">The output for this includes:</span></span>

    StorageAccountId   : /subscriptions/<subscription-GUID>/resourceGroups/ContosoResourceGroup/providers/Microsoft.Storage/storageAccounts/ContosoKeyVaultLogs
    ServiceBusRuleId   :
    StorageAccountName :
        Logs
        Enabled           : True
        Category          : AuditEvent
        RetentionPolicy
        Enabled : False
        Days    : 0


<span data-ttu-id="ae9ab-152">L’activation de la journalisation de votre coffre de clés est à présent activée et les informations sont enregistrées dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-152">This confirms that logging is now enabled for your key vault, saving information to your storage account.</span></span>

<span data-ttu-id="ae9ab-153">Si vous le souhaitez, vous pouvez également définir une stratégie de rétention pour vos journaux, par exemple la suppression automatique des anciens journaux.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-153">Optionally you can also set retention policy for your logs such that older logs will be automatically deleted.</span></span> <span data-ttu-id="ae9ab-154">Par exemple, définissez une stratégie de rétention en attribuant à l’indicateur **-RetentionEnabled** la valeur **$true** et en définissant le paramètre **-RetentionInDays** sur **90** afin que les journaux antérieurs à 90 jours soient automatiquement supprimés.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-154">For example, set retention policy using **-RetentionEnabled** flag to **$true** and set **-RetentionInDays** parameter to **90** so that logs older than 90 days will be automatically deleted.</span></span>

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent -RetentionEnabled $true -RetentionInDays 90

<span data-ttu-id="ae9ab-155">Éléments consignés :</span><span class="sxs-lookup"><span data-stu-id="ae9ab-155">What's logged:</span></span>

* <span data-ttu-id="ae9ab-156">toutes les demandes API REST authentifiées sont enregistrées, ce qui inclut des requêtes ayant échoué suite à des demandes, des erreurs système ou des autorisations d’accès incorrectes ;</span><span class="sxs-lookup"><span data-stu-id="ae9ab-156">All authenticated REST API requests are logged, which includes failed requests as a result of access permissions, system errors or bad requests.</span></span>
* <span data-ttu-id="ae9ab-157">les opérations du coffre de clés lui-même, notamment la création, la suppression la définition des stratégies d’accès aux coffres de clés, et la mise à jour des attributs de coffre de clés (par exemple, les balises) ;</span><span class="sxs-lookup"><span data-stu-id="ae9ab-157">Operations on the key vault itself, which includes creation, deletion, setting key vault access policies, and updating key vault attributes such as tags.</span></span>
* <span data-ttu-id="ae9ab-158">les opérations sur les clés et les clés secrètes dans le coffre de clés, notamment la création, la modification ou la suppression de ces clés ou ces clés secrètes ; les opérations telles que la signature, la vérification, le chiffrement, le déchiffrement, l’encapsulage et le désencapsulage des clés, l’obtention des clés secrètes, la liste des clés et des clés secrètes et leurs versions.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-158">Operations on keys and secrets in the key vault, which includes creating, modifying, or deleting these keys or secrets; operations such as sign, verify, encrypt, decrypt, wrap and unwrap keys, get secrets, list keys and secrets and their versions.</span></span>
* <span data-ttu-id="ae9ab-159">les requêtes non authentifiées qui génèrent une réponse 401.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-159">Unauthenticated requests that result in a 401 response.</span></span> <span data-ttu-id="ae9ab-160">Par exemple, les requêtes qui ne possèdent pas de jeton de porteur, qui sont incorrectes, qui ont expiré ou qui comportent un jeton non valide.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-160">For example, requests that do not have a bearer token, or are malformed or expired, or have an invalid token.</span></span>  

## <span data-ttu-id="ae9ab-161"><a id="access"></a>Accéder à vos journaux</span><span class="sxs-lookup"><span data-stu-id="ae9ab-161"><a id="access"></a>Access your logs</span></span>
<span data-ttu-id="ae9ab-162">Les journaux de coffre de clés sont stockés dans le conteneur **insights-logs-auditevent** du compte de stockage que vous avez fourni.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-162">Key vault logs are stored in the **insights-logs-auditevent** container in the storage account you provided.</span></span> <span data-ttu-id="ae9ab-163">Pour répertorier tous les objets blob présents dans ce conteneur, saisissez :</span><span class="sxs-lookup"><span data-stu-id="ae9ab-163">To list all the blobs in this container, type:</span></span>

<span data-ttu-id="ae9ab-164">Commencez par créer une variable pour le nom du conteneur.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-164">First, create a variable for the container name.</span></span> <span data-ttu-id="ae9ab-165">Ce nom sera utilisé dans le reste de cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-165">This will be used throughout the rest of the walk through.</span></span>

    $container = 'insights-logs-auditevent'

<span data-ttu-id="ae9ab-166">Pour répertorier tous les objets blob présents dans ce conteneur, saisissez :</span><span class="sxs-lookup"><span data-stu-id="ae9ab-166">To list all the blobs in this container, type:</span></span>

    Get-AzureStorageBlob -Container $container -Context $sa.Context
<span data-ttu-id="ae9ab-167">Le résultat ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="ae9ab-167">The output will look something similar to this:</span></span>

<span data-ttu-id="ae9ab-168">**URI du conteneur : https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**</span><span class="sxs-lookup"><span data-stu-id="ae9ab-168">**Container Uri: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**</span></span>

<span data-ttu-id="ae9ab-169">**Nom**</span><span class="sxs-lookup"><span data-stu-id="ae9ab-169">**Name**</span></span>

- - -
<span data-ttu-id="ae9ab-170">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**</span><span class="sxs-lookup"><span data-stu-id="ae9ab-170">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**</span></span>

<span data-ttu-id="ae9ab-171">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**</span><span class="sxs-lookup"><span data-stu-id="ae9ab-171">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**</span></span>

<span data-ttu-id="ae9ab-172">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****</span><span class="sxs-lookup"><span data-stu-id="ae9ab-172">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****</span></span>

<span data-ttu-id="ae9ab-173">Comme vous pouvez le voir dans cette sortie, les objets blob suivent une convention d’affectation de noms : **resourceId =<ARM resource ID>/y =<year>/m =<month>/d =<day of month>/h =<hour>/m =<minute>/filename.json**</span><span class="sxs-lookup"><span data-stu-id="ae9ab-173">As you can see from this output, the blobs follow a naming convention: **resourceId=<ARM resource ID>/y=<year>/m=<month>/d=<day of month>/h=<hour>/m=<minute>/filename.json**</span></span>

<span data-ttu-id="ae9ab-174">Les valeurs de date et d’heure utilisent UTC.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-174">The date and time values use UTC.</span></span>

<span data-ttu-id="ae9ab-175">Le même compte de stockage pouvant être utilisé pour collecter les journaux de plusieurs ressources, l’ID complet de ressource dans le nom de l’objet blob est très utile si vous voulez accéder seulement aux objets blob dont vous avez besoin et les télécharger.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-175">Because the same storage account can be used to collect logs for multiple resources, the full resource ID in the blob name is very useful to access or download just the blobs that you need.</span></span> <span data-ttu-id="ae9ab-176">Mais avant cela, nous aborderons le téléchargement de tous les objets blob.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-176">But before we do that, we'll first cover how to download all the blobs.</span></span>

<span data-ttu-id="ae9ab-177">Tout d’abord, créez un dossier pour télécharger les objets blob.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-177">First, create a folder to download the blobs.</span></span> <span data-ttu-id="ae9ab-178">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="ae9ab-178">For example:</span></span>

    New-Item -Path 'C:\Users\username\ContosoKeyVaultLogs' -ItemType Directory -Force

<span data-ttu-id="ae9ab-179">Procurez-vous la liste de tous les objets blob :</span><span class="sxs-lookup"><span data-stu-id="ae9ab-179">Then get a list of all blobs:</span></span>  

    $blobs = Get-AzureStorageBlob -Container $container -Context $sa.Context

<span data-ttu-id="ae9ab-180">Adressez cette liste via « Get-AzureStorageBlobContent » pour télécharger les objets blob dans notre dossier de destination :</span><span class="sxs-lookup"><span data-stu-id="ae9ab-180">Pipe this list through 'Get-AzureStorageBlobContent' to download the blobs into our destination folder:</span></span>

    $blobs | Get-AzureStorageBlobContent -Destination 'C:\Users\username\ContosoKeyVaultLogs'

<span data-ttu-id="ae9ab-181">Lorsque vous exécutez cette seconde commande, le délimiteur **/** présent dans les noms d’objet blob crée une structure de dossiers complète sous le dossier de destination, structure qui servira à télécharger et à stocker les objets blob en tant que fichiers.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-181">When you run this second command, the **/** delimiter in the blob names create a full folder structure under the destination folder, and this structure will be used to download and store the blobs as files.</span></span>

<span data-ttu-id="ae9ab-182">Pour télécharger les objets blob de façon sélective, utilisez des caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-182">To selectively download blobs, use wildcards.</span></span> <span data-ttu-id="ae9ab-183">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="ae9ab-183">For example:</span></span>

* <span data-ttu-id="ae9ab-184">Si vous disposez de plusieurs coffres de clés et souhaitez télécharger les journaux d’un seul d’entre eux nommé CONTOSOKEYVAULT3 :</span><span class="sxs-lookup"><span data-stu-id="ae9ab-184">If you have multiple key vaults and want to download logs for just one key vault, named CONTOSOKEYVAULT3:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/VAULTS/CONTOSOKEYVAULT3
* <span data-ttu-id="ae9ab-185">Si vous disposez de plusieurs groupes de ressources et souhaitez télécharger les journaux d’un seul d’entre eux, utilisez `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:</span><span class="sxs-lookup"><span data-stu-id="ae9ab-185">If you have multiple resource groups and want to download logs for just one resource group, use `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/RESOURCEGROUPS/CONTOSORESOURCEGROUP3/*'
* <span data-ttu-id="ae9ab-186">Si vous souhaitez télécharger tous les journaux du mois de janvier 2016, utilisez `-Blob '*/year=2016/m=01/*'`:</span><span class="sxs-lookup"><span data-stu-id="ae9ab-186">If you want to download all the logs for the month of January 2016, use `-Blob '*/year=2016/m=01/*'`:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/year=2016/m=01/*'

<span data-ttu-id="ae9ab-187">Vous êtes maintenant prêt à commencer les recherches dans le contenu des journaux.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-187">You're now ready to start looking at what's in the logs.</span></span> <span data-ttu-id="ae9ab-188">Mais avant de passer à cette étape, il peut s’avérer utile de connaître deux autres paramètres de Get-AzureRmDiagnosticSetting :</span><span class="sxs-lookup"><span data-stu-id="ae9ab-188">But before moving onto that, two more parameters for Get-AzureRmDiagnosticSetting that you might need to know:</span></span>

* <span data-ttu-id="ae9ab-189">Pour interroger l’état des paramètres de diagnostic de votre ressource de coffre de clés : `Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`</span><span class="sxs-lookup"><span data-stu-id="ae9ab-189">To query the  status of diagnostic settings for your key vault resource: `Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`</span></span>
* <span data-ttu-id="ae9ab-190">Pour désactiver la journalisation de votre ressource de coffre de clés : `Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`</span><span class="sxs-lookup"><span data-stu-id="ae9ab-190">To disable logging for your key vault resource: `Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`</span></span>

## <span data-ttu-id="ae9ab-191"><a id="interpret"></a>Interpréter vos journaux Key Vault</span><span class="sxs-lookup"><span data-stu-id="ae9ab-191"><a id="interpret"></a>Interpret your Key Vault logs</span></span>
<span data-ttu-id="ae9ab-192">Les objets blob individuels sont stockés sous forme de texte en tant qu’objet blob JSON.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-192">Individual blobs are stored as text, formatted as a JSON blob.</span></span> <span data-ttu-id="ae9ab-193">Voici un exemple d’entrée de journal après l’exécution de `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`:</span><span class="sxs-lookup"><span data-stu-id="ae9ab-193">This is an example log entry from running `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`:</span></span>

    {
        "records":
        [
            {
                "time": "2016-01-05T01:32:01.2691226Z",
                "resourceId": "/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSOGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT",
                "operationName": "VaultGet",
                "operationVersion": "2015-06-01",
                "category": "AuditEvent",
                "resultType": "Success",
                "resultSignature": "OK",
                "resultDescription": "",
                "durationMs": "78",
                "callerIpAddress": "104.40.82.76",
                "correlationId": "",
                "identity": {"claim":{"http://schemas.microsoft.com/identity/claims/objectidentifier":"d9da5048-2737-4770-bd64-XXXXXXXXXXXX","http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn":"live.com#username@outlook.com","appid":"1950a258-227b-4e31-a9cf-XXXXXXXXXXXX"}},
                "properties": {"clientInfo":"azure-resource-manager/2.0","requestUri":"https://control-prod-wus.vaultcore.azure.net/subscriptions/361da5d4-a47a-4c79-afdd-XXXXXXXXXXXX/resourcegroups/contosoresourcegroup/providers/Microsoft.KeyVault/vaults/contosokeyvault?api-version=2015-06-01","id":"https://contosokeyvault.vault.azure.net/","httpStatusCode":200}
            }
        ]
    }


<span data-ttu-id="ae9ab-194">Le tableau suivant répertorie les noms de champ et les descriptions.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-194">The following table lists the field names and descriptions.</span></span>

| <span data-ttu-id="ae9ab-195">Nom du champ</span><span class="sxs-lookup"><span data-stu-id="ae9ab-195">Field name</span></span> | <span data-ttu-id="ae9ab-196">Description</span><span class="sxs-lookup"><span data-stu-id="ae9ab-196">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ae9ab-197">time</span><span class="sxs-lookup"><span data-stu-id="ae9ab-197">time</span></span> |<span data-ttu-id="ae9ab-198">Date et heure (UTC)</span><span class="sxs-lookup"><span data-stu-id="ae9ab-198">Date and time (UTC).</span></span> |
| <span data-ttu-id="ae9ab-199">resourceId</span><span class="sxs-lookup"><span data-stu-id="ae9ab-199">resourceId</span></span> |<span data-ttu-id="ae9ab-200">ID de ressource Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ae9ab-200">Azure Resource Manager Resource ID.</span></span> <span data-ttu-id="ae9ab-201">Pour les journaux de coffre de clés, il s’agit toujours de l’ID de ressource du coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-201">For Key Vault logs, this is always the  Key Vault resource ID.</span></span> |
| <span data-ttu-id="ae9ab-202">operationName</span><span class="sxs-lookup"><span data-stu-id="ae9ab-202">operationName</span></span> |<span data-ttu-id="ae9ab-203">Nom de l’opération, comme indiqué dans le tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-203">Name of the operation, as documented in the next table.</span></span> |
| <span data-ttu-id="ae9ab-204">operationVersion</span><span class="sxs-lookup"><span data-stu-id="ae9ab-204">operationVersion</span></span> |<span data-ttu-id="ae9ab-205">Il s’agit de la version de l’API REST demandée par le client.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-205">This is the REST API version requested by the client.</span></span> |
| <span data-ttu-id="ae9ab-206">category</span><span class="sxs-lookup"><span data-stu-id="ae9ab-206">category</span></span> |<span data-ttu-id="ae9ab-207">Pour les journaux de coffre de clés, AuditEvent est la seule valeur disponible.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-207">For Key Vault logs, AuditEvent is the single, available value.</span></span> |
| <span data-ttu-id="ae9ab-208">resultType</span><span class="sxs-lookup"><span data-stu-id="ae9ab-208">resultType</span></span> |<span data-ttu-id="ae9ab-209">Résultat de la demande d’API REST.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-209">Result of REST API request.</span></span> |
| <span data-ttu-id="ae9ab-210">resultSignature</span><span class="sxs-lookup"><span data-stu-id="ae9ab-210">resultSignature</span></span> |<span data-ttu-id="ae9ab-211">État HTTP</span><span class="sxs-lookup"><span data-stu-id="ae9ab-211">HTTP status.</span></span> |
| <span data-ttu-id="ae9ab-212">resultDescription</span><span class="sxs-lookup"><span data-stu-id="ae9ab-212">resultDescription</span></span> |<span data-ttu-id="ae9ab-213">Description supplémentaire du résultat le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-213">Additional description about the result, when available.</span></span> |
| <span data-ttu-id="ae9ab-214">durationMS</span><span class="sxs-lookup"><span data-stu-id="ae9ab-214">durationMs</span></span> |<span data-ttu-id="ae9ab-215">Délai nécessaire pour répondre à la demande API REST, en millisecondes.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-215">Time it took to service the REST API request, in milliseconds.</span></span> <span data-ttu-id="ae9ab-216">La latence du réseau n’est pas incluse dans ce chiffre et donc, le temps mesuré côté client peut ne pas correspondre à cette durée.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-216">This does not include the network latency, so the time you measure on the client side might not match this time.</span></span> |
| <span data-ttu-id="ae9ab-217">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="ae9ab-217">callerIpAddress</span></span> |<span data-ttu-id="ae9ab-218">Adresse IP du client qui a effectué la demande.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-218">IP address of the client who made the request.</span></span> |
| <span data-ttu-id="ae9ab-219">correlationId</span><span class="sxs-lookup"><span data-stu-id="ae9ab-219">correlationId</span></span> |<span data-ttu-id="ae9ab-220">GUID facultatif que le client peut transférer pour mettre en corrélation les journaux côté client avec les journaux côté service (Key Vault).</span><span class="sxs-lookup"><span data-stu-id="ae9ab-220">An optional GUID that the client can pass to correlate client-side logs with service-side (Key Vault) logs.</span></span> |
| <span data-ttu-id="ae9ab-221">identité</span><span class="sxs-lookup"><span data-stu-id="ae9ab-221">identity</span></span> |<span data-ttu-id="ae9ab-222">Identité issue du jeton qui a été présenté lors de la création de la demande de l’API REST.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-222">Identity from the token that was presented when making the REST API request.</span></span> <span data-ttu-id="ae9ab-223">Il s’agit généralement d’un « utilisateur », d’« un principal de service » ou d’une combinaison « utilisateur + appId », comme dans le cas d’une demande résultant d’une applet de commande PowerShell Azure.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-223">This is usually a "user", a "service principal" or a combination "user+appId" as in case of a request resulting from a Azure PowerShell cmdlet.</span></span> |
| <span data-ttu-id="ae9ab-224">properties</span><span class="sxs-lookup"><span data-stu-id="ae9ab-224">properties</span></span> |<span data-ttu-id="ae9ab-225">Ce champ contient des informations différentes en fonction de l’opération (operationName).</span><span class="sxs-lookup"><span data-stu-id="ae9ab-225">This field will contain different information based on the operation (operationName).</span></span> <span data-ttu-id="ae9ab-226">Dans la plupart des cas, il contient des informations client (chaîne useragent transmise par le client), l’URI de requête API REST exacte et le code d’état HTTP.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-226">In most cases, contains client information (the useragent string passed by the client), the exact REST API request URI, and HTTP status code.</span></span> <span data-ttu-id="ae9ab-227">En outre, lorsqu’un objet est retourné suite à une demande (par exemple, KeyCreate ou VaultGet), il contient également l’URI de clé (sous la forme « id »), l’URI d’archivage ou l’URI de clé secrète.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-227">In addition, when an object is returned as a result of a request (for example, KeyCreate or VaultGet) it will also contain the Key URI (as "id"), Vault URI, or Secret URI.</span></span> |

<span data-ttu-id="ae9ab-228">Les valeurs du champ **operationName** sont au format ObjectVerb.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-228">The **operationName** field values are in ObjectVerb format.</span></span> <span data-ttu-id="ae9ab-229">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="ae9ab-229">For example:</span></span>

* <span data-ttu-id="ae9ab-230">Toutes les opérations de coffre de clés sont au format « Vault`<action>` », comme `VaultGet` et `VaultCreate`.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-230">All key vault operations have the 'Vault`<action>`' format, such as `VaultGet` and `VaultCreate`.</span></span>
* <span data-ttu-id="ae9ab-231">Toutes les opérations de clé sont au format « Key`<action>` », comme `KeySign` et `KeyList`.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-231">All  key operations have the 'Key`<action>`' format, such as `KeySign` and `KeyList`.</span></span>
* <span data-ttu-id="ae9ab-232">Toutes les opérations de secret sont au format « Secret`<action>` », comme `SecretGet` et `SecretListVersions`.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-232">All secret operations have the 'Secret`<action>`' format, such as `SecretGet` and `SecretListVersions`.</span></span>

<span data-ttu-id="ae9ab-233">Le tableau suivant répertorie les éléments operationName et la commande API REST correspondante.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-233">The following table lists the operationName and corresponding REST API command.</span></span>

| <span data-ttu-id="ae9ab-234">operationName</span><span class="sxs-lookup"><span data-stu-id="ae9ab-234">operationName</span></span> | <span data-ttu-id="ae9ab-235">Commande API REST</span><span class="sxs-lookup"><span data-stu-id="ae9ab-235">REST API Command</span></span> |
| --- | --- |
| <span data-ttu-id="ae9ab-236">Authentification</span><span class="sxs-lookup"><span data-stu-id="ae9ab-236">Authentication</span></span> |<span data-ttu-id="ae9ab-237">Via le point de terminaison Azure Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="ae9ab-237">Via Azure Active Directory endpoint</span></span> |
| <span data-ttu-id="ae9ab-238">VaultGet</span><span class="sxs-lookup"><span data-stu-id="ae9ab-238">VaultGet</span></span> |[<span data-ttu-id="ae9ab-239">Obtention des informations sur un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="ae9ab-239">Get information about a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620026.aspx) |
| <span data-ttu-id="ae9ab-240">VaultPut</span><span class="sxs-lookup"><span data-stu-id="ae9ab-240">VaultPut</span></span> |[<span data-ttu-id="ae9ab-241">Création ou mise à jour d’un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="ae9ab-241">Create or update a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620025.aspx) |
| <span data-ttu-id="ae9ab-242">VaultDelete</span><span class="sxs-lookup"><span data-stu-id="ae9ab-242">VaultDelete</span></span> |[<span data-ttu-id="ae9ab-243">Suppression d’un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="ae9ab-243">Delete a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620022.aspx) |
| <span data-ttu-id="ae9ab-244">VaultPatch</span><span class="sxs-lookup"><span data-stu-id="ae9ab-244">VaultPatch</span></span> |[<span data-ttu-id="ae9ab-245">Mise à jour d’un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="ae9ab-245">Update a key vault</span></span>](https://msdn.microsoft.com/library/azure/mt620025.aspx) |
| <span data-ttu-id="ae9ab-246">VaultList</span><span class="sxs-lookup"><span data-stu-id="ae9ab-246">VaultList</span></span> |[<span data-ttu-id="ae9ab-247">Liste de l’ensemble des coffres de clés dans un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="ae9ab-247">List all key vaults in a resource group</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620027.aspx) |
| <span data-ttu-id="ae9ab-248">KeyCreate</span><span class="sxs-lookup"><span data-stu-id="ae9ab-248">KeyCreate</span></span> |[<span data-ttu-id="ae9ab-249">Création d’une clé</span><span class="sxs-lookup"><span data-stu-id="ae9ab-249">Create a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903634.aspx) |
| <span data-ttu-id="ae9ab-250">KeyGet</span><span class="sxs-lookup"><span data-stu-id="ae9ab-250">KeyGet</span></span> |[<span data-ttu-id="ae9ab-251">Obtention des informations sur une clé</span><span class="sxs-lookup"><span data-stu-id="ae9ab-251">Get information about a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878080.aspx) |
| <span data-ttu-id="ae9ab-252">KeyImport</span><span class="sxs-lookup"><span data-stu-id="ae9ab-252">KeyImport</span></span> |[<span data-ttu-id="ae9ab-253">Importation d’une clé dans un coffre</span><span class="sxs-lookup"><span data-stu-id="ae9ab-253">Import a key into a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903626.aspx) |
| <span data-ttu-id="ae9ab-254">KeyBackup</span><span class="sxs-lookup"><span data-stu-id="ae9ab-254">KeyBackup</span></span> |<span data-ttu-id="ae9ab-255">[Sauvegarde d’une clé](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx).</span><span class="sxs-lookup"><span data-stu-id="ae9ab-255">[Backup a key](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx).</span></span> |
| <span data-ttu-id="ae9ab-256">KeyDelete</span><span class="sxs-lookup"><span data-stu-id="ae9ab-256">KeyDelete</span></span> |[<span data-ttu-id="ae9ab-257">Suppression d’une clé</span><span class="sxs-lookup"><span data-stu-id="ae9ab-257">Delete a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903611.aspx) |
| <span data-ttu-id="ae9ab-258">KeyRestore</span><span class="sxs-lookup"><span data-stu-id="ae9ab-258">KeyRestore</span></span> |[<span data-ttu-id="ae9ab-259">Restauration d’une clé</span><span class="sxs-lookup"><span data-stu-id="ae9ab-259">Restore a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878106.aspx) |
| <span data-ttu-id="ae9ab-260">KeySign</span><span class="sxs-lookup"><span data-stu-id="ae9ab-260">KeySign</span></span> |[<span data-ttu-id="ae9ab-261">Signature avec une clé</span><span class="sxs-lookup"><span data-stu-id="ae9ab-261">Sign with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878096.aspx) |
| <span data-ttu-id="ae9ab-262">KeyVerify</span><span class="sxs-lookup"><span data-stu-id="ae9ab-262">KeyVerify</span></span> |[<span data-ttu-id="ae9ab-263">Vérification à l’aide d’une clé</span><span class="sxs-lookup"><span data-stu-id="ae9ab-263">Verify with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878082.aspx) |
| <span data-ttu-id="ae9ab-264">KeyWrap</span><span class="sxs-lookup"><span data-stu-id="ae9ab-264">KeyWrap</span></span> |[<span data-ttu-id="ae9ab-265">Encapsulage d’une clé</span><span class="sxs-lookup"><span data-stu-id="ae9ab-265">Wrap a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878066.aspx) |
| <span data-ttu-id="ae9ab-266">KeyUnwrap</span><span class="sxs-lookup"><span data-stu-id="ae9ab-266">KeyUnwrap</span></span> |[<span data-ttu-id="ae9ab-267">Désencapsulage d’une clé</span><span class="sxs-lookup"><span data-stu-id="ae9ab-267">Unwrap a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878079.aspx) |
| <span data-ttu-id="ae9ab-268">KeyEncrypt</span><span class="sxs-lookup"><span data-stu-id="ae9ab-268">KeyEncrypt</span></span> |[<span data-ttu-id="ae9ab-269">Chiffrement avec une clé</span><span class="sxs-lookup"><span data-stu-id="ae9ab-269">Encrypt with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878060.aspx) |
| <span data-ttu-id="ae9ab-270">KeyDecrypt</span><span class="sxs-lookup"><span data-stu-id="ae9ab-270">KeyDecrypt</span></span> |[<span data-ttu-id="ae9ab-271">Déchiffrement avec une clé</span><span class="sxs-lookup"><span data-stu-id="ae9ab-271">Decrypt with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878097.aspx) |
| <span data-ttu-id="ae9ab-272">KeyUpdate</span><span class="sxs-lookup"><span data-stu-id="ae9ab-272">KeyUpdate</span></span> |[<span data-ttu-id="ae9ab-273">Mise à jour d’une clé</span><span class="sxs-lookup"><span data-stu-id="ae9ab-273">Update a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903616.aspx) |
| <span data-ttu-id="ae9ab-274">KeyList</span><span class="sxs-lookup"><span data-stu-id="ae9ab-274">KeyList</span></span> |[<span data-ttu-id="ae9ab-275">Liste des clés dans un coffre</span><span class="sxs-lookup"><span data-stu-id="ae9ab-275">List the keys in a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903629.aspx) |
| <span data-ttu-id="ae9ab-276">KeyListVersions</span><span class="sxs-lookup"><span data-stu-id="ae9ab-276">KeyListVersions</span></span> |[<span data-ttu-id="ae9ab-277">Liste des versions d’une clé</span><span class="sxs-lookup"><span data-stu-id="ae9ab-277">List the versions of a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986822.aspx) |
| <span data-ttu-id="ae9ab-278">SecretSet</span><span class="sxs-lookup"><span data-stu-id="ae9ab-278">SecretSet</span></span> |[<span data-ttu-id="ae9ab-279">Création d’une clé secrète</span><span class="sxs-lookup"><span data-stu-id="ae9ab-279">Create a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903618.aspx) |
| <span data-ttu-id="ae9ab-280">SecretGet</span><span class="sxs-lookup"><span data-stu-id="ae9ab-280">SecretGet</span></span> |[<span data-ttu-id="ae9ab-281">Obtention d’une clé secrète</span><span class="sxs-lookup"><span data-stu-id="ae9ab-281">Get secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903633.aspx) |
| <span data-ttu-id="ae9ab-282">SecretUpdate</span><span class="sxs-lookup"><span data-stu-id="ae9ab-282">SecretUpdate</span></span> |[<span data-ttu-id="ae9ab-283">Mise à jour d’une clé secrète</span><span class="sxs-lookup"><span data-stu-id="ae9ab-283">Update a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986818.aspx) |
| <span data-ttu-id="ae9ab-284">SecretDelete</span><span class="sxs-lookup"><span data-stu-id="ae9ab-284">SecretDelete</span></span> |[<span data-ttu-id="ae9ab-285">Suppression d’une clé secrète</span><span class="sxs-lookup"><span data-stu-id="ae9ab-285">Delete a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903613.aspx) |
| <span data-ttu-id="ae9ab-286">SecretList</span><span class="sxs-lookup"><span data-stu-id="ae9ab-286">SecretList</span></span> |[<span data-ttu-id="ae9ab-287">Liste des clés secrètes d’un coffre</span><span class="sxs-lookup"><span data-stu-id="ae9ab-287">List secrets in a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903614.aspx) |
| <span data-ttu-id="ae9ab-288">SecretListVersions</span><span class="sxs-lookup"><span data-stu-id="ae9ab-288">SecretListVersions</span></span> |[<span data-ttu-id="ae9ab-289">Liste des versions d’une clé secrète</span><span class="sxs-lookup"><span data-stu-id="ae9ab-289">List versions of a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986824.aspx) |

## <span data-ttu-id="ae9ab-290"><a id="loganalytics"></a>Utilisation de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="ae9ab-290"><a id="loganalytics"></a>Use Log Analytics</span></span>

<span data-ttu-id="ae9ab-291">Vous pouvez utiliser la solution Azure Key Vault dans Log Analytics pour consulter les journaux AuditEvent d’Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-291">You can use the Azure Key Vault solution in Log Analytics to review Azure Key Vault AuditEvent logs.</span></span> <span data-ttu-id="ae9ab-292">Pour plus d’informations, notamment sur la configuration, consultez la page [Solution Azure Key Vault dans Log Analytics](../log-analytics/log-analytics-azure-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="ae9ab-292">For more information, including how to set this up, see [Azure Key Vault solution in Log Analytics](../log-analytics/log-analytics-azure-key-vault.md).</span></span> <span data-ttu-id="ae9ab-293">Cet article contient également des instructions si vous devez migrer à partir de l’ancienne solution Key Vault qui proposée dans la version préliminaire de Log Analytics, où vous avez d’abord acheminé vos journaux vers un compte de stockage Azure et configuré Log Analytics pour lire à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="ae9ab-293">This article also contains instructions if you need to migrate from the old Key Vault solution that was offered during the Log Analytics preview, where you first routed your logs to an Azure Storage account and configured Log Analytics to read from there.</span></span>

## <span data-ttu-id="ae9ab-294"><a id="next"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ae9ab-294"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="ae9ab-295">Pour accéder à un didacticiel utilisant Azure Key Vault dans une application web, consultez l’article [Utilisation d’Azure Key Vault à partir d’une application web](key-vault-use-from-web-application.md).</span><span class="sxs-lookup"><span data-stu-id="ae9ab-295">For a tutorial that uses Azure Key Vault in a web application, see [Use Azure Key Vault from a Web Application](key-vault-use-from-web-application.md).</span></span>

<span data-ttu-id="ae9ab-296">Pour les références de programmation, consultez le [guide du développeur de coffre de clés Azure](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="ae9ab-296">For programming references, see [the Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>

<span data-ttu-id="ae9ab-297">Pour obtenir la liste des applets de commande Azure PowerShell 1.0 pour Azure Key Vault, consultez l’article [Azure Key Vault Cmdlets (Applets de commande Azure Key Vault)](/powershell/module/azurerm.keyvault/#key_vault).</span><span class="sxs-lookup"><span data-stu-id="ae9ab-297">For a list of Azure PowerShell 1.0 cmdlets for Azure Key Vault, see [Azure Key Vault Cmdlets](/powershell/module/azurerm.keyvault/#key_vault).</span></span>

<span data-ttu-id="ae9ab-298">Pour accéder à un didacticiel sur la rotation des clés et les journaux d’audit avec Azure Key Vault, consultez l’article [Configuration du coffre de clés avec une rotation des clés et un audit de bout en bout](key-vault-key-rotation-log-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="ae9ab-298">For a tutorial on key rotation and log auditing with Azure Key Vault, see [How to setup Key Vault with end to end key rotation and auditing](key-vault-key-rotation-log-monitoring.md).</span></span>
