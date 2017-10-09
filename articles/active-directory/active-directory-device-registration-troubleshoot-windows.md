---
title: ordinateurs joints au aaaTroubleshooting hello-inscription automatique de domaine Azure AD pour Windows 10 et Windows Server 2016 | Documents Microsoft
description: "Résolution des problèmes d’inscription automatique hello de domaine Azure AD les ordinateurs joints pour Windows 10 et Windows Server 2016."
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
ms.openlocfilehash: 3795323ce9392368b412b3e1208868431e59a74b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad--windows-10-and-windows-server-2016"></a><span data-ttu-id="2bcf3-103">Résolution des problèmes d’enregistrement automatique du domaine joint ordinateurs tooAzure AD – Windows 10 et Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="2bcf3-103">Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016</span></span>

<span data-ttu-id="2bcf3-104">Cette rubrique est applicable toohello suivant des clients :</span><span class="sxs-lookup"><span data-stu-id="2bcf3-104">This topic is applicable toohello following clients:</span></span>

-   <span data-ttu-id="2bcf3-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="2bcf3-105">Windows 10</span></span>
-   <span data-ttu-id="2bcf3-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="2bcf3-106">Windows Server 2016</span></span>

<span data-ttu-id="2bcf3-107">Pour d’autres clients de Windows, consultez [résolution des problèmes d’enregistrement automatique du domaine joint tooAzure d’ordinateurs Active Directory pour les clients de bas niveau Windows](active-directory-device-registration-troubleshoot-windows-legacy.md).</span><span class="sxs-lookup"><span data-stu-id="2bcf3-107">For other Windows clients, see [Troubleshooting auto-registration of domain joined computers tooAzure AD for Windows down-level clients](active-directory-device-registration-troubleshoot-windows-legacy.md).</span></span>

<span data-ttu-id="2bcf3-108">Cette rubrique suppose que vous avez configuré l’inscription automatique des appareils joints au domaine comme expliqué dans décrites dans [comment tooconfigure l’inscription automatique de Windows appartenant au domaine des appareils avec Azure Active Directory](active-directory-device-registration-get-started.md) hello toosupport les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="2bcf3-108">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md) toosupport hello following scenarios:</span></span>

- [<span data-ttu-id="2bcf3-109">Accès conditionnel basé sur les appareils</span><span class="sxs-lookup"><span data-stu-id="2bcf3-109">Device-based conditional access</span></span>](active-directory-conditional-access-automatic-device-registration-setup.md)

