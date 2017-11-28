---
title: "Résolution des problèmes de l’inscription automatique des ordinateurs joints au domaine Azure Active Directory pour Windows 10 et Windows Server 2016 | Microsoft Docs"
description: "Résolution des problèmes de l’inscription automatique des ordinateurs joints au domaine Azure Active Directory pour Windows 10 et Windows Server 2016."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 5b7f95f302f716d9221b5fae59aa2df5c956a524
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-to-azure-ad--windows-10-and-windows-server-2016"></a><span data-ttu-id="7f3ee-103">Résolution des problèmes de l’inscription automatique des ordinateurs joints au domaine à Azure AD – Windows 10 et Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="7f3ee-103">Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016</span></span>

<span data-ttu-id="7f3ee-104">Cette rubrique s’applique aux clients suivants :</span><span class="sxs-lookup"><span data-stu-id="7f3ee-104">This topic is applicable to the following clients:</span></span>

-   <span data-ttu-id="7f3ee-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="7f3ee-105">Windows 10</span></span>
-   <span data-ttu-id="7f3ee-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="7f3ee-106">Windows Server 2016</span></span>

<span data-ttu-id="7f3ee-107">Pour les autres clients Windows, consultez [Résolution des problèmes de l’inscription automatique des ordinateurs joints au domaine vers Azure AD pour les clients de bas niveau Windows](active-directory-device-registration-troubleshoot-windows-legacy.md).</span><span class="sxs-lookup"><span data-stu-id="7f3ee-107">For other Windows clients, see [Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients](active-directory-device-registration-troubleshoot-windows-legacy.md).</span></span>

<span data-ttu-id="7f3ee-108">Cette rubrique suppose que vous avez configuré l’inscription d’appareils automatique joints à un domaine comme décrit dans [Configuration de l’inscription automatique auprès d’Azure Active Directory d’appareils Windows joints à un domaine](active-directory-device-registration-get-started.md) pour prendre en charge les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="7f3ee-108">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md) to support the following scenarios:</span></span>

- [<span data-ttu-id="7f3ee-109">Accès conditionnel basé sur les appareils</span><span class="sxs-lookup"><span data-stu-id="7f3ee-109">Device-based conditional access</span></span>](active-directory-conditional-access-automatic-device-registration-setup.md)

