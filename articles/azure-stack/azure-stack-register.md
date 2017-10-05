---
title: "Inscrire Azure Stack | Microsoft Docs"
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
ms.openlocfilehash: f71ec571fee8e59ea9061cd619914b81a5bf701a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="register-azure-stack-with-your-azure-subscription"></a><span data-ttu-id="a0e77-103">Inscrire Azure Stack auprès de votre abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="a0e77-103">Register Azure Stack with your Azure Subscription</span></span>

<span data-ttu-id="a0e77-104">Pour les déploiements Azure Active Directory, vous pouvez inscrire Azure Stack auprès d’Azure pour télécharger des éléments de la Place de Marché à partir d’Azure et configurer la génération de rapports de données commerciales envoyés à Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a0e77-104">For Azure Active Directory deployments, you can register Azure Stack with Azure to download marketplace items from Azure and to set up commerce data reporting back to Microsoft.</span></span> 

> [!NOTE]
><span data-ttu-id="a0e77-105">L’inscription est recommandée, car elle vous permet de tester des fonctionnalités Azure Stack importantes, telles que la syndication de la Place de Marché et les rapports d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="a0e77-105">Registration is recommended because it enables you to test important Azure Stack functionality, like marketplace syndication and usage reporting.</span></span> <span data-ttu-id="a0e77-106">Après avoir inscrit Azure Stack, l’utilisation est signalée à Azure Commerce.</span><span class="sxs-lookup"><span data-stu-id="a0e77-106">After you register Azure Stack, usage is reported to Azure commerce.</span></span> <span data-ttu-id="a0e77-107">Vous pouvez la consulter sous l’abonnement utilisé pour l’inscription.</span><span class="sxs-lookup"><span data-stu-id="a0e77-107">You can see it under the subscription you used for registration.</span></span> <span data-ttu-id="a0e77-108">Toute utilisation que les utilisateurs du kit de développement Azure Stack signalent ne leur sera pas facturée.</span><span class="sxs-lookup"><span data-stu-id="a0e77-108">Azure Stack Development Kit users will not be charged for any usage they report.</span></span>
>


## <a name="get-azure-subscription"></a><span data-ttu-id="a0e77-109">Prendre un abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="a0e77-109">Get Azure subscription</span></span>

<span data-ttu-id="a0e77-110">Avant d’inscrire Azure Stack auprès d’Azure, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a0e77-110">Before registering Azure Stack with Azure, you must have:</span></span>

- <span data-ttu-id="a0e77-111">L’ID d’abonnement d’un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="a0e77-111">The subscription ID for an Azure subscription.</span></span> <span data-ttu-id="a0e77-112">Pour obtenir l’ID, connectez-vous à Azure, cliquez sur **Plus de services** > **Abonnements**, cliquez sur l’abonnement que vous voulez utiliser. Sous **Éléments principaux** vous trouverez alors l’**ID d’abonnement**.</span><span class="sxs-lookup"><span data-stu-id="a0e77-112">To get the ID, sign in to Azure, click **More services** > **Subscriptions**, click the subscription you want to use, and under **Essentials** you can find the **Subscription ID**.</span></span> <span data-ttu-id="a0e77-113">Les abonnements au cloud du gouvernement de Chine, d’Allemagne et des États-Unis ne sont pas pris en charge pour le moment.</span><span class="sxs-lookup"><span data-stu-id="a0e77-113">China, Germany, and US government cloud subscriptions are not currently supported.</span></span>
- <span data-ttu-id="a0e77-114">Le nom d’utilisateur et le mot de passe d’un compte qui est un propriétaire de l’abonnement (les comptes MSA/2FA sont pris en charge)</span><span class="sxs-lookup"><span data-stu-id="a0e77-114">The username and password for an account that is an owner for the subscription (MSA/2FA accounts are supported)</span></span>
- <span data-ttu-id="a0e77-115">L’annuaire Azure Active Directory de l’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="a0e77-115">The Azure Active Directory for the Azure subscription.</span></span> <span data-ttu-id="a0e77-116">Pour trouver cet annuaire dans Azure, pointez sur votre avatar situé en haut à droite dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a0e77-116">You can find this directory in Azure by hovering over your avatar at the top right corner of the Azure portal.</span></span> 
- <span data-ttu-id="a0e77-117">Le fournisseur de ressources Azure Stack inscrit (pour plus d’informations, consultez la section **Inscrire un fournisseur de ressources Azure Stack** ci-dessous)</span><span class="sxs-lookup"><span data-stu-id="a0e77-117">Registered the Azure Stack resource provider (see the **Register Azure Stack Resource Provider** section below for details)</span></span>

