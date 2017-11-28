---
title: aaaFederating plusieurs Azure AD avec unique AD FS | Documents Microsoft
description: Dans ce document, vous allez apprendre comment toofederate plusieurs Azure AD avec un seul AD FS.
keywords: "fédérer, ADFS, AD FS, plusieurs locataires, AD FS unique, un seul ADFS, fédération multi-client, adfs à forêts multiples, aad connect, fédération, fédération multi-locataire"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: anandy; billmath
ms.openlocfilehash: 442192896b3b13f7bf9388396cd3769e194329d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
#<a name="federate-multiple-instances-of-azure-ad-with-single-instance-of-ad-fs"></a><span data-ttu-id="1f78b-104">Fédérer plusieurs instances d’Azure AD avec une seule instance d’AD FS</span><span class="sxs-lookup"><span data-stu-id="1f78b-104">Federate multiple instances of Azure AD with single instance of AD FS</span></span>

<span data-ttu-id="1f78b-105">Une même batterie AD FS à haute disponibilité peut fédérer plusieurs forêts si elles entretiennent une relation d’approbation bidirectionnelle.</span><span class="sxs-lookup"><span data-stu-id="1f78b-105">A single high available AD FS farm can federate multiple forests if they have 2-way trust between them.</span></span> <span data-ttu-id="1f78b-106">Ces forêts multiples peut ou peut ne pas correspondre toohello même Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1f78b-106">These multiple forests may or may not correspond toohello same Azure Active Directory.</span></span> <span data-ttu-id="1f78b-107">Cet article fournit des instructions sur la fédération tooconfigure entre un déploiement AD FS unique et plusieurs forêts qui toodifferent de synchronisation Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f78b-107">This article provides instructions on how tooconfigure federation between a single AD FS deployment and more than one forests that sync toodifferent Azure AD.</span></span>

![Fédération multi-locataire avec une seule instance d’AD FS](media/active-directory-aadconnectfed-single-adfs-multitenant-federation/concept.png)
 
> [!NOTE]
> <span data-ttu-id="1f78b-109">L’écriture différée sur les appareils et la jonction automatique d’appareils ne sont pas prises en charge dans ce scénario.</span><span class="sxs-lookup"><span data-stu-id="1f78b-109">Device writeback and automatic device join are not supported in this scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="1f78b-110">Azure AD Connect ne peut pas être fédération tooconfigure utilisés dans ce scénario Azure AD Connect peut configurer la fédération pour les domaines dans un Azure AD unique.</span><span class="sxs-lookup"><span data-stu-id="1f78b-110">Azure AD Connect cannot be used tooconfigure federation in this scenario as Azure AD Connect can configure federation for domains in a single Azure AD.</span></span>

##<a name="steps-for-federating-ad-fs-with-multiple-azure-ad"></a><span data-ttu-id="1f78b-111">Étapes de la fédération d’AD FS avec plusieurs instances d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f78b-111">Steps for federating AD FS with multiple Azure AD</span></span>

<span data-ttu-id="1f78b-112">Envisagez de qu'un domaine est contoso.com dans Azure Active Directory contoso.onmicrosoft.com est déjà fédéré avec hello AD FS local installé dans l’environnement de Active Directory local de contoso.com.</span><span class="sxs-lookup"><span data-stu-id="1f78b-112">Consider a domain contoso.com in Azure Active Directory contoso.onmicrosoft.com is already federated with hello AD FS on-premises installed in contoso.com on-premises Active Directory environment.</span></span> <span data-ttu-id="1f78b-113">Fabrikam.com est un domaine dans Azure Active Directory fabrikam.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="1f78b-113">Fabrikam.com is a domain in fabrikam.onmicrosoft.com Azure Active Directory.</span></span>

##<a name="step-1-establish-a-two-way-trust"></a><span data-ttu-id="1f78b-114">Étape 1 : Établir une relation d’approbation bidirectionnelle</span><span class="sxs-lookup"><span data-stu-id="1f78b-114">Step 1: Establish a two-way trust</span></span>
 
