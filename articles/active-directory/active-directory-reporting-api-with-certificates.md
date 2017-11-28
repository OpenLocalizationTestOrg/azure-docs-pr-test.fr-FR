---
title: "à l’aide des données aaaGet hello Azure API de création de rapports AD avec les certificats | Documents Microsoft"
description: "Explique comment toouse hello Azure API de création de rapports AD avec des données de tooget informations d’identification de certificat à partir d’annuaires sans intervention de l’utilisateur."
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
ms.openlocfilehash: 00ddfaefe32ea6ae48f276c974a17ddcf84f7894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-data-using-hello-azure-ad-reporting-api-with-certificates"></a><span data-ttu-id="1c89a-103">Obtenir des données à l’aide des API de création de rapports Azure AD hello avec des certificats</span><span class="sxs-lookup"><span data-stu-id="1c89a-103">Get data using hello Azure AD Reporting API with certificates</span></span>
<span data-ttu-id="1c89a-104">Cet article explique comment toouse hello Azure API de création de rapports AD avec des données de tooget informations d’identification de certificat à partir d’annuaires sans intervention de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1c89a-104">This article discusses how toouse hello Azure AD Reporting API with certificate credentials tooget data from directories without user intervention.</span></span> 

## <a name="use-hello-azure-ad-reporting-api"></a><span data-ttu-id="1c89a-105">Utilisez hello API de création de rapports AD Azure</span><span class="sxs-lookup"><span data-stu-id="1c89a-105">Use hello Azure AD Reporting API</span></span> 
<span data-ttu-id="1c89a-106">API de création de rapports AD Azure nécessite que vous avez terminé de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="1c89a-106">Azure AD Reporting API requires that you complete hello following steps:</span></span>
 *  <span data-ttu-id="1c89a-107">Installation des composants requis</span><span class="sxs-lookup"><span data-stu-id="1c89a-107">Install prerequisites</span></span>
 *  <span data-ttu-id="1c89a-108">Définissez le certificat hello dans votre application</span><span class="sxs-lookup"><span data-stu-id="1c89a-108">Set hello certificate in your app</span></span>
 *  <span data-ttu-id="1c89a-109">Obtention d’un jeton d’accès</span><span class="sxs-lookup"><span data-stu-id="1c89a-109">Get an access token</span></span>
 *  <span data-ttu-id="1c89a-110">Utilisez hello de jeton toocall hello accès API Graph</span><span class="sxs-lookup"><span data-stu-id="1c89a-110">Use hello access token toocall hello Graph API</span></span>

<span data-ttu-id="1c89a-111">Pour plus d’informations sur le code source, consultez [Leverage Report API Module](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils) (Utiliser le module d’API Génération de rapports).</span><span class="sxs-lookup"><span data-stu-id="1c89a-111">For information about source code, see [Leverage Report API Module](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils).</span></span> 

### <a name="install-prerequisites"></a><span data-ttu-id="1c89a-112">Installation des composants requis</span><span class="sxs-lookup"><span data-stu-id="1c89a-112">Install prerequisites</span></span>
<span data-ttu-id="1c89a-113">Vous devez toohave Azure AD PowerShell V2 et module AzureADUtils installé.</span><span class="sxs-lookup"><span data-stu-id="1c89a-113">You will need toohave Azure AD PowerShell V2 and AzureADUtils module installed.</span></span>

