---
title: aaaRegister Azure pile | Documents Microsoft
description: "Inscrire Azure Stack auprès de votre abonnement Azure."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: erikje
ms.openlocfilehash: 3a3c8e82bec3e1e26ecfe591ecc27b2b91f6f91e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="register-azure-stack-with-your-azure-subscription"></a><span data-ttu-id="e7cbb-103">Inscrire Azure Stack auprès de votre abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="e7cbb-103">Register Azure Stack with your Azure Subscription</span></span>

<span data-ttu-id="e7cbb-104">Pour les déploiements d’Azure Active Directory, vous pouvez inscrire Azure pile avec les éléments du marketplace toodownload Azure à partir d’Azure et tooset les données du rapport tooMicrosoft commerce.</span><span class="sxs-lookup"><span data-stu-id="e7cbb-104">For Azure Active Directory deployments, you can register Azure Stack with Azure toodownload marketplace items from Azure and tooset up commerce data reporting back tooMicrosoft.</span></span> 

> [!NOTE]
><span data-ttu-id="e7cbb-105">L’inscription est recommandée, car elle vous permet de tootest fonctionnalités importantes de la pile d’Azure, telles que la syndication de marketplace et des rapports d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="e7cbb-105">Registration is recommended because it enables you tootest important Azure Stack functionality, like marketplace syndication and usage reporting.</span></span> <span data-ttu-id="e7cbb-106">Après avoir enregistré la pile de Azure, l’utilisation est signalé tooAzure commerce.</span><span class="sxs-lookup"><span data-stu-id="e7cbb-106">After you register Azure Stack, usage is reported tooAzure commerce.</span></span> <span data-ttu-id="e7cbb-107">Vous pouvez le voir dans l’abonnement hello que vous avez utilisé pour l’inscription.</span><span class="sxs-lookup"><span data-stu-id="e7cbb-107">You can see it under hello subscription you used for registration.</span></span> <span data-ttu-id="e7cbb-108">Toute utilisation que les utilisateurs du kit de développement Azure Stack signalent ne leur sera pas facturée.</span><span class="sxs-lookup"><span data-stu-id="e7cbb-108">Azure Stack Development Kit users will not be charged for any usage they report.</span></span>
>


## <a name="get-azure-subscription"></a><span data-ttu-id="e7cbb-109">Prendre un abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="e7cbb-109">Get Azure subscription</span></span>

<span data-ttu-id="e7cbb-110">Avant d’inscrire Azure Stack auprès d’Azure, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e7cbb-110">Before registering Azure Stack with Azure, you must have:</span></span>

- <span data-ttu-id="e7cbb-111">ID d’abonnement Hello pour un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="e7cbb-111">hello subscription ID for an Azure subscription.</span></span> <span data-ttu-id="e7cbb-112">ID de hello tooget, connectez-vous tooAzure, cliquez sur **davantage de services** > **abonnements**, cliquez sur abonnement hello toouse et sous **Essentials** vous pouvez recherche hello **ID d’abonnement**.</span><span class="sxs-lookup"><span data-stu-id="e7cbb-112">tooget hello ID, sign in tooAzure, click **More services** > **Subscriptions**, click hello subscription you want toouse, and under **Essentials** you can find hello **Subscription ID**.</span></span> <span data-ttu-id="e7cbb-113">Les abonnements au cloud du gouvernement de Chine, d’Allemagne et des États-Unis ne sont pas pris en charge pour le moment.</span><span class="sxs-lookup"><span data-stu-id="e7cbb-113">China, Germany, and US government cloud subscriptions are not currently supported.</span></span>
- <span data-ttu-id="e7cbb-114">Hello nom d’utilisateur et mot de passe d’un compte qui est propriétaire de l’abonnement de hello (MSA/2FA sont prises en charge)</span><span class="sxs-lookup"><span data-stu-id="e7cbb-114">hello username and password for an account that is an owner for hello subscription (MSA/2FA accounts are supported)</span></span>
- <span data-ttu-id="e7cbb-115">Bonjour Azure Active Directory pour hello abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="e7cbb-115">hello Azure Active Directory for hello Azure subscription.</span></span> <span data-ttu-id="e7cbb-116">Vous trouverez ce répertoire dans Azure, en pointant sur votre avatar à hello coin supérieur droit de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e7cbb-116">You can find this directory in Azure by hovering over your avatar at hello top right corner of hello Azure portal.</span></span> 
- <span data-ttu-id="e7cbb-117">Fournisseur de ressources Azure pile hello inscrits (voir hello **inscrire le fournisseur de ressources Azure pile** section ci-dessous pour plus d’informations)</span><span class="sxs-lookup"><span data-stu-id="e7cbb-117">Registered hello Azure Stack resource provider (see hello **Register Azure Stack Resource Provider** section below for details)</span></span>

