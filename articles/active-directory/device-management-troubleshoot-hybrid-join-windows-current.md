---
title: aaaTroubleshooting hybride Azure Active Directory joint des appareils Windows 10 et Windows Server 2016 | Documents Microsoft
description: "Résolution des problèmes des appareils hybrides Windows 10 et Windows Server 2016 joints à Azure Active Directory."
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
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: cc252d1d0684d6632694afc8a367327794228c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-windows-10-and-windows-server-2016-devices"></a><span data-ttu-id="255c2-103">Résolution des problèmes des appareils hybrides Windows 10 et Windows Server 2016 joints à Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="255c2-103">Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices</span></span> 

<span data-ttu-id="255c2-104">Cette rubrique est applicable toohello suivant des clients :</span><span class="sxs-lookup"><span data-stu-id="255c2-104">This topic is applicable toohello following clients:</span></span>

-   <span data-ttu-id="255c2-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="255c2-105">Windows 10</span></span>
-   <span data-ttu-id="255c2-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="255c2-106">Windows Server 2016</span></span>

<span data-ttu-id="255c2-107">Pour les autres clients Windows, consultez [Résoudre des problèmes des appareils hybrides de bas niveau joints à Azure Active Directory](device-management-troubleshoot-hybrid-join-windows-legacy.md).</span><span class="sxs-lookup"><span data-stu-id="255c2-107">For other Windows clients, see [Troubleshooting hybrid Azure Active Directory joined down-level devices](device-management-troubleshoot-hybrid-join-windows-legacy.md).</span></span>

<span data-ttu-id="255c2-108">Cette rubrique suppose que vous avez [configuré hybride Azure Active Directory des appareils joints à un](device-management-hybrid-azuread-joined-devices-setup.md) hello toosupport les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="255c2-108">This topic assumes that you have [configured hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md) toosupport hello following scenarios:</span></span>

- <span data-ttu-id="255c2-109">Accès conditionnel basé sur les appareils</span><span class="sxs-lookup"><span data-stu-id="255c2-109">Device-based conditional access</span></span>