<span data-ttu-id="a0e77-118">Si vous n’avez pas d’abonnement Azure répondant à ces exigences, vous pouvez [créer un compte Azure gratuit ici](https://azure.microsoft.com/en-us/free/?b=17.06).</span><span class="sxs-lookup"><span data-stu-id="a0e77-118">If you don’t have an Azure subscription that meets these requirements, you can [create a free Azure account here](https://azure.microsoft.com/en-us/free/?b=17.06).</span></span> <span data-ttu-id="a0e77-119">L’inscription d’Azure Stack n’entraîne aucun frais sur votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="a0e77-119">Registering Azure Stack incurs no cost on your Azure subscription.</span></span>



## <a name="register-azure-stack-resource-provider-in-azure"></a><span data-ttu-id="a0e77-120">Inscrire un fournisseur de ressources Azure Stack dans Azure</span><span class="sxs-lookup"><span data-stu-id="a0e77-120">Register Azure Stack resource provider in Azure</span></span>
> [!NOTE] 
> <span data-ttu-id="a0e77-121">Cette étape ne doit être effectuée qu’une seule fois dans un environnement Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="a0e77-121">This step only needs to be completed once in an Azure Stack environment.</span></span>
>

1. <span data-ttu-id="a0e77-122">Démarrez PowerShell ISE en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="a0e77-122">Start Powershell ISE as an administrator.</span></span>
2. <span data-ttu-id="a0e77-123">Connectez-vous au compte Azure qui est un propriétaire de l’abonnement Azure avec le paramètre -EnvironmentName défini sur « AzureCloud ».</span><span class="sxs-lookup"><span data-stu-id="a0e77-123">Log in to the Azure account that is an owner of the Azure subscription with -EnvironmentName parameter set to "AzureCloud".</span></span>
3. <span data-ttu-id="a0e77-124">Inscrivez le fournisseur de ressources Azure « Microsoft.AzureStack ».</span><span class="sxs-lookup"><span data-stu-id="a0e77-124">Register the Azure resource provider "Microsoft.AzureStack".</span></span>

<span data-ttu-id="a0e77-125">Exemple :</span><span class="sxs-lookup"><span data-stu-id="a0e77-125">Example:</span></span> 
```Powershell
Login-AzureRmAccount -EnvironmentName "AzureCloud"
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.AzureStack -Force
```


## <a name="register-azure-stack-with-azure"></a><span data-ttu-id="a0e77-126">Inscrire Azure Stack auprès d’Azure</span><span class="sxs-lookup"><span data-stu-id="a0e77-126">Register Azure Stack with Azure</span></span>

> [!NOTE]
><span data-ttu-id="a0e77-127">Toutes les étapes suivantes doivent être effectuées sur l’ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="a0e77-127">All these steps must be completed on the host computer.</span></span>
>

1. <span data-ttu-id="a0e77-128">[Installez PowerShell pour Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="a0e77-128">[Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span> 
2. <span data-ttu-id="a0e77-129">Copiez le [script RegisterWithAzure.ps1](https://go.microsoft.com/fwlink/?linkid=842959) dans un dossier (tel que C:\Temp).</span><span class="sxs-lookup"><span data-stu-id="a0e77-129">Copy the [RegisterWithAzure.ps1 script](https://go.microsoft.com/fwlink/?linkid=842959) to a folder (such as C:\Temp).</span></span>
3. <span data-ttu-id="a0e77-130">Démarrez PowerShell ISE en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="a0e77-130">Start PowerShell ISE as an administrator.</span></span>    
4. <span data-ttu-id="a0e77-131">Exécutez le script RegisterWithAzure.ps1, en remplaçant les espaces réservés suivants :</span><span class="sxs-lookup"><span data-stu-id="a0e77-131">Run the RegisterWithAzure.ps1 script, replacing the following placeholders:</span></span>
    - <span data-ttu-id="a0e77-132">*YourAccountName* est le propriétaire de l’abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="a0e77-132">*YourAccountName* is the owner of the Azure subscription</span></span>
    - <span data-ttu-id="a0e77-133">*YourID* est l’ID d’abonnement Azure que vous voulez utiliser pour inscrire Azure Stack</span><span class="sxs-lookup"><span data-stu-id="a0e77-133">*YourID* is the Azure subscription ID that you want to use to register Azure Stack</span></span>
    - <span data-ttu-id="a0e77-134">*YourDirectory* est le nom de votre locataire Azure Active Directory dont fait partie votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="a0e77-134">*YourDirectory* is the name of your Azure Active Directory tenant that your Azure subscription is a part of.</span></span>

    ```powershell
    RegisterWithAzure.ps1 -azureSubscriptionId YourID -azureDirectoryTenantName YourDirectory -azureAccountId YourAccountName
    ```
    
    <span data-ttu-id="a0e77-135">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="a0e77-135">For example:</span></span>
    
    ```powershell
    C:\temp\RegisterWithAzure.ps1 -azureSubscriptionId "5e0ae55d-0b7a-47a3-afbc-8b372650abd3" `
    -azureDirectoryTenantName "contoso.onmicrosoft.com" `
    -azureAccountId serviceadmin@contoso.onmicrosoft.com
    ```
    
5. <span data-ttu-id="a0e77-136">Aux deux invites, appuyez sur Entrée.</span><span class="sxs-lookup"><span data-stu-id="a0e77-136">At the two prompts, press Enter.</span></span>
6. <span data-ttu-id="a0e77-137">Dans la fenêtre de connexion indépendante, entrez les informations d’identification de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="a0e77-137">In the pop-up login window, enter your Azure subscription credentials.</span></span>

## <a name="verify-the-registration"></a><span data-ttu-id="a0e77-138">Vérifier l’inscription</span><span class="sxs-lookup"><span data-stu-id="a0e77-138">Verify the registration</span></span>

1. <span data-ttu-id="a0e77-139">Connectez-vous au portail d’administration (https://adminportal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="a0e77-139">Sign in to the administrator portal (https://adminportal.local.azurestack.external).</span></span>
2. <span data-ttu-id="a0e77-140">Cliquez sur **Plus de services** > **Gestion de la Place de Marché** > **Ajouter à partir d’Azure**.</span><span class="sxs-lookup"><span data-stu-id="a0e77-140">Click **More Services** > **Marketplace Management** > **Add from Azure**.</span></span>
3. <span data-ttu-id="a0e77-141">Si une liste d’éléments disponibles dans Azure (tels que WordPress) s’affiche, l’activation a réussi.</span><span class="sxs-lookup"><span data-stu-id="a0e77-141">If you see a list of items available from Azure (such as WordPress), your activation was successful.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0e77-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a0e77-142">Next steps</span></span>

[<span data-ttu-id="a0e77-143">Se connecter à Azure Stack</span><span class="sxs-lookup"><span data-stu-id="a0e77-143">Connect to Azure Stack</span></span>](azure-stack-connect-azure-stack.md)

