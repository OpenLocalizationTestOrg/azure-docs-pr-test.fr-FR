---
title: "aaaHow tooconfigure l’inscription automatique des périphériques joints au domaine de Windows avec Azure Active Directory | Documents Microsoft"
description: "Configurer votre tooregister d’appareils Windows joints automatiquement et silencieusement avec Azure Active Directory."
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
ms.openlocfilehash: 6a1aab753f5456ed06ba7979ab05f70f29b4ddee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-automatic-registration-of-windows-domain-joined-devices-with-azure-active-directory"></a><span data-ttu-id="d7954-103">Comment tooconfigure l’inscription automatique de Windows appartenant au domaine des appareils avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d7954-103">How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory</span></span>

<span data-ttu-id="d7954-104">toouse [accès conditionnel périphérique Azure Active Directory](active-directory-conditional-access-azure-portal.md), vos ordinateurs doivent être inscrit auprès d’Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d7954-104">toouse [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md), your computers must be registered with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="d7954-105">Vous pouvez obtenir une liste des appareils inscrits dans votre organisation à l’aide de hello [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) applet de commande Bonjour [module Azure Active Directory PowerShell](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="d7954-105">You can get a list of registered devices in your organization by using hello [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in hello [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span> 

<span data-ttu-id="d7954-106">Cet article vous fournit les étapes hello pour la configuration de l’inscription automatique des périphériques joints au domaine de Windows hello avec Azure AD dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="d7954-106">This article provides you with hello steps for configuring hello automatic registration of Windows domain-joined devices with Azure AD in your organization.</span></span>


<span data-ttu-id="d7954-107">Le cas échéant, consultez les références suivantes :</span><span class="sxs-lookup"><span data-stu-id="d7954-107">For more information about:</span></span>