- [<span data-ttu-id="255c2-110">Itinérance d’entreprise des paramètres</span><span class="sxs-lookup"><span data-stu-id="255c2-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="255c2-111">Windows Hello Entreprise</span><span class="sxs-lookup"><span data-stu-id="255c2-111">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md)


<span data-ttu-id="255c2-112">Ce document fournit des conseils de dépannage sur la façon dont des problèmes potentiels de tooresolve.</span><span class="sxs-lookup"><span data-stu-id="255c2-112">This document provides troubleshooting guidance on how tooresolve potential issues.</span></span> 


<span data-ttu-id="255c2-113">Pour Windows 10 et Windows Server 2016, hybrides Azure Active Directory join prend en charge hello Windows 10 novembre 2015 mise à jour et les versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="255c2-113">For Windows 10 and Windows Server 2016, hybrid Azure Active Directory join supports hello Windows 10 November 2015 Update and above.</span></span> <span data-ttu-id="255c2-114">Nous recommandons à l’aide de la mise à jour anniversaire de hello.</span><span class="sxs-lookup"><span data-stu-id="255c2-114">We recommend using hello Anniversary update.</span></span>

## <a name="step-1-retrieve-hello-join-status"></a><span data-ttu-id="255c2-115">Étape 1 : Récupération de l’état de jointure de hello</span><span class="sxs-lookup"><span data-stu-id="255c2-115">Step 1: Retrieve hello join status</span></span> 

<span data-ttu-id="255c2-116">**état de jointure tooretrieve hello :**</span><span class="sxs-lookup"><span data-stu-id="255c2-116">**tooretrieve hello join status:**</span></span>

1. <span data-ttu-id="255c2-117">Invite de commandes ouverte hello en tant qu’administrateur</span><span class="sxs-lookup"><span data-stu-id="255c2-117">Open hello command prompt as an administrator</span></span>

2. <span data-ttu-id="255c2-118">Entrez **dsregcmd /status**</span><span class="sxs-lookup"><span data-stu-id="255c2-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="255c2-119">+----------------------------------------------------------------------+
    | État de l’appareil                                                    | +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="255c2-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined: YES
     <span data-ttu-id="255c2-120">EnterpriseJoined : Aucun ID de périphérique : l’empreinte numérique 5820fbe9-60c8-43b0-bb11-44aee233e4e7 : B753A6679CE720451921302CA873794D94C6204A KeyContainerId : bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider : TpmProtected de fournisseur de chiffrement de plateforme Microsoft : Oui KeySignTest : : doit exécuter élevés tootest.</span><span class="sxs-lookup"><span data-stu-id="255c2-120">EnterpriseJoined: NO DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft Platform Crypto Provider TpmProtected: YES KeySignTest: : MUST Run elevated tootest.</span></span>
                  <span data-ttu-id="255c2-121">Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO</span><span class="sxs-lookup"><span data-stu-id="255c2-121">Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO</span></span>
    
    <span data-ttu-id="255c2-122">+----------------------------------------------------------------------+
    | État utilisateur                                                         | +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="255c2-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet: YES
               NgcKeyId: {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined: NO
          WamDefaultSet: YES
    <span data-ttu-id="255c2-123">WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: YES</span><span class="sxs-lookup"><span data-stu-id="255c2-123">WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: YES</span></span>



## <a name="step-2-evaluate-hello-join-status"></a><span data-ttu-id="255c2-124">Étape 2 : Évaluer l’état de jointure hello</span><span class="sxs-lookup"><span data-stu-id="255c2-124">Step 2: Evaluate hello join status</span></span> 

<span data-ttu-id="255c2-125">Passez en revue les hello suivant des champs et assurez-vous que les valeurs attendues hello :</span><span class="sxs-lookup"><span data-stu-id="255c2-125">Review hello following fields and make sure that they have hello expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="255c2-126">AzureAdJoined : YES</span><span class="sxs-lookup"><span data-stu-id="255c2-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="255c2-127">Ce champ indique si l’appareil de hello est joint à Azure AD.</span><span class="sxs-lookup"><span data-stu-id="255c2-127">This field indicates whether hello device is joined with Azure AD.</span></span> <span data-ttu-id="255c2-128">Si la valeur hello est **non**, hello tooAzure jointure AD n’est pas encore terminée.</span><span class="sxs-lookup"><span data-stu-id="255c2-128">If hello value is **NO**, hello join tooAzure AD has not completed yet.</span></span> 

<span data-ttu-id="255c2-129">**Causes possibles :**</span><span class="sxs-lookup"><span data-stu-id="255c2-129">**Possible causes:**</span></span>

- <span data-ttu-id="255c2-130">Échec de l’authentification d’ordinateur hello pour une jointure.</span><span class="sxs-lookup"><span data-stu-id="255c2-130">Authentication of hello computer for a join failed.</span></span>

- <span data-ttu-id="255c2-131">Il existe un proxy HTTP dans l’organisation hello qui ne peut pas être découverts par ordinateur de hello</span><span class="sxs-lookup"><span data-stu-id="255c2-131">There is an HTTP proxy in hello organization that cannot be discovered by hello computer</span></span>

- <span data-ttu-id="255c2-132">ordinateur de Hello ne peut pas atteindre tooauthenticate d’Azure AD ou Azure DRS pour l’inscription</span><span class="sxs-lookup"><span data-stu-id="255c2-132">hello computer cannot reach Azure AD tooauthenticate or Azure DRS for registration</span></span>

- <span data-ttu-id="255c2-133">Hello ordinateur peut-être pas sur le réseau interne de l’organisation hello ou VPN avec la ligne de vue directe tooan contrôleur de domaine Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="255c2-133">hello computer may not be on hello organization’s internal network or on VPN with direct line of sight tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="255c2-134">Si hello est équipé d’un module de plateforme sécurisée, il peut être dans un état incorrect.</span><span class="sxs-lookup"><span data-stu-id="255c2-134">If hello computer has a TPM, it can be in a bad state.</span></span>

- <span data-ttu-id="255c2-135">Il peut y avoir une configuration incorrecte dans les services de hello mentionné dans le document de hello que vous devez à nouveau tooverify.</span><span class="sxs-lookup"><span data-stu-id="255c2-135">There might be a misconfiguration in hello services noted in hello document earlier that you will need tooverify again.</span></span> <span data-ttu-id="255c2-136">Voici des exemples courants :</span><span class="sxs-lookup"><span data-stu-id="255c2-136">Common examples are:</span></span>

    - <span data-ttu-id="255c2-137">Votre serveur de fédération n’a pas de points de terminaison WS-Trust activés</span><span class="sxs-lookup"><span data-stu-id="255c2-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="255c2-138">Votre serveur de fédération n’autorise peut-être pas l’authentification entrante à partir d’ordinateurs de votre réseau à l’aide de l’authentification Windows intégrée.</span><span class="sxs-lookup"><span data-stu-id="255c2-138">Your federation server does not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="255c2-139">Il n’existe aucun objet de Point de connexion qui pointe le nom de domaine vérifié tooyour dans Azure AD dans la forêt hello AD où appartient hello ordinateur</span><span class="sxs-lookup"><span data-stu-id="255c2-139">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="255c2-140">DomainJoined : YES</span><span class="sxs-lookup"><span data-stu-id="255c2-140">DomainJoined : YES</span></span>  

<span data-ttu-id="255c2-141">Ce champ indique si l’appareil de hello est joint tooan locale Active Directory ou non.</span><span class="sxs-lookup"><span data-stu-id="255c2-141">This field indicates whether hello device is joined tooan on-premises Active Directory or not.</span></span> <span data-ttu-id="255c2-142">Si la valeur hello est **non**, appareil de hello ne peut pas effectuer une jointure hybrides Azure AD.</span><span class="sxs-lookup"><span data-stu-id="255c2-142">If hello value is **NO**, hello device cannot perform a hybrid Azure AD join.</span></span>  

---

### <a name="workplacejoined--no"></a><span data-ttu-id="255c2-143">WorkplaceJoined : NO</span><span class="sxs-lookup"><span data-stu-id="255c2-143">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="255c2-144">Ce champ indique si l’appareil de hello est inscrit auprès d’Azure AD en tant qu’un appareil personnel (marqué comme *espace de travail joint*).</span><span class="sxs-lookup"><span data-stu-id="255c2-144">This field indicates whether hello device is registered with Azure AD as a personal device (marked as *Workplace Joined*).</span></span> <span data-ttu-id="255c2-145">Cette valeur doit être **NON** pour un ordinateur appartenant à un domaine qui est également une jonction hybride Azure AD.</span><span class="sxs-lookup"><span data-stu-id="255c2-145">This value should be **NO** for a domain-joined computer that is also hybrid Azure AD joined.</span></span> <span data-ttu-id="255c2-146">Si la valeur hello est **Oui**, un compte professionnel ou scolaire a été ajouté achèvement toohello préalable de jointure de hello hybrides Azure AD.</span><span class="sxs-lookup"><span data-stu-id="255c2-146">If hello value is **YES**, a work or school account was added prior toohello completion of hello hybrid Azure AD join.</span></span> <span data-ttu-id="255c2-147">Dans ce cas, le compte de hello est ignoré lorsque vous utilisez la version de mise à jour anniversaire hello de Windows 10 (1607).</span><span class="sxs-lookup"><span data-stu-id="255c2-147">In this case, hello account is ignored when using hello Anniversary Update version of Windows 10 (1607).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="255c2-148">WamDefaultSet : YES et AzureADPrt : YES</span><span class="sxs-lookup"><span data-stu-id="255c2-148">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="255c2-149">Ces champs indiquent si les utilisateurs de hello a été authentifié tooAzure AD lors de la connexion toohello appareil.</span><span class="sxs-lookup"><span data-stu-id="255c2-149">These fields indicate whether hello user has successfully authenticated tooAzure AD when signing in toohello device.</span></span> <span data-ttu-id="255c2-150">Si les valeurs hello sont **non**, il peut être dû :</span><span class="sxs-lookup"><span data-stu-id="255c2-150">If hello values are **NO**, it could be due:</span></span>

- <span data-ttu-id="255c2-151">Clé de stockage incorrecte (STK) dans le TPM associé au périphérique hello lors de l’enregistrement (vérification hello KeySignTest lors de son exécution avec élévation de privilèges).</span><span class="sxs-lookup"><span data-stu-id="255c2-151">Bad storage key (STK) in TPM associated with hello device upon registration (check hello KeySignTest while running elevated).</span></span>

- <span data-ttu-id="255c2-152">ID de connexion de substitution</span><span class="sxs-lookup"><span data-stu-id="255c2-152">Alternate Login ID</span></span>

- <span data-ttu-id="255c2-153">Proxy HTTP introuvable</span><span class="sxs-lookup"><span data-stu-id="255c2-153">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="255c2-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="255c2-154">Next steps</span></span>

<span data-ttu-id="255c2-155">Pour toute question, consultez hello [Forum aux questions sur la gestion des appareils](device-management-faq.md)</span><span class="sxs-lookup"><span data-stu-id="255c2-155">For questions, see hello [device management FAQ](device-management-faq.md)</span></span> 