<span data-ttu-id="e7cbb-118">Si vous n’avez pas d’abonnement Azure répondant à ces exigences, vous pouvez [créer un compte Azure gratuit ici](https://azure.microsoft.com/en-us/free/?b=17.06).</span><span class="sxs-lookup"><span data-stu-id="e7cbb-118">If you don’t have an Azure subscription that meets these requirements, you can [create a free Azure account here](https://azure.microsoft.com/en-us/free/?b=17.06).</span></span> <span data-ttu-id="e7cbb-119">L’inscription d’Azure Stack n’entraîne aucun frais sur votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="e7cbb-119">Registering Azure Stack incurs no cost on your Azure subscription.</span></span>



## <a name="register-azure-stack-resource-provider-in-azure"></a><span data-ttu-id="e7cbb-120">Inscrire un fournisseur de ressources Azure Stack dans Azure</span><span class="sxs-lookup"><span data-stu-id="e7cbb-120">Register Azure Stack resource provider in Azure</span></span>
> [!NOTE] 
> <span data-ttu-id="e7cbb-121">Cette étape doit seulement toobe effectuée une seule fois dans un environnement de la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="e7cbb-121">This step only needs toobe completed once in an Azure Stack environment.</span></span>
>

1. <span data-ttu-id="e7cbb-122">Démarrez PowerShell ISE en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="e7cbb-122">Start Powershell ISE as an administrator.</span></span>
2. <span data-ttu-id="e7cbb-123">Se connecter toohello compte Azure qui est propriétaire de hello abonnement Azure avec le paramètre - EnvironmentName défini trop « Cloud Azure ».</span><span class="sxs-lookup"><span data-stu-id="e7cbb-123">Log in toohello Azure account that is an owner of hello Azure subscription with -EnvironmentName parameter set too"AzureCloud".</span></span>
3. <span data-ttu-id="e7cbb-124">Inscrire le fournisseur de ressources Azure hello « Microsoft.AzureStack ».</span><span class="sxs-lookup"><span data-stu-id="e7cbb-124">Register hello Azure resource provider "Microsoft.AzureStack".</span></span>

<span data-ttu-id="e7cbb-125">Exemple :</span><span class="sxs-lookup"><span data-stu-id="e7cbb-125">Example:</span></span> 
```Powershell
Login-AzureRmAccount -EnvironmentName "AzureCloud"
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.AzureStack -Force
```


## <a name="register-azure-stack-with-azure"></a><span data-ttu-id="e7cbb-126">Inscrire Azure Stack auprès d’Azure</span><span class="sxs-lookup"><span data-stu-id="e7cbb-126">Register Azure Stack with Azure</span></span>

> [!NOTE]
><span data-ttu-id="e7cbb-127">Toutes ces étapes doivent être effectuées sur l’ordinateur hôte hello.</span><span class="sxs-lookup"><span data-stu-id="e7cbb-127">All these steps must be completed on hello host computer.</span></span>
>

1. <span data-ttu-id="e7cbb-128">[Installez PowerShell pour Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="e7cbb-128">[Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span> 
2. <span data-ttu-id="e7cbb-129">Hello de copie [RegisterWithAzure.ps1 script](https://go.microsoft.com/fwlink/?linkid=842959) dossier tooa (tel que C:\Temp).</span><span class="sxs-lookup"><span data-stu-id="e7cbb-129">Copy hello [RegisterWithAzure.ps1 script](https://go.microsoft.com/fwlink/?linkid=842959) tooa folder (such as C:\Temp).</span></span>
3. <span data-ttu-id="e7cbb-130">Démarrez PowerShell ISE en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="e7cbb-130">Start PowerShell ISE as an administrator.</span></span>    
4. <span data-ttu-id="e7cbb-131">Exécutez hello RegisterWithAzure.ps1 script, en remplaçant hello suivant des espaces réservés :</span><span class="sxs-lookup"><span data-stu-id="e7cbb-131">Run hello RegisterWithAzure.ps1 script, replacing hello following placeholders:</span></span>
    - <span data-ttu-id="e7cbb-132">*YourAccountName* est propriétaire de hello Hello abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="e7cbb-132">*YourAccountName* is hello owner of hello Azure subscription</span></span>
    - <span data-ttu-id="e7cbb-133">*YourID* est l’ID d’abonnement Azure hello que vous souhaitez toouse tooregister pile d’Azure</span><span class="sxs-lookup"><span data-stu-id="e7cbb-133">*YourID* is hello Azure subscription ID that you want toouse tooregister Azure Stack</span></span>
    - <span data-ttu-id="e7cbb-134">*YourDirectory* hello désigne votre client Azure Active Directory dont fait partie de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="e7cbb-134">*YourDirectory* is hello name of your Azure Active Directory tenant that your Azure subscription is a part of.</span></span>

    ```powershell
    RegisterWithAzure.ps1 -azureSubscriptionId YourID -azureDirectoryTenantName YourDirectory -azureAccountId YourAccountName
    ```
    
    <span data-ttu-id="e7cbb-135">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="e7cbb-135">For example:</span></span>
    
    ```powershell
    C:\temp\RegisterWithAzure.ps1 -azureSubscriptionId "5e0ae55d-0b7a-47a3-afbc-8b372650abd3" `
    -azureDirectoryTenantName "contoso.onmicrosoft.com" `
    -azureAccountId serviceadmin@contoso.onmicrosoft.com
    ```
    
5. <span data-ttu-id="e7cbb-136">Deux invites de hello, appuyez sur ENTRÉE.</span><span class="sxs-lookup"><span data-stu-id="e7cbb-136">At hello two prompts, press Enter.</span></span>
6. <span data-ttu-id="e7cbb-137">Dans la fenêtre de connexion contextuelle hello, entrez vos informations d’identification de l’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="e7cbb-137">In hello pop-up login window, enter your Azure subscription credentials.</span></span>

## <a name="verify-hello-registration"></a><span data-ttu-id="e7cbb-138">Vérification de l’inscription de hello</span><span class="sxs-lookup"><span data-stu-id="e7cbb-138">Verify hello registration</span></span>

1. <span data-ttu-id="e7cbb-139">Se connecter dans le portail d’administration toohello (https://adminportal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="e7cbb-139">Sign in toohello administrator portal (https://adminportal.local.azurestack.external).</span></span>
2. <span data-ttu-id="e7cbb-140">Cliquez sur **Plus de services** > **Gestion de la Place de Marché** > **Ajouter à partir d’Azure**.</span><span class="sxs-lookup"><span data-stu-id="e7cbb-140">Click **More Services** > **Marketplace Management** > **Add from Azure**.</span></span>
3. <span data-ttu-id="e7cbb-141">Si une liste d’éléments disponibles dans Azure (tels que WordPress) s’affiche, l’activation a réussi.</span><span class="sxs-lookup"><span data-stu-id="e7cbb-141">If you see a list of items available from Azure (such as WordPress), your activation was successful.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e7cbb-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e7cbb-142">Next steps</span></span>

[<span data-ttu-id="e7cbb-143">Se connecter tooAzure pile</span><span class="sxs-lookup"><span data-stu-id="e7cbb-143">Connect tooAzure Stack</span></span>](azure-stack-connect-azure-stack.md)