- [<span data-ttu-id="2bcf3-110">Itinérance d’entreprise des paramètres</span><span class="sxs-lookup"><span data-stu-id="2bcf3-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="2bcf3-111">Windows Hello Entreprise</span><span class="sxs-lookup"><span data-stu-id="2bcf3-111">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md)


<span data-ttu-id="2bcf3-112">Ce document fournit des conseils de dépannage sur la façon dont des problèmes potentiels de tooresolve.</span><span class="sxs-lookup"><span data-stu-id="2bcf3-112">This document provides troubleshooting guidance on how tooresolve potential issues.</span></span> 

<span data-ttu-id="2bcf3-113">Hello l’inscription est pris en charge dans les Windows hello mise à jour 10 novembre 2015 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="2bcf3-113">hello registration is supported in hello Windows 10 November 2015 Update and above.</span></span>  
<span data-ttu-id="2bcf3-114">Nous vous recommandons d’utiliser hello mise à jour anniversaire pour activer les scénarios de hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="2bcf3-114">We recommend using hello Anniversary Update for enabling hello scenarios above.</span></span>

## <a name="step-1-retrieve-hello-registration-status"></a><span data-ttu-id="2bcf3-115">Étape 1 : Récupération de l’état de l’inscription de hello</span><span class="sxs-lookup"><span data-stu-id="2bcf3-115">Step 1: Retrieve hello registration status</span></span> 

<span data-ttu-id="2bcf3-116">**état de l’inscription de hello tooretrieve :**</span><span class="sxs-lookup"><span data-stu-id="2bcf3-116">**tooretrieve hello registration status:**</span></span>

1. <span data-ttu-id="2bcf3-117">Ouvrez l’invite de commandes hello en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="2bcf3-117">Open hello command prompt as an administrator.</span></span>

2. <span data-ttu-id="2bcf3-118">Entrez **dsregcmd /status**</span><span class="sxs-lookup"><span data-stu-id="2bcf3-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="2bcf3-119">+----------------------------------------------------------------------+
    | État de l’appareil                                                    | +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="2bcf3-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined : YES
     <span data-ttu-id="2bcf3-120">EnterpriseJoined : Aucun ID de périphérique : l’empreinte numérique 5820fbe9-60c8-43b0-bb11-44aee233e4e7 : B753A6679CE720451921302CA873794D94C6204A KeyContainerId : bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider : TpmProtected de fournisseur de chiffrement de plateforme Microsoft : Oui KeySignTest : : doit exécuter élevés tootest.</span><span class="sxs-lookup"><span data-stu-id="2bcf3-120">EnterpriseJoined : NO DeviceId : 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint : B753A6679CE720451921302CA873794D94C6204A KeyContainerId : bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider : Microsoft Platform Crypto Provider TpmProtected : YES KeySignTest: : MUST Run elevated tootest.</span></span>
                  <span data-ttu-id="2bcf3-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span><span class="sxs-lookup"><span data-stu-id="2bcf3-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span></span>
    
    <span data-ttu-id="2bcf3-122">+----------------------------------------------------------------------+
    | État utilisateur                                                         | +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="2bcf3-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet : YES
               NgcKeyId : {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined : NO
          WamDefaultSet : YES
    <span data-ttu-id="2bcf3-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span><span class="sxs-lookup"><span data-stu-id="2bcf3-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span></span>



## <a name="step-2-evaluate-hello-registration-status"></a><span data-ttu-id="2bcf3-124">Étape 2 : Évaluer l’état de l’inscription de hello</span><span class="sxs-lookup"><span data-stu-id="2bcf3-124">Step 2: Evaluate hello registration status</span></span> 

<span data-ttu-id="2bcf3-125">Passez en revue les hello suivant des champs et assurez-vous que les valeurs attendues hello :</span><span class="sxs-lookup"><span data-stu-id="2bcf3-125">Review hello following fields and make sure that they have hello expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="2bcf3-126">AzureAdJoined : YES</span><span class="sxs-lookup"><span data-stu-id="2bcf3-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="2bcf3-127">Ce champ indique si l’appareil de hello est inscrit auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2bcf3-127">This field shows whether hello device is registered with Azure AD.</span></span> <span data-ttu-id="2bcf3-128">Si la valeur de hello est affichée comme « Non », l’enregistrement n’est pas terminée.</span><span class="sxs-lookup"><span data-stu-id="2bcf3-128">If hello value shows as ‘NO’, registration has not completed.</span></span> 

<span data-ttu-id="2bcf3-129">**Causes possibles :**</span><span class="sxs-lookup"><span data-stu-id="2bcf3-129">**Possible causes:**</span></span>

- <span data-ttu-id="2bcf3-130">Échec de l’authentification d’ordinateur hello pour l’inscription.</span><span class="sxs-lookup"><span data-stu-id="2bcf3-130">Authentication of hello computer for registration failed.</span></span>

- <span data-ttu-id="2bcf3-131">Il existe un proxy HTTP dans l’organisation hello qui ne peut pas être découverts par ordinateur de hello</span><span class="sxs-lookup"><span data-stu-id="2bcf3-131">There is an HTTP proxy in hello organization that cannot be discovered by hello computer</span></span>

- <span data-ttu-id="2bcf3-132">ordinateur de Hello ne peut pas accéder à Azure AD pour l’authentification ou le service DRS Azure pour l’inscription</span><span class="sxs-lookup"><span data-stu-id="2bcf3-132">hello computer cannot reach Azure AD for authentication or Azure DRS for registration</span></span>

- <span data-ttu-id="2bcf3-133">Hello ordinateur peut-être pas sur le réseau interne de l’organisation hello ou VPN avec la ligne de vue directe tooan contrôleur de domaine Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="2bcf3-133">hello computer may not be on hello organization’s internal network or on VPN with direct line of sight tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="2bcf3-134">Si hello est équipé d’un module de plateforme sécurisée, il peut être dans un état incorrect.</span><span class="sxs-lookup"><span data-stu-id="2bcf3-134">If hello computer has a TPM, it may be in a bad state.</span></span>

- <span data-ttu-id="2bcf3-135">Il peut y avoir une configuration incorrecte dans les services mentionné dans le document de hello que vous devez à nouveau tooverify.</span><span class="sxs-lookup"><span data-stu-id="2bcf3-135">There may be a misconfiguration in services noted in hello document earlier that you will need tooverify again.</span></span> <span data-ttu-id="2bcf3-136">Voici des exemples courants :</span><span class="sxs-lookup"><span data-stu-id="2bcf3-136">Common examples are:</span></span>

    - <span data-ttu-id="2bcf3-137">Votre serveur de fédération n’a pas de points de terminaison WS-Trust activés</span><span class="sxs-lookup"><span data-stu-id="2bcf3-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="2bcf3-138">Votre serveur de fédération n’autorise peut-être pas l’authentification entrante à partir d’ordinateurs de votre réseau à l’aide de l’authentification Windows intégrée.</span><span class="sxs-lookup"><span data-stu-id="2bcf3-138">Your federation server may not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="2bcf3-139">Il n’existe aucun objet de Point de connexion qui pointe le nom de domaine vérifié tooyour dans Azure AD dans la forêt hello AD où appartient hello ordinateur</span><span class="sxs-lookup"><span data-stu-id="2bcf3-139">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="2bcf3-140">DomainJoined : YES</span><span class="sxs-lookup"><span data-stu-id="2bcf3-140">DomainJoined : YES</span></span>  

<span data-ttu-id="2bcf3-141">Ce champ indique si hello est tooan jointes locale Active Directory ou pas.</span><span class="sxs-lookup"><span data-stu-id="2bcf3-141">This field shows whether hello device is joined tooan on-premises Active Directory or not.</span></span> <span data-ttu-id="2bcf3-142">Si la valeur de hello est affichée en tant que **non**, appareil de hello ne peut pas l’enregistrement automatique avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2bcf3-142">If hello value shows as **NO**, hello device cannot auto-register with Azure AD.</span></span> <span data-ttu-id="2bcf3-143">Vérifiez d’abord que toohello de jointures hello appareil local Active Directory avant il peut s’inscrire auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2bcf3-143">Check first that hello device joins toohello on-premises Active Directory before it can register with Azure AD.</span></span> <span data-ttu-id="2bcf3-144">Si vous cherchez à l’attachement hello ordinateur tooAzure AD directement, accédez tooLearn sur les fonctionnalités d’Azure Active Directory Join.</span><span class="sxs-lookup"><span data-stu-id="2bcf3-144">If you are looking for joining hello computer tooAzure AD directly, please go tooLearn about capabilities of Azure Active Directory Join.</span></span>

---

### <a name="workplacejoined--no"></a><span data-ttu-id="2bcf3-145">WorkplaceJoined : NO</span><span class="sxs-lookup"><span data-stu-id="2bcf3-145">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="2bcf3-146">Ce champ indique si l’appareil de hello est inscrit auprès d’Azure AD, mais comme un appareil personnel (marqué comme « Espace de travail joint »).</span><span class="sxs-lookup"><span data-stu-id="2bcf3-146">This field shows whether hello device is registered with Azure AD but as a personal device (marked as ‘Workplace Joined’).</span></span> <span data-ttu-id="2bcf3-147">Si cette valeur doit être 'Non' pour un ordinateur joint à un domaine enregistré auprès d’Azure AD, toutefois s’il apparaît en tant qu’Oui, cela signifie qu’un compte professionnel ou scolaire était enregistrement de fin ordinateur ajouté toohello préalable.</span><span class="sxs-lookup"><span data-stu-id="2bcf3-147">If this value should show as ‘NO’ for a domain joined computer registered with Azure AD, however if it shows as YES it means that a work or school account was added prior toohello computer completing registration.</span></span> <span data-ttu-id="2bcf3-148">Dans ce cas les compte hello seront ignorée si vous utilisez la version de mise à jour anniversaire hello de Windows 10 (1607 lorsque exécutant la commande WinVer de hello hello fenêtre « Exécuter » ou une fenêtre d’invite de commandes).</span><span class="sxs-lookup"><span data-stu-id="2bcf3-148">In this case hello account will be ignored if using hello Anniversary Update version of Windows 10 (1607 when running hello WinVer command in hello ‘Run’ window or a command prompt window).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="2bcf3-149">WamDefaultSet : YES et AzureADPrt : YES</span><span class="sxs-lookup"><span data-stu-id="2bcf3-149">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="2bcf3-150">Ces champs indiquent que l’utilisateur hello a été authentifié tooAzure AD lors de l’ouverture de session toohello appareil.</span><span class="sxs-lookup"><span data-stu-id="2bcf3-150">These fields show that hello user has successfully authenticated tooAzure AD upon signing in toohello device.</span></span> <span data-ttu-id="2bcf3-151">Si elles affichent 'NO' hello Voici les causes possibles :</span><span class="sxs-lookup"><span data-stu-id="2bcf3-151">If they show ‘NO’ hello following are possible causes:</span></span>

- <span data-ttu-id="2bcf3-152">Clé de stockage incorrecte (STK) dans le TPM associé au périphérique hello lors de l’enregistrement (vérification hello KeySignTest lors de son exécution avec élévation de privilèges).</span><span class="sxs-lookup"><span data-stu-id="2bcf3-152">Bad storage key (STK) in TPM associated with hello device upon registration (check hello KeySignTest while running elevated).</span></span>

- <span data-ttu-id="2bcf3-153">ID de connexion de substitution</span><span class="sxs-lookup"><span data-stu-id="2bcf3-153">Alternate Login ID</span></span>

- <span data-ttu-id="2bcf3-154">Proxy HTTP introuvable</span><span class="sxs-lookup"><span data-stu-id="2bcf3-154">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="2bcf3-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2bcf3-155">Next steps</span></span>

<span data-ttu-id="2bcf3-156">Pour plus d’informations, consultez hello [Forum aux questions sur l’inscription automatique](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="2bcf3-156">For more information, see hello [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 
