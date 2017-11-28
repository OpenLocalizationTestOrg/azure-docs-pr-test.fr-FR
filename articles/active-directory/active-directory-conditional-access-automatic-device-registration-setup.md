---
title: "Configuration de l’inscription automatique auprès d’Azure Active Directory d’appareils Windows joints à un domaine | Microsoft Docs"
description: "Configurez vos appareils Windows joints à un domaine pour les inscrire automatiquement et en mode silencieux auprès d’Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: dccd7df6a5f85df4179c7ea7cfc476cfb57f48c0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-automatic-registration-of-windows-domain-joined-devices-with-azure-active-directory"></a><span data-ttu-id="d8ee0-103">Configuration de l’inscription automatique auprès d’Azure Active Directory d’appareils Windows joints à un domaine</span><span class="sxs-lookup"><span data-stu-id="d8ee0-103">How to configure automatic registration of Windows domain-joined devices with Azure Active Directory</span></span>

<span data-ttu-id="d8ee0-104">Pour utiliser [l’accès conditionnel à Azure Active Directory en fonction de l’appareil](active-directory-conditional-access-azure-portal.md), vos ordinateurs doivent être inscrits auprès d’Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d8ee0-104">To use [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md), your computers must be registered with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="d8ee0-105">Vous pouvez obtenir la liste des appareils inscrits dans votre organisation en utilisant l’applet de commande [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) dans le [module Azure Active Directory PowerShell](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="d8ee0-105">You can get a list of registered devices in your organization by using the [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in the [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span> 

<span data-ttu-id="d8ee0-106">Cet article vous présente les étapes de configuration de l’inscription automatique auprès d’Azure Active Directory d’appareils Windows joints à un domaine dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-106">This article provides you with the steps for configuring the automatic registration of Windows domain-joined devices with Azure AD in your organization.</span></span>


<span data-ttu-id="d8ee0-107">Le cas échéant, consultez les références suivantes :</span><span class="sxs-lookup"><span data-stu-id="d8ee0-107">For more information about:</span></span>

