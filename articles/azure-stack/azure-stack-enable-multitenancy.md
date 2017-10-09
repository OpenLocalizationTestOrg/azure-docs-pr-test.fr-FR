---
title: "architecture mutualisée dans Azure pile aaaEnable | Documents Microsoft"
description: "Découvrez comment toosupport plusieurs annuaires Azure Active Directory dans la pile de Azure"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: helaw
ms.openlocfilehash: d7e404894a65f6786c42c5c27f76d46f353cb8c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-multi-tenancy-in-azure-stack"></a><span data-ttu-id="71d39-103">Activer l’architecture multilocataire dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="71d39-103">Enable multi-tenancy in Azure Stack</span></span>

<span data-ttu-id="71d39-104">Vous pouvez configurer les utilisateurs toosupport de pile de Azure à partir de plusieurs services toouse de locataires Azure Active Directory (Azure AD) dans la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="71d39-104">You can configure Azure Stack toosupport users from multiple Azure Active Directory (Azure AD) tenants toouse services in Azure Stack.</span></span> <span data-ttu-id="71d39-105">Par exemple, considérez hello scénario :</span><span class="sxs-lookup"><span data-stu-id="71d39-105">As an example, consider hello following scenario:</span></span>

 - <span data-ttu-id="71d39-106">Vous êtes hello administrateur du Service de contoso.onmicrosoft.com, où la pile de Azure est installé.</span><span class="sxs-lookup"><span data-stu-id="71d39-106">You are hello Service Administrator of contoso.onmicrosoft.com, where Azure Stack is installed.</span></span>
 - <span data-ttu-id="71d39-107">Mary est hello administrateur d’annuaire de fabrikam.onmicrosoft.com, dans lequel se trouvent les utilisateurs invités.</span><span class="sxs-lookup"><span data-stu-id="71d39-107">Mary is hello Directory Administrator of fabrikam.onmicrosoft.com, where guest users are located.</span></span> 
 - <span data-ttu-id="71d39-108">Société de Mary reçoit des services IaaS et PaaS à partir de votre entreprise et doit tooallow hello invité active (fabrikam.onmicrosoft.com) toosign dans utilisateurs et utilise des ressources de la pile d’Azure dans contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="71d39-108">Mary's company receives IaaS and PaaS services from your company, and needs tooallow users from hello guest directory (fabrikam.onmicrosoft.com) toosign in and use Azure Stack resources in contoso.onmicrosoft.com.</span></span>

<span data-ttu-id="71d39-109">Ce guide fournit les étapes hello requis dans le contexte de hello de ce scénario, tooconfigure une architecture mutualisée de pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="71d39-109">This guide provides hello steps required, in hello context of this scenario, tooconfigure multi-tenancy in Azure Stack.</span></span>  <span data-ttu-id="71d39-110">Dans ce scénario, vous Mary doit effectuer les étapes que l’utilisateur à partir de toosign Fabrikam dans tooenable et consommer des services à partir de hello déploiement Azure pile de Contoso.</span><span class="sxs-lookup"><span data-stu-id="71d39-110">In this scenario, you and Mary must complete steps tooenable users from Fabrikam toosign in and consume services from hello Azure Stack deployment in Contoso.</span></span>  

