---
title: "Comment configurer des appareils hybrides joints à Azure Active Directory | Microsoft Docs"
description: "Découvrez comment configurer des appareils hybrides joints à Azure Active Directory."
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
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 4580075df9fce74664b22aa24065ba1885692384
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-configure-hybrid-azure-active-directory-joined-devices"></a><span data-ttu-id="d81d6-103">Comment configurer des appareils hybrides joints à Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d81d6-103">How to configure hybrid Azure Active Directory joined devices</span></span>

<span data-ttu-id="d81d6-104">La fonction de gestion des appareils intégrée à Azure Active Directory (Azure AD) vous permet de vous assurer que vos utilisateurs accèdent à vos ressources à partir d’appareils qui répondent à vos normes de conformité et de sécurité.</span><span class="sxs-lookup"><span data-stu-id="d81d6-104">With device management in Azure Active Directory (Azure AD), you can ensure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> <span data-ttu-id="d81d6-105">Pour plus d’informations, voir [Présentation de la gestion des appareils dans Azure Active Directory](device-management-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d81d6-105">For more details, see [Introduction to device management in Azure Active Directory](device-management-introduction.md).</span></span>

<span data-ttu-id="d81d6-106">Si vous disposez d’un environnement Active Directory local et que vous souhaitez lier à Azure AD vos appareils joints à un domaine, vous pouvez y parvenir en configurant simplement des appareils hybrides joints à Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d81d6-106">If you have an on-premises Active Directory environment and you want to join your domain-joined devices to Azure AD, you can accomplish this by configuring hybrid Azure AD joined devices.</span></span> <span data-ttu-id="d81d6-107">Cette rubrique vous présente les étapes de cette configuration.</span><span class="sxs-lookup"><span data-stu-id="d81d6-107">The topic provides you with the related steps.</span></span> 


## <a name="before-you-begin"></a><span data-ttu-id="d81d6-108">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="d81d6-108">Before you begin</span></span>

<span data-ttu-id="d81d6-109">Avant de commencer à configurer des appareils hybrides joints à Azure AD dans votre environnement, vous devez vous familiariser avec les scénarios pris en charge et avec les contraintes.</span><span class="sxs-lookup"><span data-stu-id="d81d6-109">Before you start configuring hybrid Azure AD joined devices in your environment, you should familiarize yourself with the supported scenarios and the constraints.</span></span>  

<span data-ttu-id="d81d6-110">Pour améliorer la lisibilité des descriptions, cet article utilise les termes suivants :</span><span class="sxs-lookup"><span data-stu-id="d81d6-110">To improve the readability of the descriptions, this topic uses the following term:</span></span> 

- <span data-ttu-id="d81d6-111">**Appareils Windows actuels** : ce terme désigne les appareils joints à un domaine qui exécutent Windows 10 ou Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="d81d6-111">**Windows current devices** - This term refers to domain-joined devices running Windows 10 or Windows Server 2016.</span></span>
- <span data-ttu-id="d81d6-112">**Appareils Windows de bas niveau** : ce terme fait référence à tous les appareils Windows joints à un domaine **pris en charge** qui n’exécutent ni Windows 10 ni Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="d81d6-112">**Windows down-level devices** - This term refers to all **supported** domain-joined Windows devices that are neither running Windows 10 nor Windows Server 2016.</span></span>  


### <a name="windows-current-devices"></a><span data-ttu-id="d81d6-113">Appareils Windows actuels</span><span class="sxs-lookup"><span data-stu-id="d81d6-113">Windows current devices</span></span>

- <span data-ttu-id="d81d6-114">Pour les appareils qui exécutent le système d’exploitation d’ordinateur Windows, nous recommandons d’utiliser Mise à jour anniversaire Windows 10 (version 1607) ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d81d6-114">For devices running the Windows desktop operating system, we recommend using Windows 10 Anniversary Update (version 1607) or later.</span></span> 
- <span data-ttu-id="d81d6-115">L’inscription des appareils Windows actuels **est** prise en charge dans les environnements non fédérés tels que les configurations de synchronisation du hachage de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="d81d6-115">The registration of Windows current devices **is** supported in non-federated environments such as password hash sync configurations.</span></span>  


### <a name="windows-down-level-devices"></a><span data-ttu-id="d81d6-116">Appareils Windows de bas niveau</span><span class="sxs-lookup"><span data-stu-id="d81d6-116">Windows down-level devices</span></span>

- <span data-ttu-id="d81d6-117">Les appareils Windows de bas niveau pris en charge sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="d81d6-117">The following Windows down-level devices are supported:</span></span>
    - <span data-ttu-id="d81d6-118">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="d81d6-118">Windows 8.1</span></span>
    - <span data-ttu-id="d81d6-119">Windows 7</span><span class="sxs-lookup"><span data-stu-id="d81d6-119">Windows 7</span></span>
    - <span data-ttu-id="d81d6-120">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="d81d6-120">Windows Server 2012 R2</span></span>
    - <span data-ttu-id="d81d6-121">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="d81d6-121">Windows Server 2012</span></span>
    - <span data-ttu-id="d81d6-122">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="d81d6-122">Windows Server 2008 R2</span></span>
- <span data-ttu-id="d81d6-123">L’inscription d’appareils de bas niveau Windows **est** prise en charge dans les environnements non fédérés via l’authentification unique transparente [Authentification unique transparente d’Azure Active Directory](https://aka.ms/hybrid/sso).</span><span class="sxs-lookup"><span data-stu-id="d81d6-123">The registration of Windows down-level devices **is** supported in non-federated environments through Seamless Single Sign On [Azure Active Directory Seamless Single Sign-On](https://aka.ms/hybrid/sso).</span></span>
- <span data-ttu-id="d81d6-124">L’inscription des appareils Windows de bas niveau **n’est pas** prise en charge pour les appareils utilisant des profils d’itinérance.</span><span class="sxs-lookup"><span data-stu-id="d81d6-124">The registration of Windows down-level devices **is not** supported for devices using roaming profiles.</span></span> <span data-ttu-id="d81d6-125">Si vous vous appuyez sur l’itinérance de profils ou de paramètres, utilisez Windows 10.</span><span class="sxs-lookup"><span data-stu-id="d81d6-125">If you are relying on roaming of profiles or settings, use Windows 10.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="d81d6-126">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d81d6-126">Prerequisites</span></span>

<span data-ttu-id="d81d6-127">Avant de commencer à activer des appareils hybrides joints à Azure AD dans votre organisation, vous devez vous assurer que vous exécutez une version à jour d’Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d81d6-127">Before you start enabling hybrid Azure AD joined devices in your organization, you need to make sure that you are running an up-to-date version of Azure AD connect.</span></span>

<span data-ttu-id="d81d6-128">Azure AD Connect :</span><span class="sxs-lookup"><span data-stu-id="d81d6-128">Azure AD Connect:</span></span>

- <span data-ttu-id="d81d6-129">Conserve l’association entre le compte d’ordinateur dans votre service Active Directory (AD) local et l’objet appareil dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d81d6-129">Keeps the association between the computer account in your on-premises Active Directory (AD) and the device object in Azure AD.</span></span> 
- <span data-ttu-id="d81d6-130">Permet d’utiliser d’autres fonctionnalités liées aux appareils telles que Windows Hello Entreprise.</span><span class="sxs-lookup"><span data-stu-id="d81d6-130">Enables other device related features like Windows Hello for Business.</span></span>



## <a name="configuration-steps"></a><span data-ttu-id="d81d6-131">Configuration</span><span class="sxs-lookup"><span data-stu-id="d81d6-131">Configuration steps</span></span>

<span data-ttu-id="d81d6-132">Vous pouvez configurer des appareils hybrides joints à Azure AD pour différents types de plateformes d’appareils Windows.</span><span class="sxs-lookup"><span data-stu-id="d81d6-132">You can configure hybrid Azure AD joined devices for various types of Windows device platforms.</span></span> <span data-ttu-id="d81d6-133">Cet article inclut les étapes requises pour tous les scénarios de configuration classiques.</span><span class="sxs-lookup"><span data-stu-id="d81d6-133">This topic includes the required steps for all typical configuration scenarios.</span></span>  

<span data-ttu-id="d81d6-134">Pour obtenir une vue d’ensemble des étapes requises par votre scénario, utilisez le tableau ci-après :</span><span class="sxs-lookup"><span data-stu-id="d81d6-134">Use the following table to get an overview of the steps that are required for your scenario:</span></span>  



| <span data-ttu-id="d81d6-135">Étapes</span><span class="sxs-lookup"><span data-stu-id="d81d6-135">Steps</span></span>                                      | <span data-ttu-id="d81d6-136">Appareils Windows actuels et synchronisation du hachage de mot de passe</span><span class="sxs-lookup"><span data-stu-id="d81d6-136">Windows current and password hash sync</span></span> | <span data-ttu-id="d81d6-137">Appareils Windows actuels et fédération</span><span class="sxs-lookup"><span data-stu-id="d81d6-137">Windows current and federation</span></span> | <span data-ttu-id="d81d6-138">Appareils Windows de bas niveau</span><span class="sxs-lookup"><span data-stu-id="d81d6-138">Windows down-level</span></span> |
| :--                                        | :-:                                    | :-:                            | :-:                |
| <span data-ttu-id="d81d6-139">Étape 1 : Configuration du point de connexion de service</span><span class="sxs-lookup"><span data-stu-id="d81d6-139">Step 1: Configure service connection point</span></span> | ![Vérification][1]                            | ![Vérification][1]                    | ![Vérification][1]        |
| <span data-ttu-id="d81d6-143">Étape 2 : Configuration de l’émission de revendications</span><span class="sxs-lookup"><span data-stu-id="d81d6-143">Step 2: Setup issuance of claims</span></span>           |                                        | ![Vérification][1]                    | ![Vérification][1]        |
| <span data-ttu-id="d81d6-146">Étape 3 : Activation d’appareils non-Windows 10</span><span class="sxs-lookup"><span data-stu-id="d81d6-146">Step 3: Enable non-Windows 10 devices</span></span>      |                                        |                                | ![Vérification][1]        |
| <span data-ttu-id="d81d6-148">Étape 4 : Contrôle du déploiement et du lancement</span><span class="sxs-lookup"><span data-stu-id="d81d6-148">Step 4: Control deployment and rollout</span></span>     | ![Vérification][1]                            | ![Vérification][1]                    | ![Vérification][1]        |
| <span data-ttu-id="d81d6-152">Étape 5 : Vérification des appareils joints</span><span class="sxs-lookup"><span data-stu-id="d81d6-152">Step 5: Verify joined devices</span></span>          | ![Vérification][1]                            | ![Vérification][1]                    | ![Vérification][1]        |



## <a name="step-1-configure-service-connection-point"></a><span data-ttu-id="d81d6-156">Étape 1 : Configuration du point de connexion de service</span><span class="sxs-lookup"><span data-stu-id="d81d6-156">Step 1: Configure service connection point</span></span>

<span data-ttu-id="d81d6-157">Vos appareils utilisent l’objet point de connexion de service (SCP) lors de l’inscription pour détecter les informations de client Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d81d6-157">The service connection point (SCP) object is used by your devices during the registration to discover Azure AD tenant information.</span></span> <span data-ttu-id="d81d6-158">Dans votre service Active Directory (AD) local, l’objet SCP des appareils hybrides joints à Azure AD doit exister dans la partition de contexte d’appellation de configuration de la forêt de l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d81d6-158">In your on-premises Active Directory (AD), the SCP object for the hybrid Azure AD joined devices must exist in the configuration naming context partition of the computer's forest.</span></span> <span data-ttu-id="d81d6-159">Il n’existe qu’un seul contexte d’appellation de configuration par forêt.</span><span class="sxs-lookup"><span data-stu-id="d81d6-159">There is only one configuration naming context per forest.</span></span> <span data-ttu-id="d81d6-160">Dans une configuration Active Directory à forêts multiples, le point de connexion de service doit exister dans toutes les forêts qui contiennent des ordinateurs joints à un domaine.</span><span class="sxs-lookup"><span data-stu-id="d81d6-160">In a multi-forest Active Directory configuration, the service connection point must exist in all forests containing domain-joined computers.</span></span>

<span data-ttu-id="d81d6-161">Pour récupérer le contexte d’appellation de configuration de votre forêt, vous pouvez utiliser l’applet de commande [**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx).</span><span class="sxs-lookup"><span data-stu-id="d81d6-161">You can use the [**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx) cmdlet to retrieve the configuration naming context of your forest.</span></span>  

<span data-ttu-id="d81d6-162">Pour une forêt avec le nom de domaine Active Directory *fabrikam.com*, le contexte d’appellation de configuration est le suivant :</span><span class="sxs-lookup"><span data-stu-id="d81d6-162">For a forest with the Active Directory domain name *fabrikam.com*, the configuration naming context is:</span></span>

`CN=Configuration,DC=fabrikam,DC=com`

<span data-ttu-id="d81d6-163">Dans votre forêt, l’objet SCP pour l’inscription automatique des appareils joints à un domaine se trouve à l’emplacement suivant :</span><span class="sxs-lookup"><span data-stu-id="d81d6-163">In your forest, the SCP object for the auto-registration of domain-joined devices is located at:</span></span>  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

<span data-ttu-id="d81d6-164">Selon la façon dont vous avez déployé Azure AD Connect, il est possible que l’objet SCP ait déjà été configuré.</span><span class="sxs-lookup"><span data-stu-id="d81d6-164">Depending on how you have deployed Azure AD Connect, the SCP object may have already been configured.</span></span>
<span data-ttu-id="d81d6-165">Vous pouvez vérifier l’existence de l’objet et récupérer les valeurs de détection à l’aide du script Windows PowerShell suivant :</span><span class="sxs-lookup"><span data-stu-id="d81d6-165">You can verify the existence of the object and retrieve the discovery values using the following Windows PowerShell script:</span></span> 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

<span data-ttu-id="d81d6-166">La sortie de **$scp.Keywords** présente les informations de client Azure AD, par exemple :</span><span class="sxs-lookup"><span data-stu-id="d81d6-166">The **$scp.Keywords** output shows the Azure AD tenant information, for example:</span></span>

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

<span data-ttu-id="d81d6-167">Si le point de connexion de service n’existe pas, vous pouvez le créer en exécutant l’applet de commande `Initialize-ADSyncDomainJoinedComputerSync` sur votre serveur Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d81d6-167">If the service connection point does not exist, you can create it by running the `Initialize-ADSyncDomainJoinedComputerSync` cmdlet on your Azure AD Connect server.</span></span> <span data-ttu-id="d81d6-168">Des informations d’identification d’administrateur d’entreprise sont requises pour exécuter cette applet de commande.</span><span class="sxs-lookup"><span data-stu-id="d81d6-168">Enterprise admin credential is required to run this cmdlet.</span></span>  
<span data-ttu-id="d81d6-169">Cette applet de commande :</span><span class="sxs-lookup"><span data-stu-id="d81d6-169">The cmdlet:</span></span>

- <span data-ttu-id="d81d6-170">Crée le point de connexion de service dans la forêt Active Directory à laquelle Azure AD Connect est connecté.</span><span class="sxs-lookup"><span data-stu-id="d81d6-170">Creates the service connection point in the Active Directory forest Azure AD Connect is connected to.</span></span> 
- <span data-ttu-id="d81d6-171">Vous demande de spécifier le paramètre `AdConnectorAccount`.</span><span class="sxs-lookup"><span data-stu-id="d81d6-171">Requires you to specify the `AdConnectorAccount` parameter.</span></span> <span data-ttu-id="d81d6-172">Il s’agit du compte configuré en tant que compte de connecteur Active Directory dans Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d81d6-172">This is the account that is configured as Active Directory connector account in Azure AD connect.</span></span> 


<span data-ttu-id="d81d6-173">Le script ci-après présente un exemple d’utilisation de l’applet de commande.</span><span class="sxs-lookup"><span data-stu-id="d81d6-173">The following script shows an example for using the cmdlet.</span></span> <span data-ttu-id="d81d6-174">Dans ce script, la chaîne `$aadAdminCred = Get-Credential` exige que vous tapiez un nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d81d6-174">In this script, `$aadAdminCred = Get-Credential` requires you to type a user name.</span></span> <span data-ttu-id="d81d6-175">Vous devez indiquer le nom d’utilisateur au format de nom d’utilisateur principal (UPN) (`user@example.com`).</span><span class="sxs-lookup"><span data-stu-id="d81d6-175">You need to provide the user name in the user principal name (UPN) format (`user@example.com`).</span></span> 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

<span data-ttu-id="d81d6-176">L’applet de commande `Initialize-ADSyncDomainJoinedComputerSync` :</span><span class="sxs-lookup"><span data-stu-id="d81d6-176">The `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span></span>

- <span data-ttu-id="d81d6-177">utilise le module Active Directory PowerShell qui s’appuie sur les services Web Active Directory s’exécutant sur un contrôleur de domaine.</span><span class="sxs-lookup"><span data-stu-id="d81d6-177">Uses the Active Directory PowerShell module, which relies on Active Directory Web Services running on a domain controller.</span></span> <span data-ttu-id="d81d6-178">Les services Web Active Directory sont pris en charge sur les contrôleurs de domaine exécutant Windows Server 2008 R2 et les versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="d81d6-178">Active Directory Web Services is supported on domain controllers running Windows Server 2008 R2 and later.</span></span>
- <span data-ttu-id="d81d6-179">Est pris en charge seulement par le **module MSOnline PowerShell version 1.1.166.0**.</span><span class="sxs-lookup"><span data-stu-id="d81d6-179">Is only supported by the **MSOnline PowerShell module version 1.1.166.0**.</span></span> <span data-ttu-id="d81d6-180">Pour télécharger ce module, utilisez ce [lien](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span><span class="sxs-lookup"><span data-stu-id="d81d6-180">To download this module, use this [link](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span></span>   

<span data-ttu-id="d81d6-181">Pour les contrôleurs de domaine exécutant Windows Server 2008 ou des versions antérieures, utilisez le script ci-après pour créer le point de connexion de service.</span><span class="sxs-lookup"><span data-stu-id="d81d6-181">For domain controllers running Windows Server 2008 or earlier versions, use the script below to create the service connection point.</span></span>

<span data-ttu-id="d81d6-182">Dans une configuration à forêts multiples, vous devez utiliser le script ci-dessous pour créer le point de connexion de service dans chacune des forêts contenant des ordinateurs :</span><span class="sxs-lookup"><span data-stu-id="d81d6-182">In a multi-forest configuration, you should use the following script to create the service connection point in each forest where computers exist:</span></span>
 
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


## <a name="step-2-setup-issuance-of-claims"></a><span data-ttu-id="d81d6-183">Étape 2 : Configuration de l’émission de revendications</span><span class="sxs-lookup"><span data-stu-id="d81d6-183">Step 2: Setup issuance of claims</span></span>

<span data-ttu-id="d81d6-184">Dans une configuration Azure AD fédérée, les appareils s’appuient sur les services de fédération Active Directory (AD FS) ou sur un service de fédération local tiers pour s’authentifier auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d81d6-184">In a federated Azure AD configuration, devices rely on Active Directory Federation Services (AD FS) or a 3rd party on-premises federation service to authenticate to Azure AD.</span></span> <span data-ttu-id="d81d6-185">Les appareils s’authentifient pour obtenir un jeton d’accès afin de s’inscrire auprès du service Azure Active Directory Device Registration Service (Azure DRS).</span><span class="sxs-lookup"><span data-stu-id="d81d6-185">Devices authenticate to get an access token to register against the Azure Active Directory Device Registration Service (Azure DRS).</span></span>

<span data-ttu-id="d81d6-186">Les appareils Windows actuels s’authentifient à l’aide de l’authentification Windows intégrée auprès d’un point de terminaison WS-Trust actif (version 1.3 ou 2005) hébergé par le service de fédération local.</span><span class="sxs-lookup"><span data-stu-id="d81d6-186">Windows current devices authenticate using Integrated Windows Authentication to an active WS-Trust endpoint (either 1.3 or 2005 versions) hosted by the on-premises federation service.</span></span>

> [!NOTE]
> <span data-ttu-id="d81d6-187">En cas d’utilisation d’AD FS, il est nécessaire d’activer **adfs/services/trust/13/windowstransport** ou **adfs/services/trust/2005/windowstransport**.</span><span class="sxs-lookup"><span data-stu-id="d81d6-187">When using AD FS, either **adfs/services/trust/13/windowstransport** or **adfs/services/trust/2005/windowstransport** must be enabled.</span></span> <span data-ttu-id="d81d6-188">Si vous utilisez le proxy d’authentification web, vérifiez également que ce point de terminaison est publié via le proxy.</span><span class="sxs-lookup"><span data-stu-id="d81d6-188">If you are using the Web Authentication Proxy, also ensure that this endpoint is published through the proxy.</span></span> <span data-ttu-id="d81d6-189">Vous pouvez visualiser les points de terminaison qui sont activés par le biais de la console de gestion AD FS sous **Service > Points de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="d81d6-189">You can see what end-points are enabled through the AD FS management console under **Service > Endpoints**.</span></span>
>
><span data-ttu-id="d81d6-190">Si vous n’utilisez pas AD FS en tant que service de fédération local, suivez les instructions de votre fournisseur pour vous assurer que celui-ci prend en charge les points de terminaison WS-Trust 1.3 ou 2005 et que ces derniers sont publiés par le biais du fichier Metadata Exchange (MEX).</span><span class="sxs-lookup"><span data-stu-id="d81d6-190">If you don’t have AD FS as your on-premises federation service, follow the instructions of your vendor to make sure they support WS-Trust 1.3 or 2005 end-points and that these are published through the Metadata Exchange file (MEX).</span></span>

<span data-ttu-id="d81d6-191">Pour que l’inscription d’appareils puisse s’effectuer, les revendications ci-après doivent exister dans le jeton reçu par Azure DRS.</span><span class="sxs-lookup"><span data-stu-id="d81d6-191">The following claims must exist in the token received by Azure DRS for device registration to complete.</span></span> <span data-ttu-id="d81d6-192">Azure DRS crée un objet appareil dans Azure AD avec certaines de ces informations, qu’Azure AD Connect utilise ensuite pour associer l’objet appareil nouvellement créé au compte d’ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="d81d6-192">Azure DRS will create a device object in Azure AD with some of this information which is then used by Azure AD Connect to associate the newly created device object with the computer account on-premises.</span></span>

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

<span data-ttu-id="d81d6-193">Si vous disposez de plusieurs noms de domaine vérifiés, vous devez fournir la revendication ci-après pour les ordinateurs :</span><span class="sxs-lookup"><span data-stu-id="d81d6-193">If you have more than one verified domain name, you need to provide the following claim for computers:</span></span>

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

<span data-ttu-id="d81d6-194">Si vous émettez déjà une revendication ImmutableID (par exemple, un ID de connexion alternatif), vous devez fournir une seule revendication correspondante pour les ordinateurs :</span><span class="sxs-lookup"><span data-stu-id="d81d6-194">If you are already issuing an ImmutableID claim (e.g., alternate login ID) you need to provide one corresponding claim for computers:</span></span>

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

<span data-ttu-id="d81d6-195">Dans les sections ci-après, vous trouverez des informations concernant :</span><span class="sxs-lookup"><span data-stu-id="d81d6-195">In the following sections, you find information about:</span></span>
 
- <span data-ttu-id="d81d6-196">Les valeurs requises pour chaque revendication</span><span class="sxs-lookup"><span data-stu-id="d81d6-196">The values each claim should have</span></span>
- <span data-ttu-id="d81d6-197">L’aspect d’une définition dans AD FS</span><span class="sxs-lookup"><span data-stu-id="d81d6-197">How a definition would look like in AD FS</span></span>

<span data-ttu-id="d81d6-198">La définition vous permet de vérifier si les valeurs sont présentes ou si vous devez les créer.</span><span class="sxs-lookup"><span data-stu-id="d81d6-198">The definition helps you to verify whether the values are present or if you need to create them.</span></span>

> [!NOTE]
> <span data-ttu-id="d81d6-199">Si vous n’utilisez pas AD FS pour votre serveur de fédération local, suivez les instructions de votre fournisseur afin de créer la configuration appropriée pour l’émission de ces revendications.</span><span class="sxs-lookup"><span data-stu-id="d81d6-199">If you don’t use AD FS for your on-premises federation server, follow your vendor's instructions to create the appropriate configuration to issue these claims.</span></span>

### <a name="issue-account-type-claim"></a><span data-ttu-id="d81d6-200">Émission de la revendication du type de compte</span><span class="sxs-lookup"><span data-stu-id="d81d6-200">Issue account type claim</span></span>

<span data-ttu-id="d81d6-201">**`http://schemas.microsoft.com/ws/2012/01/accounttype`** : cette revendication doit contenir la valeur **DJ**, qui identifie l’appareil en tant qu’ordinateur joint à un domaine.</span><span class="sxs-lookup"><span data-stu-id="d81d6-201">**`http://schemas.microsoft.com/ws/2012/01/accounttype`** - This claim must contain a value of **DJ**, which identifies the device as a domain-joined computer.</span></span> <span data-ttu-id="d81d6-202">Dans AD FS, vous pouvez ajouter une règle de transformation d’émission ressemblant à ceci :</span><span class="sxs-lookup"><span data-stu-id="d81d6-202">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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

### <a name="issue-objectguid-of-the-computer-account-on-premises"></a><span data-ttu-id="d81d6-203">Émission de la valeur ObjectGUID du compte d’ordinateur local</span><span class="sxs-lookup"><span data-stu-id="d81d6-203">Issue objectGUID of the computer account on-premises</span></span>

<span data-ttu-id="d81d6-204">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`** : cette revendication doit contenir la valeur **objectGUID** du compte d’ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="d81d6-204">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`** - This claim must contain the **objectGUID** value of the on-premises computer account.</span></span> <span data-ttu-id="d81d6-205">Dans AD FS, vous pouvez ajouter une règle de transformation d’émission ressemblant à ceci :</span><span class="sxs-lookup"><span data-stu-id="d81d6-205">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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
 
### <a name="issue-objectsid-of-the-computer-account-on-premises"></a><span data-ttu-id="d81d6-206">Émission de la valeur objectSID du compte d’ordinateur local</span><span class="sxs-lookup"><span data-stu-id="d81d6-206">Issue objectSID of the computer account on-premises</span></span>

<span data-ttu-id="d81d6-207">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`** : cette revendication doit contenir la valeur **objectSid** du compte d’ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="d81d6-207">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`** - This claim must contain the the **objectSid** value of the on-premises computer account.</span></span> <span data-ttu-id="d81d6-208">Dans AD FS, vous pouvez ajouter une règle de transformation d’émission ressemblant à ceci :</span><span class="sxs-lookup"><span data-stu-id="d81d6-208">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a><span data-ttu-id="d81d6-209">Émission de la valeur issuerID pour l’ordinateur s’il existe plusieurs noms de domaine vérifiés dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="d81d6-209">Issue issuerID for computer when multiple verified domain names in Azure AD</span></span>

<span data-ttu-id="d81d6-210">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`** : cette revendication doit contenir l’URI (Uniform Resource Identifier) des noms de domaine vérifiés qui se connectent avec le service de fédération local (AD FS ou tiers) émettant le jeton.</span><span class="sxs-lookup"><span data-stu-id="d81d6-210">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`** - This claim must contain the Uniform Resource Identifier (URI) of any of the verified domain names that connect with the on-premises federation service (AD FS or 3rd party) issuing the token.</span></span> <span data-ttu-id="d81d6-211">Dans AD FS, vous pouvez ajouter des règles de transformation d’émission qui ressemblent à celles ci-dessous dans l’ordre indiqué après les règles mentionnées ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="d81d6-211">In AD FS, you can add issuance transform rules that look like the ones below in that specific order after the ones above.</span></span> <span data-ttu-id="d81d6-212">Notez qu’il doit exister une règle régissant l’émission explicite de la règle pour les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="d81d6-212">Please note that one rule to explicitly issue the rule for users is necessary.</span></span> <span data-ttu-id="d81d6-213">Dans les règles ci-dessous, une première règle est ajoutée afin d’identifier l’authentification d’un utilisateur plutôt que d’un ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d81d6-213">In the rules below, a first rule identifying user vs. computer authentication is added.</span></span>

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


<span data-ttu-id="d81d6-214">Dans la revendication ci-dessus,</span><span class="sxs-lookup"><span data-stu-id="d81d6-214">In the claim above,</span></span>

- <span data-ttu-id="d81d6-215">`$<domain>` est l’URL des services AD FS</span><span class="sxs-lookup"><span data-stu-id="d81d6-215">`$<domain>` is the AD FS service URL</span></span>
- <span data-ttu-id="d81d6-216">`<verified-domain-name>` est un espace réservé que vous devez remplacer par un de vos noms de domaine vérifiés dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="d81d6-216">`<verified-domain-name>` is a placeholder you need to replace with one of your verified domain names in Azure AD</span></span>



<span data-ttu-id="d81d6-217">Pour plus d’informations sur la vérification du domaine, consultez [Ajouter un nom de domaine personnalisé à Azure Active Directory](active-directory-add-domain.md).</span><span class="sxs-lookup"><span data-stu-id="d81d6-217">For more details about verified domain names, see [Add a custom domain name to Azure Active Directory](active-directory-add-domain.md).</span></span>  
<span data-ttu-id="d81d6-218">Pour obtenir une liste de vos domaines d’entreprise vérifiés, vous pouvez utiliser l’applet de commande [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0).</span><span class="sxs-lookup"><span data-stu-id="d81d6-218">To get a list of your verified company domains, you can use the [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span></span> 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a><span data-ttu-id="d81d6-220">Émission de la valeur ImmutableID pour l’ordinateur s’il en existe une pour les utilisateurs (par exemple, définition d’un ID de connexion alternatif)</span><span class="sxs-lookup"><span data-stu-id="d81d6-220">Issue ImmutableID for computer when one for users exist (e.g. alternate login ID is set)</span></span>

<span data-ttu-id="d81d6-221">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** : cette revendication doit contenir une valeur valide pour les ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="d81d6-221">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - This claim must contain a valid value for computers.</span></span> <span data-ttu-id="d81d6-222">Dans AD FS, vous pouvez créer une règle de transformation d’émission comme suit :</span><span class="sxs-lookup"><span data-stu-id="d81d6-222">In AD FS, you can create an issuance transform rule as follows:</span></span>

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

### <a name="helper-script-to-create-the-ad-fs-issuance-transform-rules"></a><span data-ttu-id="d81d6-223">Script d’assistance pour la création des règles de transformation d’émission AD FS</span><span class="sxs-lookup"><span data-stu-id="d81d6-223">Helper script to create the AD FS issuance transform rules</span></span>

<span data-ttu-id="d81d6-224">Le script ci-après vous aide à créer les règles de transformation d’émission décrites ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="d81d6-224">The following script helps you with the creation of the issuance transform rules described above.</span></span>

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

### <a name="remarks"></a><span data-ttu-id="d81d6-225">Remarques</span><span class="sxs-lookup"><span data-stu-id="d81d6-225">Remarks</span></span> 

- <span data-ttu-id="d81d6-226">Ce script ajoute les règles aux règles existantes.</span><span class="sxs-lookup"><span data-stu-id="d81d6-226">This script appends the rules to the existing rules.</span></span> <span data-ttu-id="d81d6-227">N’exécutez pas le script à deux reprises, car l’ensemble de règles serait alors ajouté deux fois.</span><span class="sxs-lookup"><span data-stu-id="d81d6-227">Do not run the script twice because the set of rules would be added twice.</span></span> <span data-ttu-id="d81d6-228">Avant de réexécuter le script, assurez-vous qu’il n’existe aucune règle correspondante pour ces revendications (sous les conditions associées).</span><span class="sxs-lookup"><span data-stu-id="d81d6-228">Make sure that no corresponding rules exist for these claims (under the corresponding conditions) before running the script again.</span></span>

- <span data-ttu-id="d81d6-229">Si vous disposez de plusieurs noms de domaine vérifiés (comme indiqué dans le portail Azure AD ou par le biais de l’applet de commande Get-MsolDomains), définissez l’élément **$multipleVerifiedDomainNames** du script sur la valeur **$true**.</span><span class="sxs-lookup"><span data-stu-id="d81d6-229">If you have multiple verified domain names (as shown in the Azure AD portal or via the Get-MsolDomains cmdlet), set the value of **$multipleVerifiedDomainNames** in the script to **$true**.</span></span> <span data-ttu-id="d81d6-230">Veillez également à supprimer toute revendication issuerid existante pouvant avoir été créée par Azure AD Connect ou par d’autres moyens.</span><span class="sxs-lookup"><span data-stu-id="d81d6-230">Also make sure that you remove any existing issuerid claim that might have been created by Azure AD Connect or via other means.</span></span> <span data-ttu-id="d81d6-231">Voici un exemple de cette règle :</span><span class="sxs-lookup"><span data-stu-id="d81d6-231">Here is an example for this rule:</span></span>


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- <span data-ttu-id="d81d6-232">Si vous avez déjà émis une revendication **ImmutableID** pour les comptes d’utilisateurs, définissez l’élément **$immutableIDAlreadyIssuedforUsers** du script sur la valeur **$true**.</span><span class="sxs-lookup"><span data-stu-id="d81d6-232">If you have already issued an **ImmutableID** claim  for user accounts, set the value of **$immutableIDAlreadyIssuedforUsers** in the script to **$true**.</span></span>

## <a name="step-3-enable-windows-down-level-devices"></a><span data-ttu-id="d81d6-233">Étape 3 : Activation des appareils Windows de bas niveau</span><span class="sxs-lookup"><span data-stu-id="d81d6-233">Step 3: Enable Windows down-level devices</span></span>

<span data-ttu-id="d81d6-234">Si certains de vos appareils joints à un domaine sont des appareils Windows de bas niveau, vous devez :</span><span class="sxs-lookup"><span data-stu-id="d81d6-234">If some of your domain-joined devices Windows down-level devices, you need to:</span></span>

- <span data-ttu-id="d81d6-235">Définir une stratégie dans Azure AD pour permettre aux utilisateurs d’inscrire des appareils</span><span class="sxs-lookup"><span data-stu-id="d81d6-235">Set a policy in Azure AD to enable users to register devices.</span></span>
 
- <span data-ttu-id="d81d6-236">Configurer votre service de fédération local pour l’émission de revendications afin de prendre en charge **l’authentification Windows intégrée (IWA)** pour l’inscription des appareils</span><span class="sxs-lookup"><span data-stu-id="d81d6-236">Configure your on-premises federation service to issue claims to support **Integrated Windows Authentication (IWA)** for device registration.</span></span>
 
- <span data-ttu-id="d81d6-237">Ajouter le point de terminaison d’authentification d’appareil Azure AD aux zones Intranet local afin d’éviter les invites de certificat lors de l’authentification des appareils</span><span class="sxs-lookup"><span data-stu-id="d81d6-237">Add the Azure AD device authentication end-point to the local Intranet zones to avoid certificate prompts when authenticating the device.</span></span>

### <a name="set-policy-in-azure-ad-to-enable-users-to-register-devices"></a><span data-ttu-id="d81d6-238">Définir une stratégie dans Azure AD pour permettre aux utilisateurs d’inscrire des appareils</span><span class="sxs-lookup"><span data-stu-id="d81d6-238">Set policy in Azure AD to enable users to register devices</span></span>

<span data-ttu-id="d81d6-239">Pour inscrire des appareils Windows de bas niveau, vous devez vous assurer que le paramètre permettant aux utilisateurs d’inscrire des appareils dans Azure AD est défini.</span><span class="sxs-lookup"><span data-stu-id="d81d6-239">To register Windows down-level devices, you need to make sure that the setting to allow users to register devices in Azure AD is set.</span></span> <span data-ttu-id="d81d6-240">Dans le Portail Azure, ce paramètre est disponible à l’emplacement suivant :</span><span class="sxs-lookup"><span data-stu-id="d81d6-240">In the Azure portal, you can find this setting under:</span></span>

`Azure Active Directory > Users and groups > Device settings`
    
<span data-ttu-id="d81d6-241">La stratégie ci-après doit être définie sur la valeur **Tous** : **Les utilisateurs peuvent inscrire leurs appareils sur Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="d81d6-241">The following policy must be set to **All**: **Users may register their devices with Azure AD**</span></span>

![Inscrire des appareils](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a><span data-ttu-id="d81d6-243">Configurer le service de fédération local</span><span class="sxs-lookup"><span data-stu-id="d81d6-243">Configure on-premises federation service</span></span> 

<span data-ttu-id="d81d6-244">Votre service de fédération local doit prendre en charge l’émission des revendications **authenticationmehod** et **wiaormultiauthn** lors de la réception d’une demande d’authentification auprès de la partie de confiance Azure AD qui contient un paramètre resouce_params avec une valeur encodée comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d81d6-244">Your on-premises federation service must support issuing the **authenticationmehod** and **wiaormultiauthn** claims when receiving an authentication request to the Azure AD relying party holding a resouce_params parameter with an encoded value as shown below:</span></span>

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

<span data-ttu-id="d81d6-245">Lorsqu’une telle demande est reçue, le service de fédération local doit authentifier l’utilisateur à l’aide de l’authentification Windows intégrée et, en cas de réussite, doit émettre les deux revendications suivantes :</span><span class="sxs-lookup"><span data-stu-id="d81d6-245">When such a request comes, the on-premises federation service must authenticate the user using Integrated Windows Authentication and upon success, it must issue the following two claims:</span></span>

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

<span data-ttu-id="d81d6-246">Dans AD FS, vous devez ajouter une règle de transformation d’émission qui est transmise directement par le biais de la méthode d’authentification.</span><span class="sxs-lookup"><span data-stu-id="d81d6-246">In AD FS, you must add an issuance transform rule that passes-through the authentication method.</span></span>  

<span data-ttu-id="d81d6-247">**Pour ajouter cette règle :**</span><span class="sxs-lookup"><span data-stu-id="d81d6-247">**To add this rule:**</span></span>

1. <span data-ttu-id="d81d6-248">Dans la console de gestion AD FS, accédez à `AD FS > Trust Relationships > Relying Party Trusts`.</span><span class="sxs-lookup"><span data-stu-id="d81d6-248">In the AD FS management console, go to `AD FS > Trust Relationships > Relying Party Trusts`.</span></span>
2. <span data-ttu-id="d81d6-249">Cliquez avec le bouton droit sur l’objet d’approbation de partie de confiance de la plateforme d’identité Microsoft Office 365 et sélectionnez **Modifier les règles de revendication**.</span><span class="sxs-lookup"><span data-stu-id="d81d6-249">Right-click the Microsoft Office 365 Identity Platform relying party trust object, and then select **Edit Claim Rules**.</span></span>
3. <span data-ttu-id="d81d6-250">Sous l’onglet **Règles de transformation d’émission**, sélectionnez **Ajouter une règle**.</span><span class="sxs-lookup"><span data-stu-id="d81d6-250">On the **Issuance Transform Rules** tab, select **Add Rule**.</span></span>
4. <span data-ttu-id="d81d6-251">Sélectionnez **Envoyer les revendications en utilisant une règle personnalisée** dans la liste de modèles **Règle de revendication**.</span><span class="sxs-lookup"><span data-stu-id="d81d6-251">In the **Claim rule** template list, select **Send Claims Using a Custom Rule**.</span></span>
5. <span data-ttu-id="d81d6-252">Sélectionnez **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="d81d6-252">Select **Next**.</span></span>
6. <span data-ttu-id="d81d6-253">Dans la zone **Nom de la règle de revendication**, tapez **Règle de revendication de méthode d’authentification**.</span><span class="sxs-lookup"><span data-stu-id="d81d6-253">In the **Claim rule name** box, type **Auth Method Claim Rule**.</span></span>
7. <span data-ttu-id="d81d6-254">Dans la zone **Règle de revendication**, tapez la règle suivante :</span><span class="sxs-lookup"><span data-stu-id="d81d6-254">In the **Claim rule** box, type the following rule:</span></span>

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. <span data-ttu-id="d81d6-255">Sur votre serveur de fédération, tapez la commande PowerShell ci-dessous après avoir remplacé **\<RPObjectName\>** par le nom d’objet de partie de confiance de votre objet Approbation de partie de confiance Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d81d6-255">On your federation server, type the PowerShell command below after replacing **\<RPObjectName\>** with the relying party object name for your Azure AD relying party trust object.</span></span> <span data-ttu-id="d81d6-256">Cet objet est généralement nommé **plateforme d’identité Microsoft Office 365**.</span><span class="sxs-lookup"><span data-stu-id="d81d6-256">This object usually is named **Microsoft Office 365 Identity Platform**.</span></span>
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-the-azure-ad-device-authentication-end-point-to-the-local-intranet-zones"></a><span data-ttu-id="d81d6-257">Ajouter le point de terminaison d’authentification d’appareil Azure AD aux zones Intranet local</span><span class="sxs-lookup"><span data-stu-id="d81d6-257">Add the Azure AD device authentication end-point to the Local Intranet zones</span></span>

<span data-ttu-id="d81d6-258">Pour éviter les invites de certificat lorsque les utilisateurs des appareils inscrits s’authentifient auprès d’Azure AD, vous pouvez transmettre une stratégie à vos appareils joints à un domaine pour ajouter l’URL ci-après à la zone Intranet local dans Internet Explorer :</span><span class="sxs-lookup"><span data-stu-id="d81d6-258">To avoid certificate prompts when users in register devices authenticate to Azure AD you can push a policy to your domain-joined devices to add the following URL to the Local Intranet zone in Internet Explorer:</span></span>

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a><span data-ttu-id="d81d6-259">Étape 4 : Contrôle du déploiement et du lancement</span><span class="sxs-lookup"><span data-stu-id="d81d6-259">Step 4: Control deployment and rollout</span></span>

<span data-ttu-id="d81d6-260">Une fois que vous avez exécuté les étapes requises, les appareils joints à un domaine sont prêts à joindre automatiquement Azure AD :</span><span class="sxs-lookup"><span data-stu-id="d81d6-260">When you have completed the required steps, domain-joined devices are ready to automatically join Azure AD:</span></span>

- <span data-ttu-id="d81d6-261">Tous les appareils joints à un domaine qui exécutent Mise à jour anniversaire Windows 10 et Windows Server 2016 s’inscrivent automatiquement auprès d’Azure AD lors du redémarrage des appareils ou de la connexion des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="d81d6-261">All domain-joined devices running Windows 10 Anniversary Update and Windows Server 2016 automatically register with Azure AD at device restart or user sign-in.</span></span> 

- <span data-ttu-id="d81d6-262">Les nouveaux appareils s’inscrivent auprès d’Azure AD au moment de leur redémarrage une fois l’opération de jonction de domaine effectuée.</span><span class="sxs-lookup"><span data-stu-id="d81d6-262">New devices register with Azure AD when the device restarts after the domain join operation is completed.</span></span>

- <span data-ttu-id="d81d6-263">Les appareils qui ont fait précédemment l’objet d’une inscription auprès d’Azure AD (par exemple pour Intune) passent à l’état *« Joint au domaine, Enregistré avec AAD »*. Cependant, un certain temps est nécessaire pour que ce processus soit effectué sur tous les appareils, en raison du flux normal de l’activité du domaine et des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="d81d6-263">Devices that were previously Azure AD registered (for example, for Intune) transition to “*Domain Joined, AAD Registered*”; however it takes some time for this process to complete across all devices due to the normal flow of domain and user activity.</span></span>

### <a name="remarks"></a><span data-ttu-id="d81d6-264">Remarques</span><span class="sxs-lookup"><span data-stu-id="d81d6-264">Remarks</span></span>

- <span data-ttu-id="d81d6-265">Vous pouvez utiliser un objet de stratégie de groupe pour contrôler le déploiement de l’inscription automatique des ordinateurs Windows 10 et Windows Server 2016 joints à un domaine.</span><span class="sxs-lookup"><span data-stu-id="d81d6-265">You can use a Group Policy object to control the rollout of automatic registration of Windows 10 and Windows Server 2016 domain-joined computers.</span></span>

- <span data-ttu-id="d81d6-266">La mise à jour de novembre 2015 de Windows 10 effectue automatiquement la jonction à Azure AD **uniquement** si l’objet de stratégie de groupe de lancement est défini.</span><span class="sxs-lookup"><span data-stu-id="d81d6-266">Windows 10 November 2015 Update automatically joins with Azure AD **only** if the rollout Group Policy object is set.</span></span>

- <span data-ttu-id="d81d6-267">Pour un lancement des ordinateurs Windows de bas niveau, vous pouvez déployer un [package Windows Installer](#windows-installer-packages-for-non-windows-10-computers) sur les ordinateurs que vous sélectionnez.</span><span class="sxs-lookup"><span data-stu-id="d81d6-267">To rollout of Windows down-level computers, you can deploy a [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) to computers that you select.</span></span>

- <span data-ttu-id="d81d6-268">Si vous transmettez l’objet de stratégie de groupe à des appareils Windows 8.1 joints à un domaine, une tentative de jonction sera effectuée ; toutefois, il est recommandé d’utiliser le [package Windows Installer](#windows-installer-packages-for-non-windows-10-computers) pour joindre tous vos appareils Windows de bas niveau.</span><span class="sxs-lookup"><span data-stu-id="d81d6-268">If you push the Group Policy object to Windows 8.1 domain-joined devices, a join is attempted; however it is recommended that you use the [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) to join all your Windows down-level devices.</span></span> 

### <a name="create-a-group-policy-object"></a><span data-ttu-id="d81d6-269">Créer un objet de stratégie de groupe</span><span class="sxs-lookup"><span data-stu-id="d81d6-269">Create a Group Policy object</span></span> 

<span data-ttu-id="d81d6-270">Pour contrôler le lancement des ordinateurs Windows actuels, vous devez déployer l’objet de stratégie de groupe **Enregistrer les ordinateurs appartenant à un domaine en tant qu’appareils** sur les appareils que vous souhaitez inscrire.</span><span class="sxs-lookup"><span data-stu-id="d81d6-270">To control the rollout of Windows current computers, you should deploy the **Register domain-joined computers as devices** Group Policy object to the devices you want to register.</span></span> <span data-ttu-id="d81d6-271">Par exemple, vous pouvez déployer la stratégie sur un groupe de sécurité ou sur une unité organisationnelle.</span><span class="sxs-lookup"><span data-stu-id="d81d6-271">For example, you can deploy the policy to an organizational unit or to a security group.</span></span>

<span data-ttu-id="d81d6-272">**Pour configurer la stratégie :**</span><span class="sxs-lookup"><span data-stu-id="d81d6-272">**To set the policy:**</span></span>

1. <span data-ttu-id="d81d6-273">Ouvrez **Gestionnaire de serveur**, puis accédez à `Tools > Group Policy Management`.</span><span class="sxs-lookup"><span data-stu-id="d81d6-273">Open **Server Manager**, and then go to `Tools > Group Policy Management`.</span></span>
2. <span data-ttu-id="d81d6-274">Accédez au nœud de domaine qui correspond au domaine dans lequel vous souhaitez activer l’inscription automatique d’ordinateurs Windows actuels.</span><span class="sxs-lookup"><span data-stu-id="d81d6-274">Go to the domain node that corresponds to the domain where you want to activate auto-registration of Windows current computers.</span></span>
3. <span data-ttu-id="d81d6-275">Cliquez avec le bouton droit sur **Objets de stratégie de groupe**, puis sélectionnez **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="d81d6-275">Right-click **Group Policy Objects**, and then select **New**.</span></span>
4. <span data-ttu-id="d81d6-276">Entrez un nom pour votre objet de stratégie de groupe.</span><span class="sxs-lookup"><span data-stu-id="d81d6-276">Type a name for your Group Policy object.</span></span> <span data-ttu-id="d81d6-277">Par exemple, *jonction Azure AD hybride.</span><span class="sxs-lookup"><span data-stu-id="d81d6-277">For example, *Hybrid Azure AD join.</span></span> 
5. <span data-ttu-id="d81d6-278">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="d81d6-278">Click **OK**.</span></span>
6. <span data-ttu-id="d81d6-279">Cliquez avec le bouton droit sur votre nouvel objet de stratégie de groupe, puis sélectionnez **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="d81d6-279">Right-click your new Group Policy object, and then select **Edit**.</span></span>
7. <span data-ttu-id="d81d6-280">Accédez à **Configuration ordinateur** > **Stratégies** > **Modèles d’administration** > **Composants Windows** > **Enregistrement d’appareil**.</span><span class="sxs-lookup"><span data-stu-id="d81d6-280">Go to **Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Device Registration**.</span></span> 
8. <span data-ttu-id="d81d6-281">Cliquez avec le bouton droit sur **Enregistrer les ordinateurs appartenant à un domaine en tant qu’appareils**, puis sélectionnez **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="d81d6-281">Right-click **Register domain-joined computers as devices**, and then select **Edit**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d81d6-282">Ce modèle de stratégie de groupe a été renommé par rapport aux versions précédentes de la Console de gestion des stratégies de groupe.</span><span class="sxs-lookup"><span data-stu-id="d81d6-282">This Group Policy template has been renamed from earlier versions of the Group Policy Management console.</span></span> <span data-ttu-id="d81d6-283">Si vous utilisez une version antérieure de la console, accédez à `Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span><span class="sxs-lookup"><span data-stu-id="d81d6-283">If you are using an earlier version of the console, go to `Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span></span> 

7. <span data-ttu-id="d81d6-284">Sélectionnez **Activé**, puis cliquez sur **Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="d81d6-284">Select **Enabled**, and then click **Apply**.</span></span>
8. <span data-ttu-id="d81d6-285">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="d81d6-285">Click **OK**.</span></span>
9. <span data-ttu-id="d81d6-286">Liez l’objet de stratégie de groupe à un emplacement de votre choix.</span><span class="sxs-lookup"><span data-stu-id="d81d6-286">Link the Group Policy object to a location of your choice.</span></span> <span data-ttu-id="d81d6-287">Par exemple, vous pouvez le lier à une unité organisationnelle spécifique.</span><span class="sxs-lookup"><span data-stu-id="d81d6-287">For example, you can link it to a specific organizational unit.</span></span> <span data-ttu-id="d81d6-288">Vous pouvez également le lier à un groupe de sécurité spécifique d’ordinateurs qui rejoignent automatiquement Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d81d6-288">You also could link it to a specific security group of computers that automatically join with Azure AD.</span></span> <span data-ttu-id="d81d6-289">Pour définir cette stratégie pour tous les ordinateurs Windows 10 ou Windows Server 2016 joints à un domaine de votre organisation, liez l’objet de stratégie de groupe au domaine.</span><span class="sxs-lookup"><span data-stu-id="d81d6-289">To set this policy for all domain-joined Windows 10 and Windows Server 2016 computers in your organization, link the Group Policy object to the domain.</span></span>

### <a name="windows-installer-packages-for-non-windows-10-computers"></a><span data-ttu-id="d81d6-290">Packages Windows Installer pour les ordinateurs autres que Windows 10</span><span class="sxs-lookup"><span data-stu-id="d81d6-290">Windows Installer packages for non-Windows 10 computers</span></span>

<span data-ttu-id="d81d6-291">Pour joindre des ordinateurs Windows de bas niveau joints à un domaine dans un environnement fédéré, vous pouvez télécharger et installer ce package Windows Installer (.msi) à partir du Centre de téléchargement au niveau de la page [Microsoft Workplace Join for non-Windows 10 computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) (Jonction Microsoft Workplace pour les ordinateurs non Windows 10).</span><span class="sxs-lookup"><span data-stu-id="d81d6-291">To join domain-joined Windows down-level computers in a federated environment, you can download and install these Windows Installer package (.msi) from Download Center at the [Microsoft Workplace Join for non-Windows 10 computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) page.</span></span>

<span data-ttu-id="d81d6-292">Vous pouvez déployer le package à l’aide d’un système de distribution de logiciels comme System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="d81d6-292">You can deploy the package by using a software distribution system like System Center Configuration Manager.</span></span> <span data-ttu-id="d81d6-293">Le package prend en charge les options d’installation en mode silencieux standard avec le paramètre *quiet*.</span><span class="sxs-lookup"><span data-stu-id="d81d6-293">The package supports the standard silent install options with the *quiet* parameter.</span></span> <span data-ttu-id="d81d6-294">System Center Configuration Manager Current Branch offre des avantages supplémentaires par rapport aux versions précédentes, comme la possibilité d’effectuer le suivi des inscriptions terminées.</span><span class="sxs-lookup"><span data-stu-id="d81d6-294">System Center Configuration Manager Current Branch offers additional benefits from earlier versions, like the ability to track completed registrations.</span></span> <span data-ttu-id="d81d6-295">Pour plus d’informations, consultez l’article [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="d81d6-295">For more information, see [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span></span>

<span data-ttu-id="d81d6-296">Le programme d’installation crée une tâche planifiée sur le système, qui s’exécute dans le contexte de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d81d6-296">The installer creates a scheduled task on the system that runs in the user’s context.</span></span> <span data-ttu-id="d81d6-297">La tâche est déclenchée lorsque l’utilisateur se connecte à Windows.</span><span class="sxs-lookup"><span data-stu-id="d81d6-297">The task is triggered when the user signs in to Windows.</span></span> <span data-ttu-id="d81d6-298">La tâche assure la jonction de l’appareil en mode silencieux à Azure AD avec les informations d’identification de l’utilisateur après l’avoir authentifié à l’aide de l’authentification Windows intégrée.</span><span class="sxs-lookup"><span data-stu-id="d81d6-298">The task silently joins the device with Azure AD with the user credentials after authenticating using Integrated Windows Authentication.</span></span> <span data-ttu-id="d81d6-299">Pour visualiser la tâche planifiée, sélectionnez sur l’appareil **Microsoft** > **Rattacher à l’espace de travail**, puis accédez à la bibliothèque du Planificateur de tâches.</span><span class="sxs-lookup"><span data-stu-id="d81d6-299">To see the scheduled task, in the device, go to **Microsoft** > **Workplace Join**, and then go to the Task Scheduler library.</span></span>

## <a name="step-5-verify-joined-devices"></a><span data-ttu-id="d81d6-300">Étape 5 : Vérification des appareils joints</span><span class="sxs-lookup"><span data-stu-id="d81d6-300">Step 5: Verify joined devices</span></span>

<span data-ttu-id="d81d6-301">Vous pouvez vérifier les appareils qui ont été correctement joints dans votre organisation en utilisant l’applet de commande [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) dans le [module Azure Active Directory PowerShell](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="d81d6-301">You can check successful joined devices in your organization by using the [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in the [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span>

<span data-ttu-id="d81d6-302">La sortie de cette applet de commande affiche les appareils qui sont enregistrés et joints à Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d81d6-302">The output of this cmdlet shows devices that are registered and joined with Azure AD.</span></span> <span data-ttu-id="d81d6-303">Pour obtenir tous les appareils, utilisez le paramètre **-All**, puis filtrez-les à l’aide de la propriété **deviceTrustType**.</span><span class="sxs-lookup"><span data-stu-id="d81d6-303">To get all devices, use the **-All** parameter, and then filter them using the **deviceTrustType** property.</span></span> <span data-ttu-id="d81d6-304">Les appareils joints à un domaine présentent la valeur **Joint au domaine**.</span><span class="sxs-lookup"><span data-stu-id="d81d6-304">Domain joined devices have a value of **Domain Joined**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d81d6-305">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d81d6-305">Next steps</span></span>

* [<span data-ttu-id="d81d6-306">Présentation de la gestion des appareils dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d81d6-306">Introduction to device management in Azure Active Directory</span></span>](device-management-introduction.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