- <span data-ttu-id="d7954-108">Pour plus d’informations sur l’accès conditionnel, consultez l’article [Accès conditionnel dans Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d7954-108">Conditional access, see [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md).</span></span> 
- <span data-ttu-id="d7954-109">Les appareils Windows 10 dans l’espace de travail hello et expériences hello améliorée lorsque inscrit auprès d’Azure AD, consultez [Windows 10 pour les entreprises hello : utiliser des périphériques pour les travaux](active-directory-azureadjoin-windows10-devices-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d7954-109">Windows 10 devices in hello workplace and hello enhanced experiences when registered with Azure AD, see [Windows 10 for hello enterprise: Use devices for work](active-directory-azureadjoin-windows10-devices-overview.md).</span></span>
- <span data-ttu-id="d7954-110">Windows 10 entreprise E3 dans CSP, consultez hello [Windows 10 entreprise E3 dans vue d’ensemble du fournisseur de services cryptographiques](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).</span><span class="sxs-lookup"><span data-stu-id="d7954-110">Windows 10 Enterprise E3 in CSP, see hello [Windows 10 Enterprise E3 in CSP Overview](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="d7954-111">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="d7954-111">Before you begin</span></span>

<span data-ttu-id="d7954-112">Avant de commencer à configurer l’inscription automatique des périphériques joints au domaine de Windows hello dans votre environnement, vous devez vous familiariser avec les scénarios hello pris en charge et des contraintes de hello.</span><span class="sxs-lookup"><span data-stu-id="d7954-112">Before you start configuring hello automatic registration of Windows domain-joined devices in your environment, you should familiarize yourself with hello supported scenarios and hello constraints.</span></span>  

<span data-ttu-id="d7954-113">une meilleure lisibilité des hello tooimprove des descriptions de hello, cette rubrique utilise hello suivant le terme :</span><span class="sxs-lookup"><span data-stu-id="d7954-113">tooimprove hello readability of hello descriptions, this topic uses hello following term:</span></span> 

- <span data-ttu-id="d7954-114">**Les appareils Windows actuels** -ce terme fait référence à des appareils appartenant à un toodomain exécutant Windows 10 ou Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="d7954-114">**Windows current devices** - This term refers toodomain-joined devices running Windows 10 or Windows Server 2016.</span></span>
- <span data-ttu-id="d7954-115">**Les appareils Windows de bas niveau** -ce terme fait référence tooall **pris en charge** appareils Windows joints à un domaine qui sont en cours d’exécution Windows 10 ni Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="d7954-115">**Windows down-level devices** - This term refers tooall **supported** domain-joined Windows devices that are neither running Windows 10 nor Windows Server 2016.</span></span>  


### <a name="windows-current-devices"></a><span data-ttu-id="d7954-116">Appareils Windows actuels</span><span class="sxs-lookup"><span data-stu-id="d7954-116">Windows current devices</span></span>

- <span data-ttu-id="d7954-117">Pour les périphériques exécutant le système d’exploitation de bureau Windows hello, nous vous recommandons d’à l’aide de la mise à jour de la date anniversaire Windows 10 (version 1607) ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d7954-117">For devices running hello Windows desktop operating system, we recommend using Windows 10 Anniversary Update (version 1607) or later.</span></span> 
- <span data-ttu-id="d7954-118">Hello d’inscription d’appareils en cours de Windows **est** pris en charge dans les environnements non fédérées telles que les configurations de synchronisation de hachage de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="d7954-118">hello registration of Windows current devices **is** supported in non-federated environments such as password hash sync configurations.</span></span>  


### <a name="windows-down-level-devices"></a><span data-ttu-id="d7954-119">Appareils Windows de bas niveau</span><span class="sxs-lookup"><span data-stu-id="d7954-119">Windows down-level devices</span></span>

- <span data-ttu-id="d7954-120">Hello suivant de périphériques de bas niveau de Windows est prises en charge :</span><span class="sxs-lookup"><span data-stu-id="d7954-120">hello following Windows down-level devices are supported:</span></span>
    - <span data-ttu-id="d7954-121">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="d7954-121">Windows 8.1</span></span>
    - <span data-ttu-id="d7954-122">Windows 7</span><span class="sxs-lookup"><span data-stu-id="d7954-122">Windows 7</span></span>
    - <span data-ttu-id="d7954-123">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="d7954-123">Windows Server 2012 R2</span></span>
    - <span data-ttu-id="d7954-124">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="d7954-124">Windows Server 2012</span></span>
    - <span data-ttu-id="d7954-125">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="d7954-125">Windows Server 2008 R2</span></span>
- <span data-ttu-id="d7954-126">Hello d’inscription d’appareils de bas niveau Windows **est** pris en charge dans les environnements non fédérées via transparente Single Sign On [Azure Active Directory transparente l’authentification unique sur](https://aka.ms/hybrid/sso).</span><span class="sxs-lookup"><span data-stu-id="d7954-126">hello registration of Windows down-level devices **is** supported in non-federated environments through Seamless Single Sign On [Azure Active Directory Seamless Single Sign-On](https://aka.ms/hybrid/sso).</span></span>
- <span data-ttu-id="d7954-127">Hello d’inscription d’appareils de bas niveau Windows **n’est pas** pris en charge pour les appareils à l’aide de profils itinérants.</span><span class="sxs-lookup"><span data-stu-id="d7954-127">hello registration of Windows down-level devices **is not** supported for devices using roaming profiles.</span></span> <span data-ttu-id="d7954-128">Si vous vous appuyez sur l’itinérance de profils ou de paramètres, utilisez Windows 10.</span><span class="sxs-lookup"><span data-stu-id="d7954-128">If you are relying on roaming of profiles or settings, use Windows 10.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="d7954-129">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d7954-129">Prerequisites</span></span>

<span data-ttu-id="d7954-130">Avant de commencer l’activation hello-d’enregistrement automatique des appareils de joints au domaine de votre organisation, vous devez toomake que que vous exécutez une version à jour d’Azure AD se connecter.</span><span class="sxs-lookup"><span data-stu-id="d7954-130">Before you start enabling hello auto-registration of domain-joined devices in your organization, you need toomake sure that you are running an up-to-date version of Azure AD connect.</span></span>

<span data-ttu-id="d7954-131">Azure AD Connect :</span><span class="sxs-lookup"><span data-stu-id="d7954-131">Azure AD Connect:</span></span>

- <span data-ttu-id="d7954-132">Conserve l’association hello entre le compte d’ordinateur hello dans vos locaux Active Directory (AD) et un objet de périphérique hello dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7954-132">Keeps hello association between hello computer account in your on-premises Active Directory (AD) and hello device object in Azure AD.</span></span> 
- <span data-ttu-id="d7954-133">Permet d’utiliser d’autres fonctionnalités liées aux appareils telles que Windows Hello Entreprise.</span><span class="sxs-lookup"><span data-stu-id="d7954-133">Enables other device related features like Windows Hello for Business.</span></span>



## <a name="configuration-steps"></a><span data-ttu-id="d7954-134">Configuration</span><span class="sxs-lookup"><span data-stu-id="d7954-134">Configuration steps</span></span>

<span data-ttu-id="d7954-135">Cette rubrique comprend les étapes hello requis pour tous les scénarios courants de configuration.</span><span class="sxs-lookup"><span data-stu-id="d7954-135">This topic includes hello required steps for all typical configuration scenarios.</span></span>  
<span data-ttu-id="d7954-136">Utilisez hello suivant table tooget une vue d’ensemble des étapes hello qui sont requis pour votre scénario :</span><span class="sxs-lookup"><span data-stu-id="d7954-136">Use hello following table tooget an overview of hello steps that are required for your scenario:</span></span>  



| <span data-ttu-id="d7954-137">Étapes</span><span class="sxs-lookup"><span data-stu-id="d7954-137">Steps</span></span>                                      | <span data-ttu-id="d7954-138">Appareils Windows actuels et synchronisation du hachage de mot de passe</span><span class="sxs-lookup"><span data-stu-id="d7954-138">Windows current and password hash sync</span></span> | <span data-ttu-id="d7954-139">Appareils Windows actuels et fédération</span><span class="sxs-lookup"><span data-stu-id="d7954-139">Windows current and federation</span></span> | <span data-ttu-id="d7954-140">Appareils Windows de bas niveau</span><span class="sxs-lookup"><span data-stu-id="d7954-140">Windows down-level</span></span> |
| :--                                        | :-:                                    | :-:                            | :-:                |
| <span data-ttu-id="d7954-141">Étape 1 : Configuration du point de connexion de service</span><span class="sxs-lookup"><span data-stu-id="d7954-141">Step 1: Configure service connection point</span></span> | ![Vérification][1]                            | ![Vérification][1]                    | ![Vérification][1]        |
| <span data-ttu-id="d7954-145">Étape 2 : Configuration de l’émission de revendications</span><span class="sxs-lookup"><span data-stu-id="d7954-145">Step 2: Setup issuance of claims</span></span>           |                                        | ![Vérification][1]                    | ![Vérification][1]        |
| <span data-ttu-id="d7954-148">Étape 3 : Activation d’appareils non-Windows 10</span><span class="sxs-lookup"><span data-stu-id="d7954-148">Step 3: Enable non-Windows 10 devices</span></span>      |                                        |                                | ![Vérification][1]        |
| <span data-ttu-id="d7954-150">Étape 4 : Contrôle du déploiement et du lancement</span><span class="sxs-lookup"><span data-stu-id="d7954-150">Step 4: Control deployment and rollout</span></span>     | ![Vérification][1]                            | ![Vérification][1]                    | ![Vérification][1]        |
| <span data-ttu-id="d7954-154">Étape 5 : Vérification des appareils inscrits</span><span class="sxs-lookup"><span data-stu-id="d7954-154">Step 5: Verify registered devices</span></span>          | ![Vérification][1]                            | ![Vérification][1]                    | ![Vérification][1]        |



## <a name="step-1-configure-service-connection-point"></a><span data-ttu-id="d7954-158">Étape 1 : Configuration du point de connexion de service</span><span class="sxs-lookup"><span data-stu-id="d7954-158">Step 1: Configure service connection point</span></span>

<span data-ttu-id="d7954-159">objet de point de connexion de service Hello est utilisé par vos périphériques pendant l’inscription de hello toodiscover informations du locataire Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7954-159">hello service connection point (SCP) object is used by your devices during hello registration toodiscover Azure AD tenant information.</span></span> <span data-ttu-id="d7954-160">Dans vos locaux Active Directory (AD), objet SCP hello hello-d’enregistrement automatique des appareils joints au domaine doit exister dans hello d’affectation de noms contexte partition de configuration de la forêt de l’ordinateur hello.</span><span class="sxs-lookup"><span data-stu-id="d7954-160">In your on-premises Active Directory (AD), hello SCP object for hello auto-registration of domain-joined devices must exist in hello configuration naming context partition of hello computer's forest.</span></span> <span data-ttu-id="d7954-161">Il n’existe qu’un seul contexte d’appellation de configuration par forêt.</span><span class="sxs-lookup"><span data-stu-id="d7954-161">There is only one configuration naming context per forest.</span></span> <span data-ttu-id="d7954-162">Dans une configuration d’Active Directory de forêts multiples, le point de connexion de service hello doit exister dans toutes les forêts contenant des ordinateurs joints au domaine.</span><span class="sxs-lookup"><span data-stu-id="d7954-162">In a multi-forest Active Directory configuration, hello service connection point must exist in all forests containing domain-joined computers.</span></span>

<span data-ttu-id="d7954-163">Vous pouvez utiliser hello [ **Get-ADRootDSE** ](https://technet.microsoft.com/library/ee617246.aspx) applet de commande tooretrieve hello configuration contexte d’appellation de votre forêt.</span><span class="sxs-lookup"><span data-stu-id="d7954-163">You can use hello [**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx) cmdlet tooretrieve hello configuration naming context of your forest.</span></span>  

<span data-ttu-id="d7954-164">Pour une forêt avec le nom de domaine Active Directory hello *fabrikam.com*, contexte d’appellation de configuration hello est :</span><span class="sxs-lookup"><span data-stu-id="d7954-164">For a forest with hello Active Directory domain name *fabrikam.com*, hello configuration naming context is:</span></span>

`CN=Configuration,DC=fabrikam,DC=com`

<span data-ttu-id="d7954-165">Dans votre forêt, objet hello SCP pour hello auto-inscription de périphériques joints au domaine se trouve dans :</span><span class="sxs-lookup"><span data-stu-id="d7954-165">In your forest, hello SCP object for hello auto-registration of domain-joined devices is located at:</span></span>  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

<span data-ttu-id="d7954-166">Selon la façon dont vous avez déployé Azure AD Connect, objet de SCP hello peut ont déjà été configurée.</span><span class="sxs-lookup"><span data-stu-id="d7954-166">Depending on how you have deployed Azure AD Connect, hello SCP object may have already been configured.</span></span>
<span data-ttu-id="d7954-167">Vous pouvez vérifier l’existence de hello d’objet de hello et récupérer des valeurs de découverte hello à l’aide de hello Windows PowerShell script suivant :</span><span class="sxs-lookup"><span data-stu-id="d7954-167">You can verify hello existence of hello object and retrieve hello discovery values using hello following Windows PowerShell script:</span></span> 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

<span data-ttu-id="d7954-168">Hello **$scp. Mots clés** sortie affiche les informations du locataire hello Azure AD, par exemple :</span><span class="sxs-lookup"><span data-stu-id="d7954-168">hello **$scp.Keywords** output shows hello Azure AD tenant information, for example:</span></span>

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

<span data-ttu-id="d7954-169">Si le point de connexion de service hello n’existe pas, vous pouvez le créer en exécutant hello `Initialize-ADSyncDomainJoinedComputerSync` applet de commande sur votre serveur Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d7954-169">If hello service connection point does not exist, you can create it by running hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet on your Azure AD Connect server.</span></span> <span data-ttu-id="d7954-170">Informations d’identification de Enterprise admin est obligatoire toorun cette applet de commande.</span><span class="sxs-lookup"><span data-stu-id="d7954-170">Enterprise admin credential is required toorun this cmdlet.</span></span>  
<span data-ttu-id="d7954-171">applet de commande Hello :</span><span class="sxs-lookup"><span data-stu-id="d7954-171">hello cmdlet:</span></span>

- <span data-ttu-id="d7954-172">Crée le point de connexion de service hello dans la forêt Active Directory de hello À qu'azure AD Connect est connecté.</span><span class="sxs-lookup"><span data-stu-id="d7954-172">Creates hello service connection point in hello Active Directory forest Azure AD Connect is connected to.</span></span> 
- <span data-ttu-id="d7954-173">Requiert que vous toospecify hello `AdConnectorAccount` paramètre.</span><span class="sxs-lookup"><span data-stu-id="d7954-173">Requires you toospecify hello `AdConnectorAccount` parameter.</span></span> <span data-ttu-id="d7954-174">Il s’agit de compte hello qui est configuré en tant que compte de connecteur dans Azure AD de se connecter de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d7954-174">This is hello account that is configured as Active Directory connector account in Azure AD connect.</span></span> 


<span data-ttu-id="d7954-175">Hello script suivant montre un exemple d’utilisation d’applet de commande hello.</span><span class="sxs-lookup"><span data-stu-id="d7954-175">hello following script shows an example for using hello cmdlet.</span></span> <span data-ttu-id="d7954-176">Dans ce script, `$aadAdminCred = Get-Credential` nécessite que vous tootype un nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d7954-176">In this script, `$aadAdminCred = Get-Credential` requires you tootype a user name.</span></span> <span data-ttu-id="d7954-177">Vous avez besoin de nom d’utilisateur hello tooprovide hello format nom utilisateur principal (UPN) (`user@example.com`).</span><span class="sxs-lookup"><span data-stu-id="d7954-177">You need tooprovide hello user name in hello user principal name (UPN) format (`user@example.com`).</span></span> 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

<span data-ttu-id="d7954-178">Hello `Initialize-ADSyncDomainJoinedComputerSync` applet de commande :</span><span class="sxs-lookup"><span data-stu-id="d7954-178">hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span></span>

- <span data-ttu-id="d7954-179">Utilise le module Active Directory PowerShell hello, qui s’appuie sur les Services Web Active Directory s’exécutant sur un contrôleur de domaine.</span><span class="sxs-lookup"><span data-stu-id="d7954-179">Uses hello Active Directory PowerShell module, which relies on Active Directory Web Services running on a domain controller.</span></span> <span data-ttu-id="d7954-180">Les services Web Active Directory sont pris en charge sur les contrôleurs de domaine exécutant Windows Server 2008 R2 et les versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="d7954-180">Active Directory Web Services is supported on domain controllers running Windows Server 2008 R2 and later.</span></span>
- <span data-ttu-id="d7954-181">Est uniquement pris en charge par hello **MSOnline PowerShell version du module 1.1.166.0**.</span><span class="sxs-lookup"><span data-stu-id="d7954-181">Is only supported by hello **MSOnline PowerShell module version 1.1.166.0**.</span></span> <span data-ttu-id="d7954-182">toodownload ce module, utilisez cette [lien](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span><span class="sxs-lookup"><span data-stu-id="d7954-182">toodownload this module, use this [link](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span></span>   

<span data-ttu-id="d7954-183">Pour les contrôleurs de domaine exécutant Windows Server 2008 ou versions antérieures, utilisez le script de hello sous le point de connexion de service toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="d7954-183">For domain controllers running Windows Server 2008 or earlier versions, use hello script below toocreate hello service connection point.</span></span>

<span data-ttu-id="d7954-184">Dans une configuration à plusieurs forêts, vous devez utiliser hello suivant le point de connexion de service script toocreate hello dans chaque forêt où les ordinateurs existent :</span><span class="sxs-lookup"><span data-stu-id="d7954-184">In a multi-forest configuration, you should use hello following script toocreate hello service connection point in each forest where computers exist:</span></span>
 
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


## <a name="step-2-setup-issuance-of-claims"></a><span data-ttu-id="d7954-185">Étape 2 : Configuration de l’émission de revendications</span><span class="sxs-lookup"><span data-stu-id="d7954-185">Step 2: Setup issuance of claims</span></span>

<span data-ttu-id="d7954-186">Dans Azure fédéré configuration d’Active Directory, les appareils s’appuient sur les Services de fédération Active Directory (AD FS) ou un tiers 3e localement tooAzure de tooauthenticate service de fédération Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d7954-186">In a federated Azure AD configuration, devices rely on Active Directory Federation Services (AD FS) or a 3rd party on-premises federation service tooauthenticate tooAzure AD.</span></span> <span data-ttu-id="d7954-187">Les appareils s’authentifient tooget un tooregister de jeton d’accès contre hello Azure Active Directory Device Registration Service (DRS Azure).</span><span class="sxs-lookup"><span data-stu-id="d7954-187">Devices authenticate tooget an access token tooregister against hello Azure Active Directory Device Registration Service (Azure DRS).</span></span>

<span data-ttu-id="d7954-188">Les appareils en cours s’authentifient à l’aide de l’authentification Windows intégrée tooan WS-Trust point de terminaison actif (versions 1.3 ou 2005) hébergé par le service de fédération local hello de Windows.</span><span class="sxs-lookup"><span data-stu-id="d7954-188">Windows current devices authenticate using Integrated Windows Authentication tooan active WS-Trust endpoint (either 1.3 or 2005 versions) hosted by hello on-premises federation service.</span></span>

> [!NOTE]
> <span data-ttu-id="d7954-189">En cas d’utilisation d’AD FS, il est nécessaire d’activer **adfs/services/trust/13/windowstransport** ou **adfs/services/trust/2005/windowstransport**.</span><span class="sxs-lookup"><span data-stu-id="d7954-189">When using AD FS, either **adfs/services/trust/13/windowstransport** or **adfs/services/trust/2005/windowstransport** must be enabled.</span></span> <span data-ttu-id="d7954-190">Si vous utilisez hello Web d’authentification Proxy, vérifiez également que ce point de terminaison est publié via le proxy hello.</span><span class="sxs-lookup"><span data-stu-id="d7954-190">If you are using hello Web Authentication Proxy, also ensure that this endpoint is published through hello proxy.</span></span> <span data-ttu-id="d7954-191">Vous pouvez voir les points d’arrêt sont activés via la console de gestion hello AD FS sous **Service > points de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="d7954-191">You can see what end-points are enabled through hello AD FS management console under **Service > Endpoints**.</span></span>
>
><span data-ttu-id="d7954-192">Si vous n’avez pas AD FS en tant que votre service de fédération local, suivez les instructions de hello de votre fournisseur de toomake assurer qu’ils prennent en charge WS-Trust 1.3 ou des points de terminaison 2005 et qu’ils sont publiés via hello fichier d’échange de métadonnées (MEX).</span><span class="sxs-lookup"><span data-stu-id="d7954-192">If you don’t have AD FS as your on-premises federation service, follow hello instructions of your vendor toomake sure they support WS-Trust 1.3 or 2005 end-points and that these are published through hello Metadata Exchange file (MEX).</span></span>

<span data-ttu-id="d7954-193">Hello revendications suivantes doivent exister dans le jeton hello reçue par le service DRS Azure pour toocomplete d’inscription de périphérique.</span><span class="sxs-lookup"><span data-stu-id="d7954-193">hello following claims must exist in hello token received by Azure DRS for device registration toocomplete.</span></span> <span data-ttu-id="d7954-194">DRS Azure crée un objet de périphérique dans Azure AD avec certaines de ces informations sont ensuite utilisées par l’objet de périphérique Azure AD Connect tooassociate hello nouvellement créée avec hello ordinateur compte local.</span><span class="sxs-lookup"><span data-stu-id="d7954-194">Azure DRS will create a device object in Azure AD with some of this information which is then used by Azure AD Connect tooassociate hello newly created device object with hello computer account on-premises.</span></span>

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

<span data-ttu-id="d7954-195">Si vous avez plusieurs noms de domaine vérifié, vous devez hello tooprovide suivant revendication pour les ordinateurs :</span><span class="sxs-lookup"><span data-stu-id="d7954-195">If you have more than one verified domain name, you need tooprovide hello following claim for computers:</span></span>

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

<span data-ttu-id="d7954-196">Si vous émettez déjà une revendication ImmutableID (par exemple, les ID de connexion de substitution), vous devez tooprovide une revendication correspondante pour les ordinateurs :</span><span class="sxs-lookup"><span data-stu-id="d7954-196">If you are already issuing an ImmutableID claim (e.g., alternate login ID) you need tooprovide one corresponding claim for computers:</span></span>

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

<span data-ttu-id="d7954-197">Dans les sections suivantes de hello, trouver des informations sur :</span><span class="sxs-lookup"><span data-stu-id="d7954-197">In hello following sections, you find information about:</span></span>
 
- <span data-ttu-id="d7954-198">les valeurs Hello chaque revendication doit avoir.</span><span class="sxs-lookup"><span data-stu-id="d7954-198">hello values each claim should have</span></span>
- <span data-ttu-id="d7954-199">L’aspect d’une définition dans AD FS</span><span class="sxs-lookup"><span data-stu-id="d7954-199">How a definition would look like in AD FS</span></span>

<span data-ttu-id="d7954-200">définition de Hello vous aide à tooverify si les valeurs hello sont présentes, ou si vous avez besoin de toocreate les.</span><span class="sxs-lookup"><span data-stu-id="d7954-200">hello definition helps you tooverify whether hello values are present or if you need toocreate them.</span></span>

> [!NOTE]
> <span data-ttu-id="d7954-201">Si vous n’utilisez pas AD FS pour votre serveur de fédération local, suivez tooissue de configuration approprié de votre fournisseur instructions toocreate hello ces revendications.</span><span class="sxs-lookup"><span data-stu-id="d7954-201">If you don’t use AD FS for your on-premises federation server, follow your vendor's instructions toocreate hello appropriate configuration tooissue these claims.</span></span>

### <a name="issue-account-type-claim"></a><span data-ttu-id="d7954-202">Émission de la revendication du type de compte</span><span class="sxs-lookup"><span data-stu-id="d7954-202">Issue account type claim</span></span>

<span data-ttu-id="d7954-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`**-Cette revendication doit contenir une valeur de **DJ**, qui identifie le périphérique hello en tant qu’un ordinateur joint au domaine.</span><span class="sxs-lookup"><span data-stu-id="d7954-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`** - This claim must contain a value of **DJ**, which identifies hello device as a domain-joined computer.</span></span> <span data-ttu-id="d7954-204">Dans AD FS, vous pouvez ajouter une règle de transformation d’émission ressemblant à ceci :</span><span class="sxs-lookup"><span data-stu-id="d7954-204">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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

### <a name="issue-objectguid-of-hello-computer-account-on-premises"></a><span data-ttu-id="d7954-205">ObjectGUID de problème de hello ordinateur compte local</span><span class="sxs-lookup"><span data-stu-id="d7954-205">Issue objectGUID of hello computer account on-premises</span></span>

<span data-ttu-id="d7954-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`**-Cette revendication doit contenir hello **objectGUID** valeur Hello local compte d’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d7954-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`** - This claim must contain hello **objectGUID** value of hello on-premises computer account.</span></span> <span data-ttu-id="d7954-207">Dans AD FS, vous pouvez ajouter une règle de transformation d’émission ressemblant à ceci :</span><span class="sxs-lookup"><span data-stu-id="d7954-207">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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
 
### <a name="issue-objectsid-of-hello-computer-account-on-premises"></a><span data-ttu-id="d7954-208">Émettre objectSID de hello ordinateur compte local</span><span class="sxs-lookup"><span data-stu-id="d7954-208">Issue objectSID of hello computer account on-premises</span></span>

<span data-ttu-id="d7954-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`**-Cette revendication doit contenir Bonjour Bonjour **objectSid** valeur Hello local compte d’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d7954-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`** - This claim must contain hello hello **objectSid** value of hello on-premises computer account.</span></span> <span data-ttu-id="d7954-210">Dans AD FS, vous pouvez ajouter une règle de transformation d’émission ressemblant à ceci :</span><span class="sxs-lookup"><span data-stu-id="d7954-210">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a><span data-ttu-id="d7954-211">Émission de la valeur issuerID pour l’ordinateur s’il existe plusieurs noms de domaine vérifiés dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7954-211">Issue issuerID for computer when multiple verified domain names in Azure AD</span></span>

<span data-ttu-id="d7954-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`**-Cette revendication doit contenir hello identificateur URI (Uniform Resource) de n’importe quel Hello vérifié les noms de domaine qui se connectent avec hello localement le jeton de hello émettrice federation Services (AD FS ou 3e partie).</span><span class="sxs-lookup"><span data-stu-id="d7954-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`** - This claim must contain hello Uniform Resource Identifier (URI) of any of hello verified domain names that connect with hello on-premises federation service (AD FS or 3rd party) issuing hello token.</span></span> <span data-ttu-id="d7954-213">Dans AD FS, vous pouvez ajouter des règles de transformation d’émission qui ressemblent à celles hello ci-dessous dans la mesure où un ordre spécifique après ceux hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="d7954-213">In AD FS, you can add issuance transform rules that look like hello ones below in that specific order after hello ones above.</span></span> <span data-ttu-id="d7954-214">Notez qu’un tooexplicitly problème hello la règle pour les utilisateurs est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d7954-214">Please note that one rule tooexplicitly issue hello rule for users is necessary.</span></span> <span data-ttu-id="d7954-215">Dans les règles de hello ci-dessous, une première règle identifiant utilisateur ou l’authentification d’ordinateur est ajoutée.</span><span class="sxs-lookup"><span data-stu-id="d7954-215">In hello rules below, a first rule identifying user vs. computer authentication is added.</span></span>

    @RuleName = "Issue account type with hello value User when its not a computer"
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
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
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


<span data-ttu-id="d7954-216">Dans la revendication hello ci-dessus,</span><span class="sxs-lookup"><span data-stu-id="d7954-216">In hello claim above,</span></span>

- <span data-ttu-id="d7954-217">`$<domain>`est l’URL du service hello AD FS</span><span class="sxs-lookup"><span data-stu-id="d7954-217">`$<domain>` is hello AD FS service URL</span></span>
- <span data-ttu-id="d7954-218">`<verified-domain-name>`est un espace réservé que vous avez besoin de tooreplace avec l’un de vos noms de domaine vérifié dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7954-218">`<verified-domain-name>` is a placeholder you need tooreplace with one of your verified domain names in Azure AD</span></span>



<span data-ttu-id="d7954-219">Pour plus d’informations sur les noms de domaine vérifié, consultez [ajouter un tooAzure de nom de domaine personnalisé Active Directory](active-directory-add-domain.md).</span><span class="sxs-lookup"><span data-stu-id="d7954-219">For more details about verified domain names, see [Add a custom domain name tooAzure Active Directory](active-directory-add-domain.md).</span></span>  
<span data-ttu-id="d7954-220">tooget une liste de vos domaines de société vérifiés, vous pouvez utiliser hello [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="d7954-220">tooget a list of your verified company domains, you can use hello [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span></span> 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a><span data-ttu-id="d7954-222">Émission de la valeur ImmutableID pour l’ordinateur s’il en existe une pour les utilisateurs (par exemple, définition d’un ID de connexion alternatif)</span><span class="sxs-lookup"><span data-stu-id="d7954-222">Issue ImmutableID for computer when one for users exist (e.g. alternate login ID is set)</span></span>

<span data-ttu-id="d7954-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** : cette revendication doit contenir une valeur valide pour les ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="d7954-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - This claim must contain a valid value for computers.</span></span> <span data-ttu-id="d7954-224">Dans AD FS, vous pouvez créer une règle de transformation d’émission comme suit :</span><span class="sxs-lookup"><span data-stu-id="d7954-224">In AD FS, you can create an issuance transform rule as follows:</span></span>

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

### <a name="helper-script-toocreate-hello-ad-fs-issuance-transform-rules"></a><span data-ttu-id="d7954-225">Règles de transformation d’émission d’application d’assistance script toocreate hello AD FS</span><span class="sxs-lookup"><span data-stu-id="d7954-225">Helper script toocreate hello AD FS issuance transform rules</span></span>

<span data-ttu-id="d7954-226">Hello script suivant vous aide à avec création de hello d’émission de hello transformer les règles décrites ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="d7954-226">hello following script helps you with hello creation of hello issuance transform rules described above.</span></span>

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
    $rule4 = '@RuleName = "Issue account type with hello value User when it is not a computer"
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
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
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

### <a name="remarks"></a><span data-ttu-id="d7954-227">Remarques</span><span class="sxs-lookup"><span data-stu-id="d7954-227">Remarks</span></span> 

- <span data-ttu-id="d7954-228">Ce script ajoute des règles existantes de hello règles toohello.</span><span class="sxs-lookup"><span data-stu-id="d7954-228">This script appends hello rules toohello existing rules.</span></span> <span data-ttu-id="d7954-229">N’exécutez ne pas hello script à deux reprises car hello ensemble de règles est ajouté à deux reprises.</span><span class="sxs-lookup"><span data-stu-id="d7954-229">Do not run hello script twice because hello set of rules would be added twice.</span></span> <span data-ttu-id="d7954-230">Assurez-vous qu’aucune règle correspondant n’existe pour ces revendications (dans des conditions hello) avant de réexécuter le script de hello.</span><span class="sxs-lookup"><span data-stu-id="d7954-230">Make sure that no corresponding rules exist for these claims (under hello corresponding conditions) before running hello script again.</span></span>

- <span data-ttu-id="d7954-231">Si vous avez plusieurs noms de domaine vérifié (comme indiqué dans le portail de hello Azure AD ou via l’applet de commande Get-MsolDomains de hello), valeur hello **$multipleVerifiedDomainNames** Bonjour script trop**$true**.</span><span class="sxs-lookup"><span data-stu-id="d7954-231">If you have multiple verified domain names (as shown in hello Azure AD portal or via hello Get-MsolDomains cmdlet), set hello value of **$multipleVerifiedDomainNames** in hello script too**$true**.</span></span> <span data-ttu-id="d7954-232">Veillez également à supprimer toute revendication issuerid existante pouvant avoir été créée par Azure AD Connect ou par d’autres moyens.</span><span class="sxs-lookup"><span data-stu-id="d7954-232">Also make sure that you remove any existing issuerid claim that might have been created by Azure AD Connect or via other means.</span></span> <span data-ttu-id="d7954-233">Voici un exemple de cette règle :</span><span class="sxs-lookup"><span data-stu-id="d7954-233">Here is an example for this rule:</span></span>


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- <span data-ttu-id="d7954-234">Si vous avez déjà émis un **ImmutableID** de revendication pour les comptes d’utilisateur, la valeur hello **$immutableIDAlreadyIssuedforUsers** Bonjour script trop**$true**.</span><span class="sxs-lookup"><span data-stu-id="d7954-234">If you have already issued an **ImmutableID** claim  for user accounts, set hello value of **$immutableIDAlreadyIssuedforUsers** in hello script too**$true**.</span></span>

## <a name="step-3-enable-windows-down-level-devices"></a><span data-ttu-id="d7954-235">Étape 3 : Activation des appareils Windows de bas niveau</span><span class="sxs-lookup"><span data-stu-id="d7954-235">Step 3: Enable Windows down-level devices</span></span>

<span data-ttu-id="d7954-236">Si certains de vos appareils joints à un domaine sont des appareils Windows de bas niveau, vous devez :</span><span class="sxs-lookup"><span data-stu-id="d7954-236">If some of your domain-joined devices Windows down-level devices, you need to:</span></span>

- <span data-ttu-id="d7954-237">Définir une stratégie dans Azure AD tooenable tooregister les appareils des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="d7954-237">Set a policy in Azure AD tooenable users tooregister devices.</span></span>
 
- <span data-ttu-id="d7954-238">Configurer votre toosupport revendications tooissue de service de fédération local **l’authentification Windows (intégrée)** pour l’inscription de périphérique.</span><span class="sxs-lookup"><span data-stu-id="d7954-238">Configure your on-premises federation service tooissue claims toosupport **Integrated Windows Authentication (IWA)** for device registration.</span></span>
 
- <span data-ttu-id="d7954-239">Ajoutez des hello Azure AD appareil authentification point de terminaison toohello local Intranet zones tooavoid certificat invite lors de l’authentification d’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="d7954-239">Add hello Azure AD device authentication end-point toohello local Intranet zones tooavoid certificate prompts when authenticating hello device.</span></span>

### <a name="set-policy-in-azure-ad-tooenable-users-tooregister-devices"></a><span data-ttu-id="d7954-240">Définir la stratégie dans Azure AD tooenable tooregister les appareils des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="d7954-240">Set policy in Azure AD tooenable users tooregister devices</span></span>

<span data-ttu-id="d7954-241">périphériques de bas niveau tooregister Windows, vous devez toomake que ce hello définissant tooallow utilisateurs tooregister appareils dans Azure AD est défini.</span><span class="sxs-lookup"><span data-stu-id="d7954-241">tooregister Windows down-level devices, you need toomake sure that hello setting tooallow users tooregister devices in Azure AD is set.</span></span> <span data-ttu-id="d7954-242">Bonjour portail Azure, vous pouvez trouver ce paramètre sous :</span><span class="sxs-lookup"><span data-stu-id="d7954-242">In hello Azure portal, you can find this setting under:</span></span>

`Azure Active Directory > Users and groups > Device settings`
    
<span data-ttu-id="d7954-243">Hello stratégie suivante doit être défini trop**tous les**: **les utilisateurs peuvent inscrire leurs appareils auprès d’Azure AD**</span><span class="sxs-lookup"><span data-stu-id="d7954-243">hello following policy must be set too**All**: **Users may register their devices with Azure AD**</span></span>

![Inscrire des appareils](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a><span data-ttu-id="d7954-245">Configurer le service de fédération local</span><span class="sxs-lookup"><span data-stu-id="d7954-245">Configure on-premises federation service</span></span> 

<span data-ttu-id="d7954-246">Votre service de fédération local doit prendre en charge hello émettrice **authenticationmehod** et **wiaormultiauthn** revendications lors de la réception d’une authentification demande toohello Azure AD de confiance contenant un resouce_params paramètre avec une valeur codée comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d7954-246">Your on-premises federation service must support issuing hello **authenticationmehod** and **wiaormultiauthn** claims when receiving an authentication request toohello Azure AD relying party holding a resouce_params parameter with an encoded value as shown below:</span></span>

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

<span data-ttu-id="d7954-247">Lorsqu’une telle demande est fourni, service de fédération local hello doit authentifier l’utilisateur hello à l’aide de l’authentification Windows intégrée et en cas de réussite, elle doit émettre hello suivant deux revendications :</span><span class="sxs-lookup"><span data-stu-id="d7954-247">When such a request comes, hello on-premises federation service must authenticate hello user using Integrated Windows Authentication and upon success, it must issue hello following two claims:</span></span>

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

<span data-ttu-id="d7954-248">Dans AD FS, vous devez ajouter une règle de transformation d’émission de cette méthode d’authentification transmet via hello.</span><span class="sxs-lookup"><span data-stu-id="d7954-248">In AD FS, you must add an issuance transform rule that passes-through hello authentication method.</span></span>  

<span data-ttu-id="d7954-249">**tooadd cette règle :**</span><span class="sxs-lookup"><span data-stu-id="d7954-249">**tooadd this rule:**</span></span>

1. <span data-ttu-id="d7954-250">Dans la console de gestion hello AD FS, accédez trop`AD FS > Trust Relationships > Relying Party Trusts`.</span><span class="sxs-lookup"><span data-stu-id="d7954-250">In hello AD FS management console, go too`AD FS > Trust Relationships > Relying Party Trusts`.</span></span>
2. <span data-ttu-id="d7954-251">Objet d’approbation de partie de confiance de plateforme d’identité Microsoft Office 365 hello d’avec le bouton droit et sélectionnez **modifier les règles de revendication**.</span><span class="sxs-lookup"><span data-stu-id="d7954-251">Right-click hello Microsoft Office 365 Identity Platform relying party trust object, and then select **Edit Claim Rules**.</span></span>
3. <span data-ttu-id="d7954-252">Sur hello **règles de transformation d’émission** onglet, sélectionnez **ajouter une règle**.</span><span class="sxs-lookup"><span data-stu-id="d7954-252">On hello **Issuance Transform Rules** tab, select **Add Rule**.</span></span>
4. <span data-ttu-id="d7954-253">Bonjour **règle de revendication** liste des modèles, sélectionnez **envoyer des revendications à l’aide d’une règle personnalisée**.</span><span class="sxs-lookup"><span data-stu-id="d7954-253">In hello **Claim rule** template list, select **Send Claims Using a Custom Rule**.</span></span>
5. <span data-ttu-id="d7954-254">Sélectionnez **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="d7954-254">Select **Next**.</span></span>
6. <span data-ttu-id="d7954-255">Bonjour **nom de règle de revendication** , tapez **règle de revendication de méthode d’authentification**.</span><span class="sxs-lookup"><span data-stu-id="d7954-255">In hello **Claim rule name** box, type **Auth Method Claim Rule**.</span></span>
7. <span data-ttu-id="d7954-256">Bonjour **règle de revendication** boîte, hello type règle :</span><span class="sxs-lookup"><span data-stu-id="d7954-256">In hello **Claim rule** box, type hello following rule:</span></span>

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. <span data-ttu-id="d7954-257">Sur votre serveur de fédération, tapez la commande PowerShell de hello ci-dessous après le remplacement  **\<RPObjectName\>**  avec hello partie de confiance nom de l’objet pour votre objet Azure AD approbation de partie de confiance.</span><span class="sxs-lookup"><span data-stu-id="d7954-257">On your federation server, type hello PowerShell command below after replacing **\<RPObjectName\>** with hello relying party object name for your Azure AD relying party trust object.</span></span> <span data-ttu-id="d7954-258">Cet objet est généralement nommé **plateforme d’identité Microsoft Office 365**.</span><span class="sxs-lookup"><span data-stu-id="d7954-258">This object usually is named **Microsoft Office 365 Identity Platform**.</span></span>
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-hello-azure-ad-device-authentication-end-point-toohello-local-intranet-zones"></a><span data-ttu-id="d7954-259">Ajouter des zones Intranet Local de hello Azure AD appareil authentification point d’arrêt toohello</span><span class="sxs-lookup"><span data-stu-id="d7954-259">Add hello Azure AD device authentication end-point toohello Local Intranet zones</span></span>

<span data-ttu-id="d7954-260">certificat de tooavoid invite lorsque les utilisateurs de périphériques de Registre authentifient tooAzure AD, vous pouvez transmettre un Bonjour de tooadd stratégie tooyour périphériques joints au domaine suivant la zone d’Intranet Local toohello URL dans Internet Explorer :</span><span class="sxs-lookup"><span data-stu-id="d7954-260">tooavoid certificate prompts when users in register devices authenticate tooAzure AD you can push a policy tooyour domain-joined devices tooadd hello following URL toohello Local Intranet zone in Internet Explorer:</span></span>

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a><span data-ttu-id="d7954-261">Étape 4 : Contrôle du déploiement et du lancement</span><span class="sxs-lookup"><span data-stu-id="d7954-261">Step 4: Control deployment and rollout</span></span>

<span data-ttu-id="d7954-262">Lorsque vous avez terminé les étapes de hello requis, les périphériques joints au domaine sont register tooautomatically prêt avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7954-262">When you have completed hello required steps, domain-joined devices are ready tooautomatically register with Azure AD.</span></span> <span data-ttu-id="d7954-263">Tous les appareils joints à un domaine qui exécutent Mise à jour anniversaire Windows 10 et Windows Server 2016 s’inscrivent automatiquement auprès d’Azure AD lors du redémarrage des appareils ou de la connexion des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="d7954-263">All domain-joined devices running Windows 10 Anniversary Update and Windows Server 2016 automatically register with Azure AD at device restart or user sign-in.</span></span> <span data-ttu-id="d7954-264">Nouveaux périphériques s’inscrire auprès d’Azure AD quand les appareils hello redémarre après que l’opération de jointure de domaine hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="d7954-264">New devices register with Azure AD when hello device restarts after hello domain join operation is completed.</span></span>

<span data-ttu-id="d7954-265">Les appareils qui ont été précédemment appartenant à un espace de travail tooAzure AD (par exemple pour Windows Intune) transition trop »*joints à un domaine, enregistré avec AAD*« ; toutefois il prend un certain temps pour toocomplete de ce processus sur tous les périphériques en raison de toohello normal flux d’activité des utilisateurs et de domaine.</span><span class="sxs-lookup"><span data-stu-id="d7954-265">Devices that were previously workplace-joined tooAzure AD (for example for Intune) transition too“*Domain Joined, AAD Registered*”; however it takes some time for this process toocomplete across all devices due toohello normal flow of domain and user activity.</span></span>

### <a name="remarks"></a><span data-ttu-id="d7954-266">Remarques</span><span class="sxs-lookup"><span data-stu-id="d7954-266">Remarks</span></span>

- <span data-ttu-id="d7954-267">Vous pouvez utiliser un déploiement de hello de toocontrol d’objet stratégie de groupe de l’inscription automatique de Windows 10 et les ordinateurs joints à un domaine Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="d7954-267">You can use a Group Policy object toocontrol hello rollout of automatic registration of Windows 10 and Windows Server 2016 domain-joined computers.</span></span>

- <span data-ttu-id="d7954-268">Windows 10 novembre 2015 mise à jour automatiquement inscrit auprès d’Azure AD **uniquement** si l’objet de stratégie de groupe de déploiement hello est définie.</span><span class="sxs-lookup"><span data-stu-id="d7954-268">Windows 10 November 2015 Update automatically registers with Azure AD **only** if hello rollout Group Policy object is set.</span></span>

- <span data-ttu-id="d7954-269">toorollout hello l’inscription automatique des ordinateurs de bas niveau de Windows, vous pouvez déployer un [package Windows Installer](#windows-installer-packages-for-non-windows-10-computers) toocomputers que vous sélectionnez.</span><span class="sxs-lookup"><span data-stu-id="d7954-269">toorollout hello automatic registration of Windows down-level computers, you can deploy a [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) toocomputers that you select.</span></span>

- <span data-ttu-id="d7954-270">Si vous envoyez des appareils joints au domaine hello stratégie de groupe objet tooWindows 8.1, l’inscription est tentée ; Il est toutefois recommandé d’utiliser hello [package Windows Installer](#windows-installer-packages-for-non-windows-10-computers) tooregister tous vos appareils de bas niveau de Windows.</span><span class="sxs-lookup"><span data-stu-id="d7954-270">If you push hello Group Policy object tooWindows 8.1 domain-joined devices, registration will be attempted; however it is recommended that you use hello [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) tooregister all your Windows down-level devices.</span></span> 

### <a name="create-a-group-policy-object"></a><span data-ttu-id="d7954-271">Créer un objet de stratégie de groupe</span><span class="sxs-lookup"><span data-stu-id="d7954-271">Create a Group Policy object</span></span> 

<span data-ttu-id="d7954-272">lancement de hello toocontrol l’enregistrement automatique des ordinateurs en cours de Windows, vous devez déployer hello **inscrire des ordinateurs joints au domaine en tant qu’appareils** stratégie de groupe objet toohello périphériques tooregister.</span><span class="sxs-lookup"><span data-stu-id="d7954-272">toocontrol hello rollout of automatic registration of Windows current computers, you should deploy hello **Register domain-joined computers as devices** Group Policy object toohello devices you want tooregister.</span></span> <span data-ttu-id="d7954-273">Par exemple, vous pouvez déployer hello stratégie tooan unité ou le groupe de sécurité tooa.</span><span class="sxs-lookup"><span data-stu-id="d7954-273">For example, you can deploy hello policy tooan organizational unit or tooa security group.</span></span>

<span data-ttu-id="d7954-274">**stratégie tooset hello :**</span><span class="sxs-lookup"><span data-stu-id="d7954-274">**tooset hello policy:**</span></span>

1. <span data-ttu-id="d7954-275">Ouvrez **le Gestionnaire de serveur**, puis passez trop`Tools > Group Policy Management`.</span><span class="sxs-lookup"><span data-stu-id="d7954-275">Open **Server Manager**, and then go too`Tools > Group Policy Management`.</span></span>
2. <span data-ttu-id="d7954-276">Atteindre le nœud de domaine toohello correspondant toohello domaine dans lequel tooactivate-d’enregistrement automatique des ordinateurs en cours de Windows.</span><span class="sxs-lookup"><span data-stu-id="d7954-276">Go toohello domain node that corresponds toohello domain where you want tooactivate auto-registration of Windows current computers.</span></span>
3. <span data-ttu-id="d7954-277">Cliquez avec le bouton droit sur **Objets de stratégie de groupe**, puis sélectionnez **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="d7954-277">Right-click **Group Policy Objects**, and then select **New**.</span></span>
4. <span data-ttu-id="d7954-278">Entrez un nom pour votre objet de stratégie de groupe.</span><span class="sxs-lookup"><span data-stu-id="d7954-278">Type a name for your Group Policy object.</span></span> <span data-ttu-id="d7954-279">Par exemple, *l’inscription automatique tooAzure AD*.</span><span class="sxs-lookup"><span data-stu-id="d7954-279">For example, *Automatic Registration tooAzure AD*.</span></span> <span data-ttu-id="d7954-280">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="d7954-280">Select **OK**.</span></span>
5. <span data-ttu-id="d7954-281">Cliquez avec le bouton droit sur votre nouvel objet de stratégie de groupe, puis sélectionnez **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="d7954-281">Right-click your new Group Policy object, and then select **Edit**.</span></span>
6. <span data-ttu-id="d7954-282">Accédez trop**Configuration ordinateur** > **stratégies** > **modèles d’administration** > **Windows Composants** > **DRS**.</span><span class="sxs-lookup"><span data-stu-id="d7954-282">Go too**Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Device Registration**.</span></span> <span data-ttu-id="d7954-283">Cliquez avec le bouton droit sur **Enregistrer les ordinateurs appartenant à un domaine en tant qu’appareils**, puis sélectionnez **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="d7954-283">Right-click **Register domain-joined computers as devices**, and then select **Edit**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d7954-284">Ce modèle de stratégie de groupe a été renommé à partir de versions antérieures de la console de gestion des stratégies de groupe hello.</span><span class="sxs-lookup"><span data-stu-id="d7954-284">This Group Policy template has been renamed from earlier versions of hello Group Policy Management console.</span></span> <span data-ttu-id="d7954-285">Si vous utilisez une version antérieure de la console de hello, passez trop`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span><span class="sxs-lookup"><span data-stu-id="d7954-285">If you are using an earlier version of hello console, go too`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span></span> 

7. <span data-ttu-id="d7954-286">Sélectionnez **Activé**, puis **Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="d7954-286">Select **Enabled**, and then select **Apply**.</span></span>
8. <span data-ttu-id="d7954-287">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="d7954-287">Select **OK**.</span></span>
9. <span data-ttu-id="d7954-288">Hello lien emplacement de tooa d’objet de stratégie de groupe de votre choix.</span><span class="sxs-lookup"><span data-stu-id="d7954-288">Link hello Group Policy object tooa location of your choice.</span></span> <span data-ttu-id="d7954-289">Par exemple, vous pouvez le lier tooa unité d’organisation spécifique.</span><span class="sxs-lookup"><span data-stu-id="d7954-289">For example, you can link it tooa specific organizational unit.</span></span> <span data-ttu-id="d7954-290">Vous également pouvez lier le groupe de sécurité spécifique tooa des ordinateurs qui inscrivent automatiquement auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7954-290">You also could link it tooa specific security group of computers that automatically register with Azure AD.</span></span> <span data-ttu-id="d7954-291">tooset cette stratégie pour tous les ordinateurs joints au domaine Windows 10 et Windows Server 2016 dans votre organisation, le domaine toohello objet lien hello stratégie de groupe.</span><span class="sxs-lookup"><span data-stu-id="d7954-291">tooset this policy for all domain-joined Windows 10 and Windows Server 2016 computers in your organization, link hello Group Policy object toohello domain.</span></span>

### <a name="windows-installer-packages-for-non-windows-10-computers"></a><span data-ttu-id="d7954-292">Packages Windows Installer pour les ordinateurs autres que Windows 10</span><span class="sxs-lookup"><span data-stu-id="d7954-292">Windows Installer packages for non-Windows 10 computers</span></span>

<span data-ttu-id="d7954-293">ordinateurs de bas niveau Windows appartenant au domaine tooregister dans un environnement fédéré, vous pouvez télécharger et installer ces packages Windows Installer (.msi) à partir du centre de téléchargement à hello [Microsoft jonction d’espace pour les ordinateurs non Windows 10](https://www.microsoft.com/en-us/download/details.aspx?id=53554) page.</span><span class="sxs-lookup"><span data-stu-id="d7954-293">tooregister domain-joined Windows down-level computers in a federated environment, you can download and install these Windows Installer package (.msi) from Download Center at hello [Microsoft Workplace Join for non-Windows 10 computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) page.</span></span>

<span data-ttu-id="d7954-294">Vous pouvez déployer le package de hello à l’aide d’un système de distribution de logiciels tels que System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="d7954-294">You can deploy hello package by using a software distribution system like System Center Configuration Manager.</span></span> <span data-ttu-id="d7954-295">Hello package prend en charge les options d’installation silencieuse standard hello avec hello *silencieux* paramètre.</span><span class="sxs-lookup"><span data-stu-id="d7954-295">hello package supports hello standard silent install options with hello *quiet* parameter.</span></span> <span data-ttu-id="d7954-296">Branche actuelle de System Center Configuration Manager offre des avantages supplémentaires à partir de versions antérieures, telles que les enregistrements de hello capacité tootrack s’est terminée.</span><span class="sxs-lookup"><span data-stu-id="d7954-296">System Center Configuration Manager Current Branch offers additional benefits from earlier versions, like hello ability tootrack completed registrations.</span></span> <span data-ttu-id="d7954-297">Pour plus d’informations, consultez l’article [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="d7954-297">For more information, see [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span></span>

<span data-ttu-id="d7954-298">programme d’installation Hello crée une tâche planifiée sur le système hello qui s’exécute dans le contexte de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="d7954-298">hello installer creates a scheduled task on hello system that runs in hello user’s context.</span></span> <span data-ttu-id="d7954-299">tâche Hello est déclenchée lorsque l’utilisateur de hello se connecte tooWindows.</span><span class="sxs-lookup"><span data-stu-id="d7954-299">hello task is triggered when hello user signs in tooWindows.</span></span> <span data-ttu-id="d7954-300">tâche Hello inscrit en mode silencieux les appareils hello avec Azure AD avec des informations d’identification utilisateur de hello après avoir authentifié à l’aide de l’authentification Windows intégrée.</span><span class="sxs-lookup"><span data-stu-id="d7954-300">hello task silently registers hello device with Azure AD with hello user credentials after authenticating using Integrated Windows Authentication.</span></span> <span data-ttu-id="d7954-301">toosee la tâche planifiée de hello, dans l’unité de hello, accédez trop**Microsoft** > **jonction**, puis passez la bibliothèque du Planificateur de tâches toohello.</span><span class="sxs-lookup"><span data-stu-id="d7954-301">toosee hello scheduled task, in hello device, go too**Microsoft** > **Workplace Join**, and then go toohello Task Scheduler library.</span></span>

## <a name="step-5-verify-registered-devices"></a><span data-ttu-id="d7954-302">Étape 5 : Vérification des appareils inscrits</span><span class="sxs-lookup"><span data-stu-id="d7954-302">Step 5: Verify registered devices</span></span>

<span data-ttu-id="d7954-303">Vous pouvez vérifier la réussite appareils inscrits dans votre organisation à l’aide de hello [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) applet de commande Bonjour [module Azure Active Directory PowerShell](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="d7954-303">You can check successful registered devices in your organization by using hello [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in hello [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span>

<span data-ttu-id="d7954-304">sortie Hello de cette applet de commande affiche les appareils inscrits dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7954-304">hello output of this cmdlet shows devices registered in Azure AD.</span></span> <span data-ttu-id="d7954-305">tooget tous les appareils, utilisez hello **-tous les** paramètre, puis filtre les à l’aide de hello **deviceTrustType** propriété.</span><span class="sxs-lookup"><span data-stu-id="d7954-305">tooget all devices, use hello **-All** parameter, and then filter them using hello **deviceTrustType** property.</span></span> <span data-ttu-id="d7954-306">Les appareils joints à un domaine présentent la valeur **Joint au domaine**.</span><span class="sxs-lookup"><span data-stu-id="d7954-306">Domain joined devices have a value of **Domain Joined**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7954-307">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d7954-307">Next steps</span></span>

* [<span data-ttu-id="d7954-308">FAQ sur l’inscription d’appareils automatique</span><span class="sxs-lookup"><span data-stu-id="d7954-308">Automatic device registration FAQ</span></span>](active-directory-device-registration-faq.md)
* [<span data-ttu-id="d7954-309">Résolution des problèmes d’enregistrement automatique du domaine joint ordinateurs tooAzure AD – Windows 10 et Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="d7954-309">Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)
* [<span data-ttu-id="d7954-310">Résolution des problèmes d’enregistrement automatique du domaine joint ordinateurs tooAzure AD-non Windows 10</span><span class="sxs-lookup"><span data-stu-id="d7954-310">Troubleshooting auto-registration of domain joined computers tooAzure AD – non-Windows 10</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
* [<span data-ttu-id="d7954-311">Accès conditionnel Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d7954-311">Azure Active Directory conditional access</span></span>](active-directory-conditional-access-azure-portal.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
