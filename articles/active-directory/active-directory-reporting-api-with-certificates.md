---
title: "Obtenir des données à l’aide de l’API Génération de rapports Azure AD avec des certificats | Microsoft Docs"
description: "Explique comment utiliser l’API Génération de rapports Azure AD avec les informations d’identification de certificat pour obtenir des données à partir de répertoires sans intervention de l’utilisateur."
services: active-directory
documentationcenter: 
author: ramical
writer: v-lorisc
manager: kannar
ms.assetid: 
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2017
ms.author: ramical
ms.openlocfilehash: c1345dcda6e52267a8037ffd7207e6bc3b0d3b31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-data-using-the-azure-ad-reporting-api-with-certificates"></a><span data-ttu-id="9f222-103">Obtenir des données à l’aide de l’API Génération de rapports Azure AD avec des certificats</span><span class="sxs-lookup"><span data-stu-id="9f222-103">Get data using the Azure AD Reporting API with certificates</span></span>
<span data-ttu-id="9f222-104">Cet article explique comment utiliser l’API Génération de rapports Azure AD avec les informations d’identification de certificat pour obtenir des données à partir de répertoires sans intervention de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9f222-104">This article discusses how to use the Azure AD Reporting API with certificate credentials to get data from directories without user intervention.</span></span> 

## <a name="use-the-azure-ad-reporting-api"></a><span data-ttu-id="9f222-105">Utiliser l’API Génération de rapports Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f222-105">Use the Azure AD Reporting API</span></span> 
<span data-ttu-id="9f222-106">L’API Génération de rapports Azure AD exige que vous effectuiez les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="9f222-106">Azure AD Reporting API requires that you complete the following steps:</span></span>
 *  <span data-ttu-id="9f222-107">Installation des composants requis</span><span class="sxs-lookup"><span data-stu-id="9f222-107">Install prerequisites</span></span>
 *  <span data-ttu-id="9f222-108">Définition du certificat dans votre application</span><span class="sxs-lookup"><span data-stu-id="9f222-108">Set the certificate in your app</span></span>
 *  <span data-ttu-id="9f222-109">Obtention d’un jeton d’accès</span><span class="sxs-lookup"><span data-stu-id="9f222-109">Get an access token</span></span>
 *  <span data-ttu-id="9f222-110">Utilisation du jeton d’accès pour appeler l’API Graph</span><span class="sxs-lookup"><span data-stu-id="9f222-110">Use the access token to call the Graph API</span></span>

<span data-ttu-id="9f222-111">Pour plus d’informations sur le code source, consultez [Leverage Report API Module](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils) (Utiliser le module d’API Génération de rapports).</span><span class="sxs-lookup"><span data-stu-id="9f222-111">For information about source code, see [Leverage Report API Module](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils).</span></span> 

### <a name="install-prerequisites"></a><span data-ttu-id="9f222-112">Installation des composants requis</span><span class="sxs-lookup"><span data-stu-id="9f222-112">Install prerequisites</span></span>
<span data-ttu-id="9f222-113">Vous devez avoir le module AzureADUtils et Azure AD PowerShell V2 installés.</span><span class="sxs-lookup"><span data-stu-id="9f222-113">You will need to have Azure AD PowerShell V2 and AzureADUtils module installed.</span></span>