1. <span data-ttu-id="1c89a-114">Téléchargez et installez Azure AD Powershell V2, suivant les instructions de hello sur [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span><span class="sxs-lookup"><span data-stu-id="1c89a-114">Download and install Azure AD Powershell V2, following hello instructions at [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span></span>
2. <span data-ttu-id="1c89a-115">Télécharger le module Azure AD Utils hello [organisation/azure-Active Directory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span><span class="sxs-lookup"><span data-stu-id="1c89a-115">Download hello Azure AD Utils module from [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span></span> 
  <span data-ttu-id="1c89a-116">Ce module fournit plusieurs applets de commande d’utilitaire, notamment :</span><span class="sxs-lookup"><span data-stu-id="1c89a-116">This module provides several utility cmdlets including:</span></span>
   * <span data-ttu-id="1c89a-117">version la plus récente de la bibliothèque ADAL à l’aide de Nuget Hello</span><span class="sxs-lookup"><span data-stu-id="1c89a-117">hello latest version of ADAL using Nuget</span></span>
   * <span data-ttu-id="1c89a-118">Les jetons d’accès d’utilisateur, de clés d’application et de certificats à l’aide d’ADAL</span><span class="sxs-lookup"><span data-stu-id="1c89a-118">Access tokens from user, application keys, and certificates using ADAL</span></span>
   * <span data-ttu-id="1c89a-119">L’API Graph gérant les résultats paginés</span><span class="sxs-lookup"><span data-stu-id="1c89a-119">Graph API handling paged results</span></span>

<span data-ttu-id="1c89a-120">**module de Azure AD Utils tooinstall hello :**</span><span class="sxs-lookup"><span data-stu-id="1c89a-120">**tooinstall hello Azure AD Utils module:**</span></span>

1. <span data-ttu-id="1c89a-121">Créer un module d’utilitaires de répertoire toosave hello (par exemple, c:\azureAD) et télécharger le module de hello à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="1c89a-121">Create a directory toosave hello utilities module (for example, c:\azureAD) and download hello module from GitHub.</span></span>
2. <span data-ttu-id="1c89a-122">Ouvrez une session PowerShell et accédez répertoire toohello que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="1c89a-122">Open a PowerShell session, and go toohello directory you just created.</span></span> 
3. <span data-ttu-id="1c89a-123">Importer le module de hello et installez-le dans le chemin du module PowerShell hello à l’aide d’applet de commande hello AzureADUtilsModule de l’installation.</span><span class="sxs-lookup"><span data-stu-id="1c89a-123">Import hello module, and install it in hello PowerShell module path using hello Install-AzureADUtilsModule cmdlet.</span></span> 

<span data-ttu-id="1c89a-124">session de Hello doit se présenter comme écran de toothis :</span><span class="sxs-lookup"><span data-stu-id="1c89a-124">hello session should look similar toothis screen:</span></span>

  ![Windows PowerShell](./media/active-directory-report-api-with-certificates/windows-powershell.png)

### <a name="set-hello-certificate-in-your-app"></a><span data-ttu-id="1c89a-126">Définissez le certificat hello dans votre application</span><span class="sxs-lookup"><span data-stu-id="1c89a-126">Set hello certificate in your app</span></span>
1. <span data-ttu-id="1c89a-127">Si vous disposez déjà d’une application, obtenir son ID d’objet à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1c89a-127">If you already have an app, get its Object ID from hello Azure Portal.</span></span> 

  ![Portail Azure](./media/active-directory-report-api-with-certificates/azure-portal.png)

2. <span data-ttu-id="1c89a-129">Ouvrez une session PowerShell et se connecter tooAzure AD à l’aide d’applet de commande hello organisation de se connecter.</span><span class="sxs-lookup"><span data-stu-id="1c89a-129">Open a PowerShell session and connect tooAzure AD using hello Connect-AzureAD cmdlet.</span></span>

  ![Portail Azure](./media/active-directory-report-api-with-certificates/connect-azuaread-cmdlet.png)

3. <span data-ttu-id="1c89a-131">Utilisez hello applet de commande New-AzureADApplicationCertificateCredential de AzureADUtils tooadd un tooit d’informations d’identification de certificat.</span><span class="sxs-lookup"><span data-stu-id="1c89a-131">Use hello New-AzureADApplicationCertificateCredential cmdlet from AzureADUtils tooadd a certificate credential tooit.</span></span> 

>[!Note]
><span data-ttu-id="1c89a-132">Vous avez besoin d’application de hello tooprovide ID d’objet que vous avez capturés précédemment, ainsi que hello d’objet de certificat (obtenir à l’aide de cette hello Cert : lecteur).</span><span class="sxs-lookup"><span data-stu-id="1c89a-132">You need tooprovide hello application Object ID that you captured earlier, as well as hello certificate object (get this using hello Cert: drive).</span></span>
>


  ![Portail Azure](./media/active-directory-report-api-with-certificates/add-certificate-credential.png)
  
### <a name="get-an-access-token"></a><span data-ttu-id="1c89a-134">Obtention d’un jeton d’accès</span><span class="sxs-lookup"><span data-stu-id="1c89a-134">Get an access token</span></span>

<span data-ttu-id="1c89a-135">tooget un jeton d’accès, utilisez hello applet de commande Get-AzureADGraphAPIAccessTokenFromCert de AzureADUtils.</span><span class="sxs-lookup"><span data-stu-id="1c89a-135">tooget an access token, use hello Get-AzureADGraphAPIAccessTokenFromCert cmdlet from AzureADUtils.</span></span> 

>[!NOTE]
><span data-ttu-id="1c89a-136">Vous devez toouse hello ID d’Application au lieu de hello ID d’objet que vous avez utilisé dans la dernière section de hello.</span><span class="sxs-lookup"><span data-stu-id="1c89a-136">You need toouse hello Application ID instead of hello Object ID that you used in hello last section.</span></span>
>

 ![Portail Azure](./media/active-directory-report-api-with-certificates/application-id.png)

### <a name="use-hello-access-token-toocall-hello-graph-api"></a><span data-ttu-id="1c89a-138">Utilisez hello de jeton toocall hello accès API Graph</span><span class="sxs-lookup"><span data-stu-id="1c89a-138">Use hello access token toocall hello Graph API</span></span>

<span data-ttu-id="1c89a-139">Vous pouvez désormais créer le script de hello.</span><span class="sxs-lookup"><span data-stu-id="1c89a-139">Now you can create hello script.</span></span> <span data-ttu-id="1c89a-140">Voici un exemple utilisant l’applet de commande Invoke-AzureADGraphAPIQuery de hello hello AzureADUtils.</span><span class="sxs-lookup"><span data-stu-id="1c89a-140">Below is an example using hello Invoke-AzureADGraphAPIQuery cmdlet from hello AzureADUtils.</span></span> <span data-ttu-id="1c89a-141">Cette applet de commande gère les résultats composé de plusieurs pages, puis envoie ces pipeline PowerShell de toohello résultats.</span><span class="sxs-lookup"><span data-stu-id="1c89a-141">This cmdlet handles multi-paged results, and then sends those results toohello PowerShell pipeline.</span></span> 

 ![Portail Azure](./media/active-directory-report-api-with-certificates/script-completed.png)

<span data-ttu-id="1c89a-143">Vous êtes maintenant prêt tooexport tooa volume partagé de cluster et que vous enregistrez tooa SIEM système.</span><span class="sxs-lookup"><span data-stu-id="1c89a-143">You are now ready tooexport tooa CSV and save tooa SIEM system.</span></span> <span data-ttu-id="1c89a-144">Vous pouvez également encapsuler votre script dans une tâche planifiée de tooget données Azure AD à partir de votre client régulièrement sans avoir des clés de l’application toostore dans le code source de hello.</span><span class="sxs-lookup"><span data-stu-id="1c89a-144">You can also wrap your script in a scheduled task tooget Azure AD data from your tenant periodically without having toostore application keys in hello source code.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1c89a-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1c89a-145">Next steps</span></span>
[<span data-ttu-id="1c89a-146">Notions de base Hello de gestion des identités de Azure</span><span class="sxs-lookup"><span data-stu-id="1c89a-146">hello fundamentals of Azure identity management</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity)<br>