- [<span data-ttu-id="7f3ee-110">Itinérance d’entreprise des paramètres</span><span class="sxs-lookup"><span data-stu-id="7f3ee-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="7f3ee-111">Windows Hello Entreprise</span><span class="sxs-lookup"><span data-stu-id="7f3ee-111">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md)


<span data-ttu-id="7f3ee-112">Ce document fournit des conseils sur la façon de résoudre les problèmes potentiels.</span><span class="sxs-lookup"><span data-stu-id="7f3ee-112">This document provides troubleshooting guidance on how to resolve potential issues.</span></span> 

<span data-ttu-id="7f3ee-113">L’inscription est prise en charge dans la Mise à jour Windows 10 de novembre 2015 et les versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="7f3ee-113">The registration is supported in the Windows 10 November 2015 Update and above.</span></span>  
<span data-ttu-id="7f3ee-114">Nous vous recommandons d’utiliser la mise à jour anniversaire pour activer les scénarios ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="7f3ee-114">We recommend using the Anniversary Update for enabling the scenarios above.</span></span>

## <a name="step-1-retrieve-the-registration-status"></a><span data-ttu-id="7f3ee-115">Étape 1 : Récupérer l’état de l’inscription</span><span class="sxs-lookup"><span data-stu-id="7f3ee-115">Step 1: Retrieve the registration status</span></span> 

<span data-ttu-id="7f3ee-116">**Pour récupérer l’état de l’inscription :**</span><span class="sxs-lookup"><span data-stu-id="7f3ee-116">**To retrieve the registration status:**</span></span>

1. <span data-ttu-id="7f3ee-117">Ouvrez une invite de commandes en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="7f3ee-117">Open the command prompt as an administrator.</span></span>

2. <span data-ttu-id="7f3ee-118">Entrez **dsregcmd /status**</span><span class="sxs-lookup"><span data-stu-id="7f3ee-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="7f3ee-119">+----------------------------------------------------------------------+
    | État de l’appareil                                                    | +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="7f3ee-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined : YES
     <span data-ttu-id="7f3ee-120">EnterpriseJoined : NO DeviceId : 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint : B753A6679CE720451921302CA873794D94C6204A KeyContainerId : bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider : Microsoft Platform Crypto Provider TpmProtected : YES KeySignTest: : MUST Run elevated to test.</span><span class="sxs-lookup"><span data-stu-id="7f3ee-120">EnterpriseJoined : NO DeviceId : 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint : B753A6679CE720451921302CA873794D94C6204A KeyContainerId : bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider : Microsoft Platform Crypto Provider TpmProtected : YES KeySignTest: : MUST Run elevated to test.</span></span>
                  <span data-ttu-id="7f3ee-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span><span class="sxs-lookup"><span data-stu-id="7f3ee-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span></span>
    
    <span data-ttu-id="7f3ee-122">+----------------------------------------------------------------------+
    | État utilisateur                                                         | +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="7f3ee-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet : YES
               NgcKeyId : {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined : NO
          WamDefaultSet : YES
    <span data-ttu-id="7f3ee-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span><span class="sxs-lookup"><span data-stu-id="7f3ee-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span></span>



## <a name="step-2-evaluate-the-registration-status"></a><span data-ttu-id="7f3ee-124">Étape 2 : Évaluer l’état de l’inscription</span><span class="sxs-lookup"><span data-stu-id="7f3ee-124">Step 2: Evaluate the registration status</span></span> 

<span data-ttu-id="7f3ee-125">Examinez les champs suivants et assurez-vous qu’ils disposent des valeurs attendues :</span><span class="sxs-lookup"><span data-stu-id="7f3ee-125">Review the following fields and make sure that they have the expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="7f3ee-126">AzureAdJoined : YES</span><span class="sxs-lookup"><span data-stu-id="7f3ee-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="7f3ee-127">Ce champ indique si l’appareil est inscrit auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f3ee-127">This field shows whether the device is registered with Azure AD.</span></span> <span data-ttu-id="7f3ee-128">Si la valeur affichée est « NO », l’inscription n’est pas terminée.</span><span class="sxs-lookup"><span data-stu-id="7f3ee-128">If the value shows as ‘NO’, registration has not completed.</span></span> 

<span data-ttu-id="7f3ee-129">**Causes possibles :**</span><span class="sxs-lookup"><span data-stu-id="7f3ee-129">**Possible causes:**</span></span>

- <span data-ttu-id="7f3ee-130">Échec de l’authentification de l’ordinateur pour l’inscription.</span><span class="sxs-lookup"><span data-stu-id="7f3ee-130">Authentication of the computer for registration failed.</span></span>

- <span data-ttu-id="7f3ee-131">Il existe un proxy HTTP dans l’organisation qui ne peut pas être détecté par l’ordinateur</span><span class="sxs-lookup"><span data-stu-id="7f3ee-131">There is an HTTP proxy in the organization that cannot be discovered by the computer</span></span>

- <span data-ttu-id="7f3ee-132">L’ordinateur ne peut pas atteindre Azure AD pour l’authentification ou Azure DRS pour l’inscription</span><span class="sxs-lookup"><span data-stu-id="7f3ee-132">The computer cannot reach Azure AD for authentication or Azure DRS for registration</span></span>

- <span data-ttu-id="7f3ee-133">L’ordinateur n’est peut-être pas sur le réseau interne de l’entreprise ou un réseau privé virtuel avec une vue directe sur un contrôleur de domaine AD local.</span><span class="sxs-lookup"><span data-stu-id="7f3ee-133">The computer may not be on the organization’s internal network or on VPN with direct line of sight to an on-premises AD domain controller.</span></span>

- <span data-ttu-id="7f3ee-134">Si l’ordinateur dispose d’un module de plateforme sécurisée, celui-ci est peut être en mauvais état.</span><span class="sxs-lookup"><span data-stu-id="7f3ee-134">If the computer has a TPM, it may be in a bad state.</span></span>

- <span data-ttu-id="7f3ee-135">Il peut y avoir un problème de configuration des services mentionnés plus haut dans ce document que vous devez vérifier à nouveau.</span><span class="sxs-lookup"><span data-stu-id="7f3ee-135">There may be a misconfiguration in services noted in the document earlier that you will need to verify again.</span></span> <span data-ttu-id="7f3ee-136">Voici des exemples courants :</span><span class="sxs-lookup"><span data-stu-id="7f3ee-136">Common examples are:</span></span>

    - <span data-ttu-id="7f3ee-137">Votre serveur de fédération n’a pas de points de terminaison WS-Trust activés</span><span class="sxs-lookup"><span data-stu-id="7f3ee-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="7f3ee-138">Votre serveur de fédération n’autorise peut-être pas l’authentification entrante à partir d’ordinateurs de votre réseau à l’aide de l’authentification Windows intégrée.</span><span class="sxs-lookup"><span data-stu-id="7f3ee-138">Your federation server may not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="7f3ee-139">Il n’existe aucun objet de point de connexion de service qui pointe vers le nom de votre domaine vérifié dans Azure AD dans la forêt Active Directory à laquelle l’ordinateur appartient</span><span class="sxs-lookup"><span data-stu-id="7f3ee-139">There is no Service Connection Point object that points to your verified domain name in Azure AD in the AD forest where the computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="7f3ee-140">DomainJoined : YES</span><span class="sxs-lookup"><span data-stu-id="7f3ee-140">DomainJoined : YES</span></span>  

<span data-ttu-id="7f3ee-141">Ce champ indique si l’appareil est joint à un répertoire Active Directory local ou non.</span><span class="sxs-lookup"><span data-stu-id="7f3ee-141">This field shows whether the device is joined to an on-premises Active Directory or not.</span></span> <span data-ttu-id="7f3ee-142">Si la valeur affichée est **NO**, l’appareil ne peut pas s’enregistrer automatiquement auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f3ee-142">If the value shows as **NO**, the device cannot auto-register with Azure AD.</span></span> <span data-ttu-id="7f3ee-143">Vérifiez d’abord que l’appareil est joint au répertoire Active Directory local pour pouvoir s’enregistrer auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f3ee-143">Check first that the device joins to the on-premises Active Directory before it can register with Azure AD.</span></span> <span data-ttu-id="7f3ee-144">Si vous voulez joindre l’ordinateur à Azure AD directement, consultez « Learn about capabilities of Azure Active Directory Join » (En savoir plus sur les fonctionnalités d’Azure Active Directory Join).</span><span class="sxs-lookup"><span data-stu-id="7f3ee-144">If you are looking for joining the computer to Azure AD directly, please go to Learn about capabilities of Azure Active Directory Join.</span></span>

---

### <a name="workplacejoined--no"></a><span data-ttu-id="7f3ee-145">WorkplaceJoined : NO</span><span class="sxs-lookup"><span data-stu-id="7f3ee-145">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="7f3ee-146">Ce champ indique si l’appareil est inscrit auprès d’Azure AD mais en tant qu’appareil personnel (avec la mention « Joint à l’espace de travail »).</span><span class="sxs-lookup"><span data-stu-id="7f3ee-146">This field shows whether the device is registered with Azure AD but as a personal device (marked as ‘Workplace Joined’).</span></span> <span data-ttu-id="7f3ee-147">La valeur affichée doit être « NO » pour un ordinateur joint à un domaine inscrit auprès d’Azure AD, cependant si la valeur affichée est « YES », cela signifie qu’un compte professionnel ou scolaire a été ajouté avant que l’inscription de l’ordinateur ne soit terminée.</span><span class="sxs-lookup"><span data-stu-id="7f3ee-147">If this value should show as ‘NO’ for a domain joined computer registered with Azure AD, however if it shows as YES it means that a work or school account was added prior to the computer completing registration.</span></span> <span data-ttu-id="7f3ee-148">Dans ce cas, le compte sera ignoré si la version Mise à jour Anniversaire de Windows 10 est utilisée (1607 avec l’exécution de la commande WinVer dans la fenêtre « Exécuter » ou une fenêtre d’invite de commandes).</span><span class="sxs-lookup"><span data-stu-id="7f3ee-148">In this case the account will be ignored if using the Anniversary Update version of Windows 10 (1607 when running the WinVer command in the ‘Run’ window or a command prompt window).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="7f3ee-149">WamDefaultSet : YES et AzureADPrt : YES</span><span class="sxs-lookup"><span data-stu-id="7f3ee-149">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="7f3ee-150">Ces champs indiquent que l’utilisateur s’est correctement authentifié auprès d’Azure AD lors de la connexion à l’appareil.</span><span class="sxs-lookup"><span data-stu-id="7f3ee-150">These fields show that the user has successfully authenticated to Azure AD upon signing in to the device.</span></span> <span data-ttu-id="7f3ee-151">Si la valeur affichée est « NO », voici quelques causes possibles :</span><span class="sxs-lookup"><span data-stu-id="7f3ee-151">If they show ‘NO’ the following are possible causes:</span></span>

- <span data-ttu-id="7f3ee-152">Clé de stockage défectueuse (STK) dans le module de plateforme sécurisée associé à l’appareil lors de l’inscription (vérifiez KeySignTest en cours d’exécution avec élévation de privilèges).</span><span class="sxs-lookup"><span data-stu-id="7f3ee-152">Bad storage key (STK) in TPM associated with the device upon registration (check the KeySignTest while running elevated).</span></span>

- <span data-ttu-id="7f3ee-153">ID de connexion de substitution</span><span class="sxs-lookup"><span data-stu-id="7f3ee-153">Alternate Login ID</span></span>

- <span data-ttu-id="7f3ee-154">Proxy HTTP introuvable</span><span class="sxs-lookup"><span data-stu-id="7f3ee-154">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f3ee-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7f3ee-155">Next steps</span></span>

<span data-ttu-id="7f3ee-156">Pour plus d’informations, consultez le [FAQ sur l’inscription d’appareils automatique](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="7f3ee-156">For more information, see the [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 