## <a name="before-you-begin"></a><span data-ttu-id="71d39-111">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="71d39-111">Before you begin</span></span>
<span data-ttu-id="71d39-112">Il existe quelques tooaccount de conditions préalables pour avant de configurer une architecture mutualisée de pile de Azure :</span><span class="sxs-lookup"><span data-stu-id="71d39-112">There are a few pre-requisites tooaccount for before you configure multi-tenancy in Azure Stack:</span></span>
  
 - <span data-ttu-id="71d39-113">Vous Mary doit coordonner des étapes administratives sur les deux annuaires hello Azure pile est installé dans (Contoso) et hello active de l’invité (Fabrikam).</span><span class="sxs-lookup"><span data-stu-id="71d39-113">You and Mary must coordinate administrative steps across both hello directory Azure Stack is installed in (Contoso), and hello guest directory (Fabrikam).</span></span>  
 - <span data-ttu-id="71d39-114">Vérifiez que vous avez [installé](azure-stack-powershell-install.md) et [configuré](azure-stack-powershell-configure-admin.md) PowerShell pour Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="71d39-114">Make sure you've [installed](azure-stack-powershell-install.md) and [configured](azure-stack-powershell-configure-admin.md) PowerShell for Azure Stack.</span></span>
 - <span data-ttu-id="71d39-115">[Télécharger les outils de pile Azure hello](azure-stack-powershell-download.md)et importer des modules de se connecter et d’identité hello :</span><span class="sxs-lookup"><span data-stu-id="71d39-115">[Download hello Azure Stack Tools](azure-stack-powershell-download.md), and import hello Connect and Identity modules:</span></span>

    ````PowerShell
        Import-Module .\Connect\AzureStack.Connect.psm1
        Import-Module .\Identity\AzureStack.Identity.psm1
    ```` 
 - <span data-ttu-id="71d39-116">Mary nécessitera [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) tooAzure pile d’accès.</span><span class="sxs-lookup"><span data-stu-id="71d39-116">Mary will require [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) access tooAzure Stack.</span></span> 

## <a name="configure-azure-stack-directory"></a><span data-ttu-id="71d39-117">Configurer l’annuaire Azure Stack</span><span class="sxs-lookup"><span data-stu-id="71d39-117">Configure Azure Stack directory</span></span>
<span data-ttu-id="71d39-118">Dans cette section, vous configurez Azure pile tooallow les connexions depuis des clients d’annuaire Azure AD de Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="71d39-118">In this section, you configure Azure Stack tooallow sign-ins from Fabrikam Azure AD directory tenants.</span></span>

### <a name="onboard-guest-directory-tenant"></a><span data-ttu-id="71d39-119">Intégrer le locataire d’annuaire invité</span><span class="sxs-lookup"><span data-stu-id="71d39-119">Onboard guest directory tenant</span></span>
<span data-ttu-id="71d39-120">TooAzure du locataire d’annuaire invité (Fabrikam) suivant, intégrer hello pile.</span><span class="sxs-lookup"><span data-stu-id="71d39-120">Next, onboard hello Guest Directory Tenant (Fabrikam) tooAzure Stack.</span></span>  <span data-ttu-id="71d39-121">Cette étape configure le Gestionnaire de ressources Azure tooaccept utilisateurs et principaux de service à partir du locataire d’annuaire hello invité.</span><span class="sxs-lookup"><span data-stu-id="71d39-121">This step configures Azure Resource Manager tooaccept users and service principals from hello guest directory tenant.</span></span>

````PowerShell
$adminARMEndpoint = "https://adminmanagement.local.azurestack.external"

## Replace hello value below with hello Azure Stack directory
$azureStackDirectoryTenant = "contoso.onmicrosoft.com"

## Replace hello value below with hello guest tenant directory. 
$guestDirectoryTenantToBeOnboarded = "fabrikam.onmicrosoft.com"