<span data-ttu-id="1f78b-115">Pour AD FS dans contoso.com toobe tooauthenticate en mesure d’utilisateurs du domaine fabrikam.com, une approbation bidirectionnelle est nécessaire entre contoso.com et fabrikam.com. Suivez les indications hello dans ce [article](https://technet.microsoft.com/library/cc816590.aspx) toocreate hello d’approbation bidirectionnelle.</span><span class="sxs-lookup"><span data-stu-id="1f78b-115">For AD FS in contoso.com toobe able tooauthenticate users in fabrikam.com, a two-way trust is needed between contoso.com and fabrikam.com. Follow hello guideline in this [article](https://technet.microsoft.com/library/cc816590.aspx) toocreate hello two-way trust.</span></span>
 
##<a name="step-2-modify-contosocom-federation-settings"></a><span data-ttu-id="1f78b-116">Étape 2 : Modifier les paramètres de fédération contoso.com</span><span class="sxs-lookup"><span data-stu-id="1f78b-116">Step 2: Modify contoso.com federation settings</span></span> 
 
<span data-ttu-id="1f78b-117">émetteur par défaut est Hello pour un seul domaine fédéré de tooAD FS est « http://ADFSServiceFQDN/adfs/services/trust », par exemple, « http://fs.contoso.com/adfs/services/trust ».</span><span class="sxs-lookup"><span data-stu-id="1f78b-117">hello default issuer set for a single domain federated tooAD FS is "http://ADFSServiceFQDN/adfs/services/trust", for example, “http://fs.contoso.com/adfs/services/trust”.</span></span> <span data-ttu-id="1f78b-118">Azure Active Directory nécessite un émetteur unique pour chaque domaine fédéré.</span><span class="sxs-lookup"><span data-stu-id="1f78b-118">Azure Active Directory requires unique issuer for each federated domain.</span></span> <span data-ttu-id="1f78b-119">Étant donné que hello même AD FS va toofederate deux domaines, valeur d’émetteur hello doit toobe modifié afin qu’il soit unique pour chaque domaine QU'AD FS se fédère avec Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1f78b-119">Since hello same AD FS is going toofederate two domains, hello issuer value needs toobe modified so that it is unique for each domain AD FS federates with Azure Active Directory.</span></span> 
 
<span data-ttu-id="1f78b-120">Sur le serveur de hello AD FS, ouvrez PowerShell Azure AD et effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="1f78b-120">On hello AD FS server, open Azure AD PowerShell and perform hello following steps:</span></span>
 
<span data-ttu-id="1f78b-121">Se connecter toohello Azure Active Directory qui contient les paramètres fédération hello domaine contoso.com mise à jour Connect-MsolService hello pour contoso.com Update-MsolFederatedDomain - DomainName contoso.com – SupportMultipleDomain</span><span class="sxs-lookup"><span data-stu-id="1f78b-121">Connect toohello Azure Active Directory that contains hello domain contoso.com Connect-MsolService Update hello federation settings for contoso.com Update-MsolFederatedDomain -DomainName contoso.com –SupportMultipleDomain</span></span>
 
<span data-ttu-id="1f78b-122">L’émetteur dans les paramètres de fédération de domaine hello sera modifié trop « http://contoso.com/adfs/services/trust » et une émission de revendication règle est ajoutée pour hello Azure AD de confiance tooissue hello correct issuerId valeur basée sur un suffixe UPN hello.</span><span class="sxs-lookup"><span data-stu-id="1f78b-122">Issuer in hello domain federation setting will be changed too"http://contoso.com/adfs/services/trust" and an issuance claim rule will be added for hello Azure AD Relying Party Trust tooissue hello correct issuerId value based on hello UPN suffix.</span></span>
 
##<a name="step-3-federate-fabrikamcom-with-ad-fs"></a><span data-ttu-id="1f78b-123">Étape 3 : Fédérer fabrikam.com avec AD FS</span><span class="sxs-lookup"><span data-stu-id="1f78b-123">Step 3: Federate fabrikam.com with AD FS</span></span>
 
<span data-ttu-id="1f78b-124">Dans Azure AD powershell session effectuer hello comme suit : se connecter tooAzure Active Directory contenant hello domaine fabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="1f78b-124">In Azure AD powershell session perform hello following steps: Connect tooAzure Active Directory that contains hello domain fabrikam.com</span></span>

    Connect-MsolService
<span data-ttu-id="1f78b-125">Convertir toofederated de domaine fabrikam.com gérés hello :</span><span class="sxs-lookup"><span data-stu-id="1f78b-125">Convert hello fabrikam.com managed domain toofederated:</span></span>

    Convert-MsolDomainToFederated -DomainName anandmsft.com -Verbose -SupportMultipleDomain
 
<span data-ttu-id="1f78b-126">Hello ci-dessus opération sera fédérer hello domaine fabrikam.com avec hello même AD FS.</span><span class="sxs-lookup"><span data-stu-id="1f78b-126">hello above operation will federate hello domain fabrikam.com with hello same AD FS.</span></span> <span data-ttu-id="1f78b-127">Vous pouvez vérifier les paramètres de domaine hello à l’aide de Get-MsolDomainFederationSettings pour les deux domaines.</span><span class="sxs-lookup"><span data-stu-id="1f78b-127">You can verify hello domain settings by using Get-MsolDomainFederationSettings for both domains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f78b-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1f78b-128">Next steps</span></span>
[<span data-ttu-id="1f78b-129">Connecter Active Directory à Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1f78b-129">Connect Active Directory with Azure Active Directory</span></span>](active-directory-aadconnect.md)