- <span data-ttu-id="d8ee0-108">Pour plus d’informations sur l’accès conditionnel, consultez l’article [Accès conditionnel dans Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d8ee0-108">Conditional access, see [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md).</span></span> 
- <span data-ttu-id="d8ee0-109">Pour plus d’informations sur les appareils Windows 10 dans l’espace de travail et sur les expériences améliorées après inscription auprès d’Azure AD, consultez l’article [Windows 10 pour l’entreprise : plusieurs manières d’utiliser des appareils professionnels](active-directory-azureadjoin-windows10-devices-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d8ee0-109">Windows 10 devices in the workplace and the enhanced experiences when registered with Azure AD, see [Windows 10 for the enterprise: Use devices for work](active-directory-azureadjoin-windows10-devices-overview.md).</span></span>
- <span data-ttu-id="d8ee0-110">Windows 10 Entreprise E3 dans CSP. Consultez la [Vue d’ensemble de Windows 10 Entreprise E3 dans CSP](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).</span><span class="sxs-lookup"><span data-stu-id="d8ee0-110">Windows 10 Enterprise E3 in CSP, see the [Windows 10 Enterprise E3 in CSP Overview](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="d8ee0-111">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="d8ee0-111">Before you begin</span></span>

<span data-ttu-id="d8ee0-112">Avant de commencer à configurer l’inscription automatique des appareils Windows joints à un domaine dans votre environnement, vous devez vous familiariser avec les scénarios pris en charge et avec les contraintes.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-112">Before you start configuring the automatic registration of Windows domain-joined devices in your environment, you should familiarize yourself with the supported scenarios and the constraints.</span></span>  

<span data-ttu-id="d8ee0-113">Pour améliorer la lisibilité des descriptions, cet article utilise les termes suivants :</span><span class="sxs-lookup"><span data-stu-id="d8ee0-113">To improve the readability of the descriptions, this topic uses the following term:</span></span> 

- <span data-ttu-id="d8ee0-114">**Appareils Windows actuels** : ce terme désigne les appareils joints à un domaine qui exécutent Windows 10 ou Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-114">**Windows current devices** - This term refers to domain-joined devices running Windows 10 or Windows Server 2016.</span></span>
- <span data-ttu-id="d8ee0-115">**Appareils Windows de bas niveau** : ce terme fait référence à tous les appareils Windows joints à un domaine **pris en charge** qui n’exécutent ni Windows 10 ni Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-115">**Windows down-level devices** - This term refers to all **supported** domain-joined Windows devices that are neither running Windows 10 nor Windows Server 2016.</span></span>  


### <a name="windows-current-devices"></a><span data-ttu-id="d8ee0-116">Appareils Windows actuels</span><span class="sxs-lookup"><span data-stu-id="d8ee0-116">Windows current devices</span></span>

- <span data-ttu-id="d8ee0-117">Pour les appareils qui exécutent le système d’exploitation d’ordinateur Windows, nous recommandons d’utiliser Mise à jour anniversaire Windows 10 (version 1607) ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-117">For devices running the Windows desktop operating system, we recommend using Windows 10 Anniversary Update (version 1607) or later.</span></span> 
- <span data-ttu-id="d8ee0-118">L’inscription des appareils Windows actuels **est** prise en charge dans les environnements non fédérés tels que les configurations de synchronisation du hachage de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-118">The registration of Windows current devices **is** supported in non-federated environments such as password hash sync configurations.</span></span>  


### <a name="windows-down-level-devices"></a><span data-ttu-id="d8ee0-119">Appareils Windows de bas niveau</span><span class="sxs-lookup"><span data-stu-id="d8ee0-119">Windows down-level devices</span></span>

- <span data-ttu-id="d8ee0-120">Les appareils Windows de bas niveau pris en charge sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="d8ee0-120">The following Windows down-level devices are supported:</span></span>
    - <span data-ttu-id="d8ee0-121">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="d8ee0-121">Windows 8.1</span></span>
    - <span data-ttu-id="d8ee0-122">Windows 7</span><span class="sxs-lookup"><span data-stu-id="d8ee0-122">Windows 7</span></span>
    - <span data-ttu-id="d8ee0-123">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="d8ee0-123">Windows Server 2012 R2</span></span>
    - <span data-ttu-id="d8ee0-124">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="d8ee0-124">Windows Server 2012</span></span>
    - <span data-ttu-id="d8ee0-125">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="d8ee0-125">Windows Server 2008 R2</span></span>
- <span data-ttu-id="d8ee0-126">L’inscription d’appareils de bas niveau Windows **est** prise en charge dans les environnements non fédérés via l’authentification unique transparente [Authentification unique transparente d’Azure Active Directory](https://aka.ms/hybrid/sso).</span><span class="sxs-lookup"><span data-stu-id="d8ee0-126">The registration of Windows down-level devices **is** supported in non-federated environments through Seamless Single Sign On [Azure Active Directory Seamless Single Sign-On](https://aka.ms/hybrid/sso).</span></span>
- <span data-ttu-id="d8ee0-127">L’inscription des appareils Windows de bas niveau **n’est pas** prise en charge pour les appareils utilisant des profils d’itinérance.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-127">The registration of Windows down-level devices **is not** supported for devices using roaming profiles.</span></span> <span data-ttu-id="d8ee0-128">Si vous vous appuyez sur l’itinérance de profils ou de paramètres, utilisez Windows 10.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-128">If you are relying on roaming of profiles or settings, use Windows 10.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="d8ee0-129">Prérequis</span><span class="sxs-lookup"><span data-stu-id="d8ee0-129">Prerequisites</span></span>

<span data-ttu-id="d8ee0-130">Avant de commencer à activer l’inscription automatique d’appareils joints à un domaine dans votre organisation, vous devez vous assurer que vous exécutez une version à jour d’Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-130">Before you start enabling the auto-registration of domain-joined devices in your organization, you need to make sure that you are running an up-to-date version of Azure AD connect.</span></span>

<span data-ttu-id="d8ee0-131">Azure AD Connect :</span><span class="sxs-lookup"><span data-stu-id="d8ee0-131">Azure AD Connect:</span></span>

- <span data-ttu-id="d8ee0-132">Conserve l’association entre le compte d’ordinateur dans votre service Active Directory (AD) local et l’objet appareil dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-132">Keeps the association between the computer account in your on-premises Active Directory (AD) and the device object in Azure AD.</span></span> 
- <span data-ttu-id="d8ee0-133">Permet d’utiliser d’autres fonctionnalités liées aux appareils telles que Windows Hello Entreprise.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-133">Enables other device related features like Windows Hello for Business.</span></span>



## <a name="configuration-steps"></a><span data-ttu-id="d8ee0-134">Configuration</span><span class="sxs-lookup"><span data-stu-id="d8ee0-134">Configuration steps</span></span>

<span data-ttu-id="d8ee0-135">Cet article inclut les étapes requises pour tous les scénarios de configuration classiques.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-135">This topic includes the required steps for all typical configuration scenarios.</span></span>  
<span data-ttu-id="d8ee0-136">Pour obtenir une vue d’ensemble des étapes requises par votre scénario, utilisez le tableau ci-après :</span><span class="sxs-lookup"><span data-stu-id="d8ee0-136">Use the following table to get an overview of the steps that are required for your scenario:</span></span>  



| <span data-ttu-id="d8ee0-137">Étapes</span><span class="sxs-lookup"><span data-stu-id="d8ee0-137">Steps</span></span>                                      | <span data-ttu-id="d8ee0-138">Appareils Windows actuels et synchronisation du hachage de mot de passe</span><span class="sxs-lookup"><span data-stu-id="d8ee0-138">Windows current and password hash sync</span></span> | <span data-ttu-id="d8ee0-139">Appareils Windows actuels et fédération</span><span class="sxs-lookup"><span data-stu-id="d8ee0-139">Windows current and federation</span></span> | <span data-ttu-id="d8ee0-140">Appareils Windows de bas niveau</span><span class="sxs-lookup"><span data-stu-id="d8ee0-140">Windows down-level</span></span> |
| :--                                        | :-:                                    | :-:                            | :-:                |
| <span data-ttu-id="d8ee0-141">Étape 1 : Configuration du point de connexion de service</span><span class="sxs-lookup"><span data-stu-id="d8ee0-141">Step 1: Configure service connection point</span></span> | ![Vérification][1]                            | ![Vérification][1]                    | ![Vérification][1]        |
| <span data-ttu-id="d8ee0-145">Étape 2 : Configuration de l’émission de revendications</span><span class="sxs-lookup"><span data-stu-id="d8ee0-145">Step 2: Setup issuance of claims</span></span>           |                                        | ![Vérification][1]                    | ![Vérification][1]        |
| <span data-ttu-id="d8ee0-148">Étape 3 : Activation d’appareils non-Windows 10</span><span class="sxs-lookup"><span data-stu-id="d8ee0-148">Step 3: Enable non-Windows 10 devices</span></span>      |                                        |                                | ![Vérification][1]        |
| <span data-ttu-id="d8ee0-150">Étape 4 : Contrôle du déploiement et du lancement</span><span class="sxs-lookup"><span data-stu-id="d8ee0-150">Step 4: Control deployment and rollout</span></span>     | ![Vérification][1]                            | ![Vérification][1]                    | ![Vérification][1]        |
| <span data-ttu-id="d8ee0-154">Étape 5 : Vérification des appareils inscrits</span><span class="sxs-lookup"><span data-stu-id="d8ee0-154">Step 5: Verify registered devices</span></span>          | ![Vérification][1]                            | ![Vérification][1]                    | ![Vérification][1]        |



## <a name="step-1-configure-service-connection-point"></a><span data-ttu-id="d8ee0-158">Étape 1 : Configuration du point de connexion de service</span><span class="sxs-lookup"><span data-stu-id="d8ee0-158">Step 1: Configure service connection point</span></span>

<span data-ttu-id="d8ee0-159">Vos appareils utilisent l’objet point de connexion de service (SCP) lors de l’inscription pour détecter les informations de client Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-159">The service connection point (SCP) object is used by your devices during the registration to discover Azure AD tenant information.</span></span> <span data-ttu-id="d8ee0-160">Dans votre service Active Directory (AD) local, l’objet SCP pour l’inscription automatique des appareils joints à un domaine doit exister dans la partition de contexte d’appellation de configuration de la forêt de l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-160">In your on-premises Active Directory (AD), the SCP object for the auto-registration of domain-joined devices must exist in the configuration naming context partition of the computer's forest.</span></span> <span data-ttu-id="d8ee0-161">Il n’existe qu’un seul contexte d’appellation de configuration par forêt.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-161">There is only one configuration naming context per forest.</span></span> <span data-ttu-id="d8ee0-162">Dans une configuration Active Directory à forêts multiples, le point de connexion de service doit exister dans toutes les forêts qui contiennent des ordinateurs joints à un domaine.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-162">In a multi-forest Active Directory configuration, the service connection point must exist in all forests containing domain-joined computers.</span></span>

<span data-ttu-id="d8ee0-163">Pour récupérer le contexte d’appellation de configuration de votre forêt, vous pouvez utiliser l’applet de commande [**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx).</span><span class="sxs-lookup"><span data-stu-id="d8ee0-163">You can use the [**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx) cmdlet to retrieve the configuration naming context of your forest.</span></span>  

<span data-ttu-id="d8ee0-164">Pour une forêt avec le nom de domaine Active Directory *fabrikam.com*, le contexte d’appellation de configuration est le suivant :</span><span class="sxs-lookup"><span data-stu-id="d8ee0-164">For a forest with the Active Directory domain name *fabrikam.com*, the configuration naming context is:</span></span>

`CN=Configuration,DC=fabrikam,DC=com`

<span data-ttu-id="d8ee0-165">Dans votre forêt, l’objet SCP pour l’inscription automatique des appareils joints à un domaine se trouve à l’emplacement suivant :</span><span class="sxs-lookup"><span data-stu-id="d8ee0-165">In your forest, the SCP object for the auto-registration of domain-joined devices is located at:</span></span>  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

<span data-ttu-id="d8ee0-166">Selon la façon dont vous avez déployé Azure AD Connect, il est possible que l’objet SCP ait déjà été configuré.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-166">Depending on how you have deployed Azure AD Connect, the SCP object may have already been configured.</span></span>
<span data-ttu-id="d8ee0-167">Vous pouvez vérifier l’existence de l’objet et récupérer les valeurs de détection à l’aide du script Windows PowerShell suivant :</span><span class="sxs-lookup"><span data-stu-id="d8ee0-167">You can verify the existence of the object and retrieve the discovery values using the following Windows PowerShell script:</span></span> 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

<span data-ttu-id="d8ee0-168">La sortie de **$scp.Keywords** présente les informations de client Azure AD, par exemple :</span><span class="sxs-lookup"><span data-stu-id="d8ee0-168">The **$scp.Keywords** output shows the Azure AD tenant information, for example:</span></span>

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

<span data-ttu-id="d8ee0-169">Si le point de connexion de service n’existe pas, vous pouvez le créer en exécutant l’applet de commande `Initialize-ADSyncDomainJoinedComputerSync` sur votre serveur Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-169">If the service connection point does not exist, you can create it by running the `Initialize-ADSyncDomainJoinedComputerSync` cmdlet on your Azure AD Connect server.</span></span> <span data-ttu-id="d8ee0-170">Des informations d’identification d’administrateur d’entreprise sont requises pour exécuter cette applet de commande.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-170">Enterprise admin credential is required to run this cmdlet.</span></span>  
<span data-ttu-id="d8ee0-171">Cette applet de commande :</span><span class="sxs-lookup"><span data-stu-id="d8ee0-171">The cmdlet:</span></span>

- <span data-ttu-id="d8ee0-172">Crée le point de connexion de service dans la forêt Active Directory à laquelle Azure AD Connect est connecté.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-172">Creates the service connection point in the Active Directory forest Azure AD Connect is connected to.</span></span> 
- <span data-ttu-id="d8ee0-173">Vous demande de spécifier le paramètre `AdConnectorAccount`.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-173">Requires you to specify the `AdConnectorAccount` parameter.</span></span> <span data-ttu-id="d8ee0-174">Il s’agit du compte configuré en tant que compte de connecteur Active Directory dans Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-174">This is the account that is configured as Active Directory connector account in Azure AD connect.</span></span> 


<span data-ttu-id="d8ee0-175">Le script ci-après présente un exemple d’utilisation de l’applet de commande.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-175">The following script shows an example for using the cmdlet.</span></span> <span data-ttu-id="d8ee0-176">Dans ce script, la chaîne `$aadAdminCred = Get-Credential` exige que vous tapiez un nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-176">In this script, `$aadAdminCred = Get-Credential` requires you to type a user name.</span></span> <span data-ttu-id="d8ee0-177">Vous devez indiquer le nom d’utilisateur au format de nom d’utilisateur principal (UPN) (`user@example.com`).</span><span class="sxs-lookup"><span data-stu-id="d8ee0-177">You need to provide the user name in the user principal name (UPN) format (`user@example.com`).</span></span> 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

<span data-ttu-id="d8ee0-178">L’applet de commande `Initialize-ADSyncDomainJoinedComputerSync` :</span><span class="sxs-lookup"><span data-stu-id="d8ee0-178">The `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span></span>

- <span data-ttu-id="d8ee0-179">utilise le module Active Directory PowerShell qui s’appuie sur les services Web Active Directory s’exécutant sur un contrôleur de domaine.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-179">Uses the Active Directory PowerShell module, which relies on Active Directory Web Services running on a domain controller.</span></span> <span data-ttu-id="d8ee0-180">Les services Web Active Directory sont pris en charge sur les contrôleurs de domaine exécutant Windows Server 2008 R2 et les versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-180">Active Directory Web Services is supported on domain controllers running Windows Server 2008 R2 and later.</span></span>
- <span data-ttu-id="d8ee0-181">Est pris en charge seulement par le **module MSOnline PowerShell version 1.1.166.0**.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-181">Is only supported by the **MSOnline PowerShell module version 1.1.166.0**.</span></span> <span data-ttu-id="d8ee0-182">Pour télécharger ce module, utilisez ce [lien](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span><span class="sxs-lookup"><span data-stu-id="d8ee0-182">To download this module, use this [link](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span></span>   

<span data-ttu-id="d8ee0-183">Pour les contrôleurs de domaine exécutant Windows Server 2008 ou des versions antérieures, utilisez le script ci-après pour créer le point de connexion de service.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-183">For domain controllers running Windows Server 2008 or earlier versions, use the script below to create the service connection point.</span></span>

<span data-ttu-id="d8ee0-184">Dans une configuration à forêts multiples, vous devez utiliser le script ci-dessous pour créer le point de connexion de service dans chacune des forêts contenant des ordinateurs :</span><span class="sxs-lookup"><span data-stu-id="d8ee0-184">In a multi-forest configuration, you should use the following script to create the service connection point in each forest where computers exist:</span></span>
 
    $verifiedDomain = "contoso.com"    # Replace this with any of your verified domain names in Azure AD
    $tenantID = "72f988bf-86f1-41af-91ab-2d7cd011db47"    # Replace this with you tenant ID
    $configNC = "CN=Configuration,DC=corp,DC=contoso,DC=com"    # Replace this with your AD configuration naming context

    $de = New-Object System.DirectoryServices.DirectoryEntry
    $de.Path = "LDAP://CN=Services," + $configNC

    $deDRC = $de.Children.Add("CN=Device Registration Configuration", "container")
    $deDRC.CommitChanges()

    $deSCP = $deDRC.Children.Add("CN=62a0ff2e-97b9-4513-943f-0d221bd30080", "serviceConnectionPoint")
    $deSCP.Properties["keywords"].Add("azureADName:" + $verifiedDomain)
    $deSCP.Properties["keywords"].Add("azureADId:" + $tenantID)

    $deSCP.CommitChanges()


## <a name="step-2-setup-issuance-of-claims"></a><span data-ttu-id="d8ee0-185">Étape 2 : Configuration de l’émission de revendications</span><span class="sxs-lookup"><span data-stu-id="d8ee0-185">Step 2: Setup issuance of claims</span></span>

<span data-ttu-id="d8ee0-186">Dans une configuration Azure AD fédérée, les appareils s’appuient sur les services de fédération Active Directory (AD FS) ou sur un service de fédération local tiers pour s’authentifier auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-186">In a federated Azure AD configuration, devices rely on Active Directory Federation Services (AD FS) or a 3rd party on-premises federation service to authenticate to Azure AD.</span></span> <span data-ttu-id="d8ee0-187">Les appareils s’authentifient pour obtenir un jeton d’accès afin de s’inscrire auprès du service Azure Active Directory Device Registration Service (Azure DRS).</span><span class="sxs-lookup"><span data-stu-id="d8ee0-187">Devices authenticate to get an access token to register against the Azure Active Directory Device Registration Service (Azure DRS).</span></span>

<span data-ttu-id="d8ee0-188">Les appareils Windows actuels s’authentifient à l’aide de l’authentification Windows intégrée auprès d’un point de terminaison WS-Trust actif (version 1.3 ou 2005) hébergé par le service de fédération local.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-188">Windows current devices authenticate using Integrated Windows Authentication to an active WS-Trust endpoint (either 1.3 or 2005 versions) hosted by the on-premises federation service.</span></span>

> [!NOTE]
> <span data-ttu-id="d8ee0-189">En cas d’utilisation d’AD FS, il est nécessaire d’activer **adfs/services/trust/13/windowstransport** ou **adfs/services/trust/2005/windowstransport**.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-189">When using AD FS, either **adfs/services/trust/13/windowstransport** or **adfs/services/trust/2005/windowstransport** must be enabled.</span></span> <span data-ttu-id="d8ee0-190">Si vous utilisez le proxy d’authentification web, vérifiez également que ce point de terminaison est publié via le proxy.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-190">If you are using the Web Authentication Proxy, also ensure that this endpoint is published through the proxy.</span></span> <span data-ttu-id="d8ee0-191">Vous pouvez visualiser les points de terminaison qui sont activés par le biais de la console de gestion AD FS sous **Service > Points de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-191">You can see what end-points are enabled through the AD FS management console under **Service > Endpoints**.</span></span>
>
><span data-ttu-id="d8ee0-192">Si vous n’utilisez pas AD FS en tant que service de fédération local, suivez les instructions de votre fournisseur pour vous assurer que celui-ci prend en charge les points de terminaison WS-Trust 1.3 ou 2005 et que ces derniers sont publiés par le biais du fichier Metadata Exchange (MEX).</span><span class="sxs-lookup"><span data-stu-id="d8ee0-192">If you don’t have AD FS as your on-premises federation service, follow the instructions of your vendor to make sure they support WS-Trust 1.3 or 2005 end-points and that these are published through the Metadata Exchange file (MEX).</span></span>

<span data-ttu-id="d8ee0-193">Pour que l’inscription d’appareils puisse s’effectuer, les revendications ci-après doivent exister dans le jeton reçu par Azure DRS.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-193">The following claims must exist in the token received by Azure DRS for device registration to complete.</span></span> <span data-ttu-id="d8ee0-194">Azure DRS crée un objet appareil dans Azure AD avec certaines de ces informations, qu’Azure AD Connect utilise ensuite pour associer l’objet appareil nouvellement créé au compte d’ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-194">Azure DRS will create a device object in Azure AD with some of this information which is then used by Azure AD Connect to associate the newly created device object with the computer account on-premises.</span></span>

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

<span data-ttu-id="d8ee0-195">Si vous disposez de plusieurs noms de domaine vérifiés, vous devez fournir la revendication ci-après pour les ordinateurs :</span><span class="sxs-lookup"><span data-stu-id="d8ee0-195">If you have more than one verified domain name, you need to provide the following claim for computers:</span></span>

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

<span data-ttu-id="d8ee0-196">Si vous émettez déjà une revendication ImmutableID (par exemple, un ID de connexion alternatif), vous devez fournir une seule revendication correspondante pour les ordinateurs :</span><span class="sxs-lookup"><span data-stu-id="d8ee0-196">If you are already issuing an ImmutableID claim (e.g., alternate login ID) you need to provide one corresponding claim for computers:</span></span>

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

<span data-ttu-id="d8ee0-197">Dans les sections ci-après, vous trouverez des informations concernant :</span><span class="sxs-lookup"><span data-stu-id="d8ee0-197">In the following sections, you find information about:</span></span>
 
- <span data-ttu-id="d8ee0-198">Les valeurs requises pour chaque revendication</span><span class="sxs-lookup"><span data-stu-id="d8ee0-198">The values each claim should have</span></span>
- <span data-ttu-id="d8ee0-199">L’aspect d’une définition dans AD FS</span><span class="sxs-lookup"><span data-stu-id="d8ee0-199">How a definition would look like in AD FS</span></span>

<span data-ttu-id="d8ee0-200">La définition vous permet de vérifier si les valeurs sont présentes ou si vous devez les créer.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-200">The definition helps you to verify whether the values are present or if you need to create them.</span></span>

> [!NOTE]
> <span data-ttu-id="d8ee0-201">Si vous n’utilisez pas AD FS pour votre serveur de fédération local, suivez les instructions de votre fournisseur afin de créer la configuration appropriée pour l’émission de ces revendications.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-201">If you don’t use AD FS for your on-premises federation server, follow your vendor's instructions to create the appropriate configuration to issue these claims.</span></span>

### <a name="issue-account-type-claim"></a><span data-ttu-id="d8ee0-202">Émission de la revendication du type de compte</span><span class="sxs-lookup"><span data-stu-id="d8ee0-202">Issue account type claim</span></span>

<span data-ttu-id="d8ee0-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`** : cette revendication doit contenir la valeur **DJ**, qui identifie l’appareil en tant qu’ordinateur joint à un domaine.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`** - This claim must contain a value of **DJ**, which identifies the device as a domain-joined computer.</span></span> <span data-ttu-id="d8ee0-204">Dans AD FS, vous pouvez ajouter une règle de transformation d’émission ressemblant à ceci :</span><span class="sxs-lookup"><span data-stu-id="d8ee0-204">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

    @RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );

### <a name="issue-objectguid-of-the-computer-account-on-premises"></a><span data-ttu-id="d8ee0-205">Émission de la valeur ObjectGUID du compte d’ordinateur local</span><span class="sxs-lookup"><span data-stu-id="d8ee0-205">Issue objectGUID of the computer account on-premises</span></span>

<span data-ttu-id="d8ee0-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`** : cette revendication doit contenir la valeur **objectGUID** du compte d’ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`** - This claim must contain the **objectGUID** value of the on-premises computer account.</span></span> <span data-ttu-id="d8ee0-207">Dans AD FS, vous pouvez ajouter une règle de transformation d’émission ressemblant à ceci :</span><span class="sxs-lookup"><span data-stu-id="d8ee0-207">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

    @RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );
 
### <a name="issue-objectsid-of-the-computer-account-on-premises"></a><span data-ttu-id="d8ee0-208">Émission de la valeur objectSID du compte d’ordinateur local</span><span class="sxs-lookup"><span data-stu-id="d8ee0-208">Issue objectSID of the computer account on-premises</span></span>

<span data-ttu-id="d8ee0-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`** : cette revendication doit contenir la valeur **objectSid** du compte d’ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`** - This claim must contain the the **objectSid** value of the on-premises computer account.</span></span> <span data-ttu-id="d8ee0-210">Dans AD FS, vous pouvez ajouter une règle de transformation d’émission ressemblant à ceci :</span><span class="sxs-lookup"><span data-stu-id="d8ee0-210">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

    @RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a><span data-ttu-id="d8ee0-211">Émission de la valeur issuerID pour l’ordinateur s’il existe plusieurs noms de domaine vérifiés dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8ee0-211">Issue issuerID for computer when multiple verified domain names in Azure AD</span></span>

<span data-ttu-id="d8ee0-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`** : cette revendication doit contenir l’URI (Uniform Resource Identifier) des noms de domaine vérifiés qui se connectent avec le service de fédération local (AD FS ou tiers) émettant le jeton.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`** - This claim must contain the Uniform Resource Identifier (URI) of any of the verified domain names that connect with the on-premises federation service (AD FS or 3rd party) issuing the token.</span></span> <span data-ttu-id="d8ee0-213">Dans AD FS, vous pouvez ajouter des règles de transformation d’émission qui ressemblent à celles ci-dessous dans l’ordre indiqué après les règles mentionnées ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-213">In AD FS, you can add issuance transform rules that look like the ones below in that specific order after the ones above.</span></span> <span data-ttu-id="d8ee0-214">Notez qu’il doit exister une règle régissant l’émission explicite de la règle pour les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-214">Please note that one rule to explicitly issue the rule for users is necessary.</span></span> <span data-ttu-id="d8ee0-215">Dans les règles ci-dessous, une première règle est ajoutée afin d’identifier l’authentification d’un utilisateur plutôt que d’un ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-215">In the rules below, a first rule identifying user vs. computer authentication is added.</span></span>

    @RuleName = "Issue account type with the value User when its not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue the IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://<verified-domain-name>/adfs/services/trust/"
    );


<span data-ttu-id="d8ee0-216">Dans la revendication ci-dessus,</span><span class="sxs-lookup"><span data-stu-id="d8ee0-216">In the claim above,</span></span>

- <span data-ttu-id="d8ee0-217">`$<domain>` est l’URL des services AD FS</span><span class="sxs-lookup"><span data-stu-id="d8ee0-217">`$<domain>` is the AD FS service URL</span></span>
- <span data-ttu-id="d8ee0-218">`<verified-domain-name>` est un espace réservé que vous devez remplacer par un de vos noms de domaine vérifiés dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8ee0-218">`<verified-domain-name>` is a placeholder you need to replace with one of your verified domain names in Azure AD</span></span>



<span data-ttu-id="d8ee0-219">Pour plus d’informations sur la vérification du domaine, consultez [Ajouter un nom de domaine personnalisé à Azure Active Directory](active-directory-add-domain.md).</span><span class="sxs-lookup"><span data-stu-id="d8ee0-219">For more details about verified domain names, see [Add a custom domain name to Azure Active Directory](active-directory-add-domain.md).</span></span>  
<span data-ttu-id="d8ee0-220">Pour obtenir une liste de vos domaines d’entreprise vérifiés, vous pouvez utiliser l’applet de commande [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0).</span><span class="sxs-lookup"><span data-stu-id="d8ee0-220">To get a list of your verified company domains, you can use the [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span></span> 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a><span data-ttu-id="d8ee0-222">Émission de la valeur ImmutableID pour l’ordinateur s’il en existe une pour les utilisateurs (par exemple, définition d’un ID de connexion alternatif)</span><span class="sxs-lookup"><span data-stu-id="d8ee0-222">Issue ImmutableID for computer when one for users exist (e.g. alternate login ID is set)</span></span>

<span data-ttu-id="d8ee0-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** : cette revendication doit contenir une valeur valide pour les ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - This claim must contain a valid value for computers.</span></span> <span data-ttu-id="d8ee0-224">Dans AD FS, vous pouvez créer une règle de transformation d’émission comme suit :</span><span class="sxs-lookup"><span data-stu-id="d8ee0-224">In AD FS, you can create an issuance transform rule as follows:</span></span>

    @RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );

### <a name="helper-script-to-create-the-ad-fs-issuance-transform-rules"></a><span data-ttu-id="d8ee0-225">Script d’assistance pour la création des règles de transformation d’émission AD FS</span><span class="sxs-lookup"><span data-stu-id="d8ee0-225">Helper script to create the AD FS issuance transform rules</span></span>

<span data-ttu-id="d8ee0-226">Le script ci-après vous aide à créer les règles de transformation d’émission décrites ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-226">The following script helps you with the creation of the issuance transform rules described above.</span></span>

    $multipleVerifiedDomainNames = $false
    $immutableIDAlreadyIssuedforUsers = $false
    $oneOfVerifiedDomainNames = 'example.com'   # Replace example.com with one of your verified domains
    
    $rule1 = '@RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );'

    $rule2 = '@RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'

    $rule3 = '@RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);'

    $rule4 = ''
    if ($multipleVerifiedDomainNames -eq $true) {
    $rule4 = '@RuleName = "Issue account type with the value User when it is not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue the IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://' + $oneOfVerifiedDomainNames + '/adfs/services/trust/"
    );'
    }

    $rule5 = ''
    if ($immutableIDAlreadyIssuedforUsers -eq $true) {
    $rule5 = '@RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'
    }

    $existingRules = (Get-ADFSRelyingPartyTrust -Identifier urn:federation:MicrosoftOnline).IssuanceTransformRules 

    $updatedRules = $existingRules + $rule1 + $rule2 + $rule3 + $rule4 + $rule5

    $crSet = New-ADFSClaimRuleSet -ClaimRule $updatedRules 

    Set-AdfsRelyingPartyTrust -TargetIdentifier urn:federation:MicrosoftOnline -IssuanceTransformRules $crSet.ClaimRulesString 

### <a name="remarks"></a><span data-ttu-id="d8ee0-227">Remarques</span><span class="sxs-lookup"><span data-stu-id="d8ee0-227">Remarks</span></span> 

- <span data-ttu-id="d8ee0-228">Ce script ajoute les règles aux règles existantes.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-228">This script appends the rules to the existing rules.</span></span> <span data-ttu-id="d8ee0-229">N’exécutez pas le script à deux reprises, car l’ensemble de règles serait alors ajouté deux fois.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-229">Do not run the script twice because the set of rules would be added twice.</span></span> <span data-ttu-id="d8ee0-230">Avant de réexécuter le script, assurez-vous qu’il n’existe aucune règle correspondante pour ces revendications (sous les conditions associées).</span><span class="sxs-lookup"><span data-stu-id="d8ee0-230">Make sure that no corresponding rules exist for these claims (under the corresponding conditions) before running the script again.</span></span>

- <span data-ttu-id="d8ee0-231">Si vous disposez de plusieurs noms de domaine vérifiés (comme indiqué dans le portail Azure AD ou par le biais de l’applet de commande Get-MsolDomains), définissez l’élément **$multipleVerifiedDomainNames** du script sur la valeur **$true**.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-231">If you have multiple verified domain names (as shown in the Azure AD portal or via the Get-MsolDomains cmdlet), set the value of **$multipleVerifiedDomainNames** in the script to **$true**.</span></span> <span data-ttu-id="d8ee0-232">Veillez également à supprimer toute revendication issuerid existante pouvant avoir été créée par Azure AD Connect ou par d’autres moyens.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-232">Also make sure that you remove any existing issuerid claim that might have been created by Azure AD Connect or via other means.</span></span> <span data-ttu-id="d8ee0-233">Voici un exemple de cette règle :</span><span class="sxs-lookup"><span data-stu-id="d8ee0-233">Here is an example for this rule:</span></span>


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- <span data-ttu-id="d8ee0-234">Si vous avez déjà émis une revendication **ImmutableID** pour les comptes d’utilisateurs, définissez l’élément **$immutableIDAlreadyIssuedforUsers** du script sur la valeur **$true**.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-234">If you have already issued an **ImmutableID** claim  for user accounts, set the value of **$immutableIDAlreadyIssuedforUsers** in the script to **$true**.</span></span>

## <a name="step-3-enable-windows-down-level-devices"></a><span data-ttu-id="d8ee0-235">Étape 3 : Activation des appareils Windows de bas niveau</span><span class="sxs-lookup"><span data-stu-id="d8ee0-235">Step 3: Enable Windows down-level devices</span></span>

<span data-ttu-id="d8ee0-236">Si certains de vos appareils joints à un domaine sont des appareils Windows de bas niveau, vous devez :</span><span class="sxs-lookup"><span data-stu-id="d8ee0-236">If some of your domain-joined devices Windows down-level devices, you need to:</span></span>

- <span data-ttu-id="d8ee0-237">Définir une stratégie dans Azure AD pour permettre aux utilisateurs d’inscrire des appareils</span><span class="sxs-lookup"><span data-stu-id="d8ee0-237">Set a policy in Azure AD to enable users to register devices.</span></span>
 
- <span data-ttu-id="d8ee0-238">Configurer votre service de fédération local pour l’émission de revendications afin de prendre en charge **l’authentification Windows intégrée (IWA)** pour l’inscription des appareils</span><span class="sxs-lookup"><span data-stu-id="d8ee0-238">Configure your on-premises federation service to issue claims to support **Integrated Windows Authentication (IWA)** for device registration.</span></span>
 
- <span data-ttu-id="d8ee0-239">Ajouter le point de terminaison d’authentification d’appareil Azure AD aux zones Intranet local afin d’éviter les invites de certificat lors de l’authentification des appareils</span><span class="sxs-lookup"><span data-stu-id="d8ee0-239">Add the Azure AD device authentication end-point to the local Intranet zones to avoid certificate prompts when authenticating the device.</span></span>

### <a name="set-policy-in-azure-ad-to-enable-users-to-register-devices"></a><span data-ttu-id="d8ee0-240">Définir une stratégie dans Azure AD pour permettre aux utilisateurs d’inscrire des appareils</span><span class="sxs-lookup"><span data-stu-id="d8ee0-240">Set policy in Azure AD to enable users to register devices</span></span>

<span data-ttu-id="d8ee0-241">Pour inscrire des appareils Windows de bas niveau, vous devez vous assurer que le paramètre permettant aux utilisateurs d’inscrire des appareils dans Azure AD est défini.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-241">To register Windows down-level devices, you need to make sure that the setting to allow users to register devices in Azure AD is set.</span></span> <span data-ttu-id="d8ee0-242">Dans le Portail Azure, ce paramètre est disponible à l’emplacement suivant :</span><span class="sxs-lookup"><span data-stu-id="d8ee0-242">In the Azure portal, you can find this setting under:</span></span>

`Azure Active Directory > Users and groups > Device settings`
    
<span data-ttu-id="d8ee0-243">La stratégie ci-après doit être définie sur la valeur **Tous** : **Les utilisateurs peuvent inscrire leurs appareils sur Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-243">The following policy must be set to **All**: **Users may register their devices with Azure AD**</span></span>

![Inscrire des appareils](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a><span data-ttu-id="d8ee0-245">Configurer le service de fédération local</span><span class="sxs-lookup"><span data-stu-id="d8ee0-245">Configure on-premises federation service</span></span> 

<span data-ttu-id="d8ee0-246">Votre service de fédération local doit prendre en charge l’émission des revendications **authenticationmehod** et **wiaormultiauthn** lors de la réception d’une demande d’authentification auprès de la partie de confiance Azure AD qui contient un paramètre resouce_params avec une valeur encodée comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d8ee0-246">Your on-premises federation service must support issuing the **authenticationmehod** and **wiaormultiauthn** claims when receiving an authentication request to the Azure AD relying party holding a resouce_params parameter with an encoded value as shown below:</span></span>

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

<span data-ttu-id="d8ee0-247">Lorsqu’une telle demande est reçue, le service de fédération local doit authentifier l’utilisateur à l’aide de l’authentification Windows intégrée et, en cas de réussite, doit émettre les deux revendications suivantes :</span><span class="sxs-lookup"><span data-stu-id="d8ee0-247">When such a request comes, the on-premises federation service must authenticate the user using Integrated Windows Authentication and upon success, it must issue the following two claims:</span></span>

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

<span data-ttu-id="d8ee0-248">Dans AD FS, vous devez ajouter une règle de transformation d’émission qui est transmise directement par le biais de la méthode d’authentification.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-248">In AD FS, you must add an issuance transform rule that passes-through the authentication method.</span></span>  

<span data-ttu-id="d8ee0-249">**Pour ajouter cette règle :**</span><span class="sxs-lookup"><span data-stu-id="d8ee0-249">**To add this rule:**</span></span>

1. <span data-ttu-id="d8ee0-250">Dans la console de gestion AD FS, accédez à `AD FS > Trust Relationships > Relying Party Trusts`.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-250">In the AD FS management console, go to `AD FS > Trust Relationships > Relying Party Trusts`.</span></span>
2. <span data-ttu-id="d8ee0-251">Cliquez avec le bouton droit sur l’objet d’approbation de partie de confiance de la plateforme d’identité Microsoft Office 365 et sélectionnez **Modifier les règles de revendication**.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-251">Right-click the Microsoft Office 365 Identity Platform relying party trust object, and then select **Edit Claim Rules**.</span></span>
3. <span data-ttu-id="d8ee0-252">Sous l’onglet **Règles de transformation d’émission**, sélectionnez **Ajouter une règle**.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-252">On the **Issuance Transform Rules** tab, select **Add Rule**.</span></span>
4. <span data-ttu-id="d8ee0-253">Sélectionnez **Envoyer les revendications en utilisant une règle personnalisée** dans la liste de modèles **Règle de revendication**.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-253">In the **Claim rule** template list, select **Send Claims Using a Custom Rule**.</span></span>
5. <span data-ttu-id="d8ee0-254">Sélectionnez **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-254">Select **Next**.</span></span>
6. <span data-ttu-id="d8ee0-255">Dans la zone **Nom de la règle de revendication**, tapez **Règle de revendication de méthode d’authentification**.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-255">In the **Claim rule name** box, type **Auth Method Claim Rule**.</span></span>
7. <span data-ttu-id="d8ee0-256">Dans la zone **Règle de revendication**, tapez la règle suivante :</span><span class="sxs-lookup"><span data-stu-id="d8ee0-256">In the **Claim rule** box, type the following rule:</span></span>

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. <span data-ttu-id="d8ee0-257">Sur votre serveur de fédération, tapez la commande PowerShell ci-dessous après avoir remplacé **\<RPObjectName\>** par le nom d’objet de partie de confiance de votre objet Approbation de partie de confiance Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-257">On your federation server, type the PowerShell command below after replacing **\<RPObjectName\>** with the relying party object name for your Azure AD relying party trust object.</span></span> <span data-ttu-id="d8ee0-258">Cet objet est généralement nommé **plateforme d’identité Microsoft Office 365**.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-258">This object usually is named **Microsoft Office 365 Identity Platform**.</span></span>
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-the-azure-ad-device-authentication-end-point-to-the-local-intranet-zones"></a><span data-ttu-id="d8ee0-259">Ajouter le point de terminaison d’authentification d’appareil Azure AD aux zones Intranet local</span><span class="sxs-lookup"><span data-stu-id="d8ee0-259">Add the Azure AD device authentication end-point to the Local Intranet zones</span></span>

<span data-ttu-id="d8ee0-260">Pour éviter les invites de certificat lorsque les utilisateurs des appareils inscrits s’authentifient auprès d’Azure AD, vous pouvez transmettre une stratégie à vos appareils joints à un domaine pour ajouter l’URL ci-après à la zone Intranet local dans Internet Explorer :</span><span class="sxs-lookup"><span data-stu-id="d8ee0-260">To avoid certificate prompts when users in register devices authenticate to Azure AD you can push a policy to your domain-joined devices to add the following URL to the Local Intranet zone in Internet Explorer:</span></span>

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a><span data-ttu-id="d8ee0-261">Étape 4 : Contrôle du déploiement et du lancement</span><span class="sxs-lookup"><span data-stu-id="d8ee0-261">Step 4: Control deployment and rollout</span></span>

<span data-ttu-id="d8ee0-262">Une fois que vous avez exécuté les étapes requises, les appareils joints à un domaine sont prêts à s’inscrire automatiquement auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-262">When you have completed the required steps, domain-joined devices are ready to automatically register with Azure AD.</span></span> <span data-ttu-id="d8ee0-263">Tous les appareils joints à un domaine qui exécutent Mise à jour anniversaire Windows 10 et Windows Server 2016 s’inscrivent automatiquement auprès d’Azure AD lors du redémarrage des appareils ou de la connexion des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-263">All domain-joined devices running Windows 10 Anniversary Update and Windows Server 2016 automatically register with Azure AD at device restart or user sign-in.</span></span> <span data-ttu-id="d8ee0-264">Les nouveaux appareils s’inscrivent auprès d’Azure AD au moment de leur redémarrage une fois l’opération de jonction de domaine effectuée.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-264">New devices register with Azure AD when the device restarts after the domain join operation is completed.</span></span>

<span data-ttu-id="d8ee0-265">Les appareils qui ont fait précédemment l’objet d’une jonction d’espace de travail à Azure AD (par exemple pour Intune) passent à « *Joint au domaine, Enregistré avec AAD* ». Cependant, un certain temps est nécessaire pour que ce processus soit effectué sur tous les appareils, en raison du flux normal de l’activité du domaine et des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-265">Devices that were previously workplace-joined to Azure AD (for example for Intune) transition to “*Domain Joined, AAD Registered*”; however it takes some time for this process to complete across all devices due to the normal flow of domain and user activity.</span></span>

### <a name="remarks"></a><span data-ttu-id="d8ee0-266">Remarques</span><span class="sxs-lookup"><span data-stu-id="d8ee0-266">Remarks</span></span>

- <span data-ttu-id="d8ee0-267">Vous pouvez utiliser un objet de stratégie de groupe pour contrôler le déploiement de l’inscription automatique des ordinateurs Windows 10 et Windows Server 2016 joints à un domaine.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-267">You can use a Group Policy object to control the rollout of automatic registration of Windows 10 and Windows Server 2016 domain-joined computers.</span></span>

- <span data-ttu-id="d8ee0-268">La mise à jour de novembre 2015 de Windows 10 s’inscrit automatiquement auprès d’Azure AD **uniquement** si l’objet de stratégie de groupe de lancement est défini.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-268">Windows 10 November 2015 Update automatically registers with Azure AD **only** if the rollout Group Policy object is set.</span></span>

- <span data-ttu-id="d8ee0-269">Pour lancer l’inscription automatique des ordinateurs Windows de bas niveau, vous pouvez déployer un [package Windows Installer](#windows-installer-packages-for-non-windows-10-computers) sur les ordinateurs que vous sélectionnez.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-269">To rollout the automatic registration of Windows down-level computers, you can deploy a [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) to computers that you select.</span></span>

- <span data-ttu-id="d8ee0-270">Si vous transmettez l’objet de stratégie de groupe à des appareils Windows 8.1 joints à un domaine, l’inscription sera tentée ; toutefois, il est recommandé d’utiliser le [package Windows Installer](#windows-installer-packages-for-non-windows-10-computers) pour inscrire tous vos appareils Windows de bas niveau.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-270">If you push the Group Policy object to Windows 8.1 domain-joined devices, registration will be attempted; however it is recommended that you use the [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) to register all your Windows down-level devices.</span></span> 

### <a name="create-a-group-policy-object"></a><span data-ttu-id="d8ee0-271">Créer un objet de stratégie de groupe</span><span class="sxs-lookup"><span data-stu-id="d8ee0-271">Create a Group Policy object</span></span> 

<span data-ttu-id="d8ee0-272">Pour contrôler le lancement de l’inscription automatique des ordinateurs Windows actuels, vous devez déployer l’objet de stratégie de groupe **Enregistrer les ordinateurs appartenant à un domaine en tant qu’appareils** sur les appareils que vous souhaitez inscrire.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-272">To control the rollout of automatic registration of Windows current computers, you should deploy the **Register domain-joined computers as devices** Group Policy object to the devices you want to register.</span></span> <span data-ttu-id="d8ee0-273">Par exemple, vous pouvez déployer la stratégie sur un groupe de sécurité ou sur une unité organisationnelle.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-273">For example, you can deploy the policy to an organizational unit or to a security group.</span></span>

<span data-ttu-id="d8ee0-274">**Pour configurer la stratégie :**</span><span class="sxs-lookup"><span data-stu-id="d8ee0-274">**To set the policy:**</span></span>

1. <span data-ttu-id="d8ee0-275">Ouvrez **Gestionnaire de serveur**, puis accédez à `Tools > Group Policy Management`.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-275">Open **Server Manager**, and then go to `Tools > Group Policy Management`.</span></span>
2. <span data-ttu-id="d8ee0-276">Accédez au nœud de domaine qui correspond au domaine dans lequel vous souhaitez activer l’inscription automatique d’ordinateurs Windows actuels.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-276">Go to the domain node that corresponds to the domain where you want to activate auto-registration of Windows current computers.</span></span>
3. <span data-ttu-id="d8ee0-277">Cliquez avec le bouton droit sur **Objets de stratégie de groupe**, puis sélectionnez **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-277">Right-click **Group Policy Objects**, and then select **New**.</span></span>
4. <span data-ttu-id="d8ee0-278">Entrez un nom pour votre objet de stratégie de groupe.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-278">Type a name for your Group Policy object.</span></span> <span data-ttu-id="d8ee0-279">Par exemple, *Inscription automatique dans Azure AD*.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-279">For example, *Automatic Registration to Azure AD*.</span></span> <span data-ttu-id="d8ee0-280">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-280">Select **OK**.</span></span>
5. <span data-ttu-id="d8ee0-281">Cliquez avec le bouton droit sur votre nouvel objet de stratégie de groupe, puis sélectionnez **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-281">Right-click your new Group Policy object, and then select **Edit**.</span></span>
6. <span data-ttu-id="d8ee0-282">Accédez à **Configuration ordinateur** > **Stratégies** > **Modèles d’administration** > **Composants Windows** > **Enregistrement d’appareil**.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-282">Go to **Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Device Registration**.</span></span> <span data-ttu-id="d8ee0-283">Cliquez avec le bouton droit sur **Enregistrer les ordinateurs appartenant à un domaine en tant qu’appareils**, puis sélectionnez **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-283">Right-click **Register domain-joined computers as devices**, and then select **Edit**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d8ee0-284">Ce modèle de stratégie de groupe a été renommé par rapport aux versions précédentes de la Console de gestion des stratégies de groupe.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-284">This Group Policy template has been renamed from earlier versions of the Group Policy Management console.</span></span> <span data-ttu-id="d8ee0-285">Si vous utilisez une version antérieure de la console, accédez à `Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-285">If you are using an earlier version of the console, go to `Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span></span> 

7. <span data-ttu-id="d8ee0-286">Sélectionnez **Activé**, puis **Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-286">Select **Enabled**, and then select **Apply**.</span></span>
8. <span data-ttu-id="d8ee0-287">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-287">Select **OK**.</span></span>
9. <span data-ttu-id="d8ee0-288">Liez l’objet de stratégie de groupe à un emplacement de votre choix.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-288">Link the Group Policy object to a location of your choice.</span></span> <span data-ttu-id="d8ee0-289">Par exemple, vous pouvez le lier à une unité organisationnelle spécifique.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-289">For example, you can link it to a specific organizational unit.</span></span> <span data-ttu-id="d8ee0-290">Vous pouvez également le lier à un groupe de sécurité spécifique d’ordinateurs qui s’inscrivent automatiquement auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-290">You also could link it to a specific security group of computers that automatically register with Azure AD.</span></span> <span data-ttu-id="d8ee0-291">Pour définir cette stratégie pour tous les ordinateurs Windows 10 ou Windows Server 2016 joints à un domaine de votre organisation, liez l’objet de stratégie de groupe au domaine.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-291">To set this policy for all domain-joined Windows 10 and Windows Server 2016 computers in your organization, link the Group Policy object to the domain.</span></span>

### <a name="windows-installer-packages-for-non-windows-10-computers"></a><span data-ttu-id="d8ee0-292">Packages Windows Installer pour les ordinateurs autres que Windows 10</span><span class="sxs-lookup"><span data-stu-id="d8ee0-292">Windows Installer packages for non-Windows 10 computers</span></span>

<span data-ttu-id="d8ee0-293">Pour inscrire des ordinateurs Windows de bas niveau joints à un domaine dans un environnement fédéré, vous pouvez télécharger et installer ce package Windows Installer (.msi) à partir du Centre de téléchargement au niveau de la page [Microsoft Workplace Join for non-Windows 10 computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) (Microsoft Workplace pour les ordinateurs non-Windows 10).</span><span class="sxs-lookup"><span data-stu-id="d8ee0-293">To register domain-joined Windows down-level computers in a federated environment, you can download and install these Windows Installer package (.msi) from Download Center at the [Microsoft Workplace Join for non-Windows 10 computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) page.</span></span>

<span data-ttu-id="d8ee0-294">Vous pouvez déployer le package à l’aide d’un système de distribution de logiciels comme System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-294">You can deploy the package by using a software distribution system like System Center Configuration Manager.</span></span> <span data-ttu-id="d8ee0-295">Le package prend en charge les options d’installation en mode silencieux standard avec le paramètre *quiet*.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-295">The package supports the standard silent install options with the *quiet* parameter.</span></span> <span data-ttu-id="d8ee0-296">System Center Configuration Manager Current Branch offre des avantages supplémentaires par rapport aux versions précédentes, comme la possibilité d’effectuer le suivi des inscriptions terminées.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-296">System Center Configuration Manager Current Branch offers additional benefits from earlier versions, like the ability to track completed registrations.</span></span> <span data-ttu-id="d8ee0-297">Pour plus d’informations, consultez l’article [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="d8ee0-297">For more information, see [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span></span>

<span data-ttu-id="d8ee0-298">Le programme d’installation crée une tâche planifiée sur le système, qui s’exécute dans le contexte de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-298">The installer creates a scheduled task on the system that runs in the user’s context.</span></span> <span data-ttu-id="d8ee0-299">La tâche est déclenchée lorsque l’utilisateur se connecte à Windows.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-299">The task is triggered when the user signs in to Windows.</span></span> <span data-ttu-id="d8ee0-300">La tâche inscrit l’appareil en mode silencieux auprès d’Azure AD avec les informations d’identification de l’utilisateur après l’avoir authentifié à l’aide de l’authentification Windows intégrée.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-300">The task silently registers the device with Azure AD with the user credentials after authenticating using Integrated Windows Authentication.</span></span> <span data-ttu-id="d8ee0-301">Pour visualiser la tâche planifiée, sélectionnez sur l’appareil **Microsoft** > **Rattacher à l’espace de travail**, puis accédez à la bibliothèque du Planificateur de tâches.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-301">To see the scheduled task, in the device, go to **Microsoft** > **Workplace Join**, and then go to the Task Scheduler library.</span></span>

## <a name="step-5-verify-registered-devices"></a><span data-ttu-id="d8ee0-302">Étape 5 : Vérification des appareils inscrits</span><span class="sxs-lookup"><span data-stu-id="d8ee0-302">Step 5: Verify registered devices</span></span>

<span data-ttu-id="d8ee0-303">Vous pouvez vérifier les appareils qui ont été correctement inscrits dans votre organisation en utilisant l’applet de commande [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) dans le [module Azure Active Directory PowerShell](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="d8ee0-303">You can check successful registered devices in your organization by using the [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in the [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span>

<span data-ttu-id="d8ee0-304">La sortie de cette applet de commande affiche les appareils inscrits dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-304">The output of this cmdlet shows devices registered in Azure AD.</span></span> <span data-ttu-id="d8ee0-305">Pour obtenir tous les appareils, utilisez le paramètre **-All**, puis filtrez-les à l’aide de la propriété **deviceTrustType**.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-305">To get all devices, use the **-All** parameter, and then filter them using the **deviceTrustType** property.</span></span> <span data-ttu-id="d8ee0-306">Les appareils joints à un domaine présentent la valeur **Joint au domaine**.</span><span class="sxs-lookup"><span data-stu-id="d8ee0-306">Domain joined devices have a value of **Domain Joined**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8ee0-307">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d8ee0-307">Next steps</span></span>

* [<span data-ttu-id="d8ee0-308">FAQ sur l’inscription d’appareils automatique</span><span class="sxs-lookup"><span data-stu-id="d8ee0-308">Automatic device registration FAQ</span></span>](active-directory-device-registration-faq.md)
* [<span data-ttu-id="d8ee0-309">Résolution des problèmes de l’inscription automatique des ordinateurs joints au domaine à Azure AD – Windows 10 et Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="d8ee0-309">Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)
* [<span data-ttu-id="d8ee0-310">Résolution des problèmes d’inscription automatique des ordinateurs non-Windows 10 joints à un domaine auprès d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8ee0-310">Troubleshooting auto-registration of domain joined computers to Azure AD – non-Windows 10</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
* [<span data-ttu-id="d8ee0-311">Accès conditionnel Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d8ee0-311">Azure Active Directory conditional access</span></span>](active-directory-conditional-access-azure-portal.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