Register-AzSGuestDirectoryTenant -AdminResourceManagerEndpoint $adminARMEndpoint `
 -DirectoryTenantName $azureStackDirectoryTenant `
 -GuestDirectoryTenantName $guestDirectoryTenantToBeOnboarded `
 -Location "local"
````



## <a name="configure-guest-directory"></a><span data-ttu-id="71d39-122">Configurer l’annuaire invité</span><span class="sxs-lookup"><span data-stu-id="71d39-122">Configure guest directory</span></span>
<span data-ttu-id="71d39-123">Après avoir terminé les étapes décrites dans le répertoire de pile de Azure hello, Mary doit fournir son consentement tooAzure pile accès hello invité annuaire et Azure pile auprès active d’invité hello.</span><span class="sxs-lookup"><span data-stu-id="71d39-123">After you complete steps in hello Azure Stack directory, Mary must provide consent tooAzure Stack accessing hello guest directory and register Azure Stack with hello guest directory.</span></span> 

### <a name="registering-azure-stack-with-hello-guest-directory"></a><span data-ttu-id="71d39-124">L’inscription de la pile d’Azure avec le répertoire d’invité hello</span><span class="sxs-lookup"><span data-stu-id="71d39-124">Registering Azure Stack with hello guest directory</span></span>
<span data-ttu-id="71d39-125">Une fois que l’administrateur d’annuaire hello invité a fourni le consentement pour le répertoire de la pile de Azure tooaccess Fabrikam, ils doivent s’inscrire à Azure pile de locataire d’annuaire de Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="71d39-125">Once hello guest directory administrator has provided consent for Azure Stack tooaccess Fabrikam's directory, they must register Azure Stack with Fabrikam's directory tenant.</span></span>

````PowerShell
$tenantARMEndpoint = "https://management.local.azurestack.external"
    
## Replace hello value below with hello guest tenant directory. 
$guestDirectoryTenantName = "fabrikam.onmicrosoft.com"

Register-AzSWithMyDirectoryTenant `
 -TenantResourceManagerEndpoint $tenantARMEndpoint `
 -DirectoryTenantName $guestDirectoryTenantName ` 
 -Verbose 
````
## <a name="direct-users-toosign-in"></a><span data-ttu-id="71d39-126">Toosign de diriger les utilisateurs dans</span><span class="sxs-lookup"><span data-stu-id="71d39-126">Direct users toosign in</span></span>
<span data-ttu-id="71d39-127">Maintenant que vous et Mary terminées active de hello étapes tooonboard Mary, Mary peut diriger toosign les utilisateurs de Fabrikam dans.</span><span class="sxs-lookup"><span data-stu-id="71d39-127">Now that you and Mary have completed hello steps tooonboard Mary's directory, Mary can direct Fabrikam users toosign in.</span></span>  <span data-ttu-id="71d39-128">Les utilisateurs de Fabrikam (autrement dit, les utilisateurs avec le suffixe de fabrikam.onmicrosoft.com hello) se connectent en visitant https://portal.local.azurestack.external.</span><span class="sxs-lookup"><span data-stu-id="71d39-128">Fabrikam users (that is, users with hello fabrikam.onmicrosoft.com suffix) sign in by visiting https://portal.local.azurestack.external.</span></span>  

<span data-ttu-id="71d39-129">Mary dirigera les [étrangère principaux](../active-directory/active-directory-understanding-resource-access.md) dans toosign de répertoire (autrement dit, les utilisateurs dans le répertoire de Fabrikam hello sans suffixe hello fabrikam.onmicrosoft.com) hello Fabrikam à l’aide de https://portal.local.azurestack.external/fabrikam.onmicrosoft.com.  Si elles n’utilisent pas cette URL, ils sont envoyés de répertoire par défaut de tootheir (Fabrikam) et vous recevez une erreur indiquant que leur administrateur n’a pas donné son consentement.</span><span class="sxs-lookup"><span data-stu-id="71d39-129">Mary will direct any [foreign principals](../active-directory/active-directory-understanding-resource-access.md) in hello Fabrikam directory (that is, users in hello Fabrikam directory without hello suffix of fabrikam.onmicrosoft.com) toosign in using https://portal.local.azurestack.external/fabrikam.onmicrosoft.com.  If they do not use this URL, they are sent tootheir default directory (Fabrikam) and receive an error that says their admin has not consented.</span></span>

## <a name="next-steps"></a><span data-ttu-id="71d39-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="71d39-130">Next Steps</span></span>

- [<span data-ttu-id="71d39-131">Gérer les fournisseurs délégués</span><span class="sxs-lookup"><span data-stu-id="71d39-131">Manage delegated providers</span></span>](azure-stack-delegated-provider.md)
- [<span data-ttu-id="71d39-132">Concepts clés d’Azure Stack</span><span class="sxs-lookup"><span data-stu-id="71d39-132">Azure Stack key concepts</span></span>](azure-stack-key-features.md)