1. <span data-ttu-id="9f222-114">Téléchargez et installez Azure AD Powershell V2 en suivant les instructions dans [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span><span class="sxs-lookup"><span data-stu-id="9f222-114">Download and install Azure AD Powershell V2, following the instructions at [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span></span>
2. <span data-ttu-id="9f222-115">Téléchargez le module Azure AD Utils à partir de [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span><span class="sxs-lookup"><span data-stu-id="9f222-115">Download the Azure AD Utils module from [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span></span> 
  <span data-ttu-id="9f222-116">Ce module fournit plusieurs applets de commande d’utilitaire, notamment :</span><span class="sxs-lookup"><span data-stu-id="9f222-116">This module provides several utility cmdlets including:</span></span>
   * <span data-ttu-id="9f222-117">La dernière version d’ADAL à l’aide de Nuget</span><span class="sxs-lookup"><span data-stu-id="9f222-117">The latest version of ADAL using Nuget</span></span>
   * <span data-ttu-id="9f222-118">Les jetons d’accès d’utilisateur, de clés d’application et de certificats à l’aide d’ADAL</span><span class="sxs-lookup"><span data-stu-id="9f222-118">Access tokens from user, application keys, and certificates using ADAL</span></span>
   * <span data-ttu-id="9f222-119">L’API Graph gérant les résultats paginés</span><span class="sxs-lookup"><span data-stu-id="9f222-119">Graph API handling paged results</span></span>

<span data-ttu-id="9f222-120">**Pour installer le module Azure AD Utils :**</span><span class="sxs-lookup"><span data-stu-id="9f222-120">**To install the Azure AD Utils module:**</span></span>

1. <span data-ttu-id="9f222-121">Créez un répertoire pour enregistrer le module d’utilitaires (par exemple, c:\azureAD) et téléchargez le module à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="9f222-121">Create a directory to save the utilities module (for example, c:\azureAD) and download the module from GitHub.</span></span>
2. <span data-ttu-id="9f222-122">Ouvrez une session PowerShell et accédez au répertoire que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="9f222-122">Open a PowerShell session, and go to the directory you just created.</span></span> 
3. <span data-ttu-id="9f222-123">Importez le module et installez-le dans le chemin d’accès du module PowerShell à l’aide de l’applet de commande Install-AzureADUtilsModule.</span><span class="sxs-lookup"><span data-stu-id="9f222-123">Import the module, and install it in the PowerShell module path using the Install-AzureADUtilsModule cmdlet.</span></span> 

<span data-ttu-id="9f222-124">La session doit ressembler à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="9f222-124">The session should look similar to this screen:</span></span>

  ![Windows PowerShell](./media/active-directory-report-api-with-certificates/windows-powershell.png)

### <a name="set-the-certificate-in-your-app"></a><span data-ttu-id="9f222-126">Définition du certificat dans votre application</span><span class="sxs-lookup"><span data-stu-id="9f222-126">Set the certificate in your app</span></span>
1. <span data-ttu-id="9f222-127">Si vous disposez déjà d’une application, récupérez son ID d’objet à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9f222-127">If you already have an app, get its Object ID from the Azure Portal.</span></span> 

  ![Portail Azure](./media/active-directory-report-api-with-certificates/azure-portal.png)

2. <span data-ttu-id="9f222-129">Ouvrez une session PowerShell et connectez-vous à Azure AD à l’aide de l’applet de commande Connect-AzureAD.</span><span class="sxs-lookup"><span data-stu-id="9f222-129">Open a PowerShell session and connect to Azure AD using the Connect-AzureAD cmdlet.</span></span>

  ![Portail Azure](./media/active-directory-report-api-with-certificates/connect-azuaread-cmdlet.png)

3. <span data-ttu-id="9f222-131">Utilisez l’applet de commande New-AzureADApplicationCertificateCredential d’AzureADUtils pour y ajouter des informations d’identification de certificat.</span><span class="sxs-lookup"><span data-stu-id="9f222-131">Use the New-AzureADApplicationCertificateCredential cmdlet from AzureADUtils to add a certificate credential to it.</span></span> 

>[!Note]
><span data-ttu-id="9f222-132">Vous devez fournir l’ID d’objet de l’application que vous avez récupéré précédemment, ainsi que l’objet de certificat (récupérez-le à l’aide du lecteur Cert :).</span><span class="sxs-lookup"><span data-stu-id="9f222-132">You need to provide the application Object ID that you captured earlier, as well as the certificate object (get this using the Cert: drive).</span></span>
>


  ![Portail Azure](./media/active-directory-report-api-with-certificates/add-certificate-credential.png)
  
### <a name="get-an-access-token"></a><span data-ttu-id="9f222-134">Obtention d’un jeton d’accès</span><span class="sxs-lookup"><span data-stu-id="9f222-134">Get an access token</span></span>

<span data-ttu-id="9f222-135">Pour obtenir un jeton d’accès, utilisez l’applet de commande Get-AzureADGraphAPIAccessTokenFromCert de AzureADUtils.</span><span class="sxs-lookup"><span data-stu-id="9f222-135">To get an access token, use the Get-AzureADGraphAPIAccessTokenFromCert cmdlet from AzureADUtils.</span></span> 

>[!NOTE]
><span data-ttu-id="9f222-136">Vous devez utiliser l’ID d’application plutôt que l’ID d’objet que vous avez utilisé dans la dernière section.</span><span class="sxs-lookup"><span data-stu-id="9f222-136">You need to use the Application ID instead of the Object ID that you used in the last section.</span></span>
>

 ![Portail Azure](./media/active-directory-report-api-with-certificates/application-id.png)

### <a name="use-the-access-token-to-call-the-graph-api"></a><span data-ttu-id="9f222-138">Utilisation du jeton d’accès pour appeler l’API Graph</span><span class="sxs-lookup"><span data-stu-id="9f222-138">Use the access token to call the Graph API</span></span>

<span data-ttu-id="9f222-139">Vous pouvez maintenant créer le script.</span><span class="sxs-lookup"><span data-stu-id="9f222-139">Now you can create the script.</span></span> <span data-ttu-id="9f222-140">Voici un exemple d’utilisation de l’applet de commande Invoke-AzureADGraphAPIQuery à partir du module AzureADUtils.</span><span class="sxs-lookup"><span data-stu-id="9f222-140">Below is an example using the Invoke-AzureADGraphAPIQuery cmdlet from the AzureADUtils.</span></span> <span data-ttu-id="9f222-141">Cette applet de commande gère les résultats composés de plusieurs pages et les envoie ensuite dans le pipeline PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9f222-141">This cmdlet handles multi-paged results, and then sends those results to the PowerShell pipeline.</span></span> 

 ![Portail Azure](./media/active-directory-report-api-with-certificates/script-completed.png)

<span data-ttu-id="9f222-143">Vous êtes maintenant prêt à exporter vers un fichier CSV et enregistrer dans un système SIEM.</span><span class="sxs-lookup"><span data-stu-id="9f222-143">You are now ready to export to a CSV and save to a SIEM system.</span></span> <span data-ttu-id="9f222-144">Vous pouvez également encapsuler votre script dans une tâche planifiée pour obtenir régulièrement des données Azure AD à partir de votre client sans avoir à stocker des clés d’application dans le code source.</span><span class="sxs-lookup"><span data-stu-id="9f222-144">You can also wrap your script in a scheduled task to get Azure AD data from your tenant periodically without having to store application keys in the source code.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9f222-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9f222-145">Next steps</span></span>
[<span data-ttu-id="9f222-146">Principes de base de la gestion des identités Azure</span><span class="sxs-lookup"><span data-stu-id="9f222-146">The fundamentals of Azure identity management</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity)<br>



