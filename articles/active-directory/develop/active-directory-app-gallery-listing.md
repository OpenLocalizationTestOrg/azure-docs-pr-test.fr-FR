---
title: "aaaListing votre application dans la galerie d’applications Azure Active Directory hello"
description: "Comment toolist une application qui prend en charge l’authentification unique dans hello Galerie d’Azure Active Directory | Microsoft Azure"
services: active-directory
documentationcenter: dev-center-name
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 09ccd3b4645a180059b9a9d502e39f1b8933c988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="listing-your-application-in-hello-azure-active-directory-application-gallery"></a><span data-ttu-id="5e456-103">Affichage de votre application dans la galerie d’applications Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="5e456-103">Listing your application in hello Azure Active Directory application gallery</span></span>
<span data-ttu-id="5e456-104">une application qui prend en charge l’authentification unique sur avec Azure Active Directory Bonjour de toolist [Galerie d’Azure AD](https://azure.microsoft.com/marketplace/active-directory/all/), application hello doit tout d’abord une tooimplement Hello suivant des modes d’intégration :</span><span class="sxs-lookup"><span data-stu-id="5e456-104">toolist an application that supports single sign-on with Azure Active Directory in hello [Azure AD gallery](https://azure.microsoft.com/marketplace/active-directory/all/), hello application first needs tooimplement one of hello following integration modes:</span></span>

* <span data-ttu-id="5e456-105">**OpenID Connect** - intégration directe avec Azure AD en utilisant OpenID Connect pour l’authentification et hello consentement d’Azure AD API pour la configuration.</span><span class="sxs-lookup"><span data-stu-id="5e456-105">**OpenID Connect** - Direct integration with Azure AD using OpenID Connect for authentication and hello Azure AD consent API for configuration.</span></span> <span data-ttu-id="5e456-106">Si vous commencez une intégration et votre application ne prend pas en charge SAML, il s’agit de mode de recommandation hello.</span><span class="sxs-lookup"><span data-stu-id="5e456-106">If you are just starting an integration and your application does not support SAML, then this is hello recommend mode.</span></span>
* <span data-ttu-id="5e456-107">**SAML** : votre application a déjà des fournisseurs d’identité tiers hello capacité tooconfigure à l’aide du protocole SAML de hello.</span><span class="sxs-lookup"><span data-stu-id="5e456-107">**SAML** – Your application already has hello ability tooconfigure third-party identity providers using hello SAML protocol.</span></span>

<span data-ttu-id="5e456-108">Les exigences pour chaque mode sont indiquées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="5e456-108">Listing requirements for each mode are below.</span></span>

## <a name="openid-connect-integration"></a><span data-ttu-id="5e456-109">Intégration d'OpenID Connect</span><span class="sxs-lookup"><span data-stu-id="5e456-109">OpenID Connect Integration</span></span>
<span data-ttu-id="5e456-110">toointegrate votre application auprès d’Azure AD, hello suivant [les instructions de développeur](active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="5e456-110">toointegrate your application with Azure AD, following hello [developer instructions](active-directory-authentication-scenarios.md).</span></span> <span data-ttu-id="5e456-111">Répondez aux questions de hello ci-dessous, puis envoyer toowaadpartners@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="5e456-111">Then complete hello questions below and send toowaadpartners@microsoft.com.</span></span>

* <span data-ttu-id="5e456-112">Fournissez les informations d’identification pour un compte ou un client de test avec l’application qui peut être utilisée par hello intégration d’Azure AD équipe tootest hello.</span><span class="sxs-lookup"><span data-stu-id="5e456-112">Provide credentials for a test tenant or account with your application that can be used by hello Azure AD team tootest hello integration.</span></span>  
* <span data-ttu-id="5e456-113">Fournissent des instructions sur l’équipe de hello Azure AD peut se connecter et se connecter à une instance de l’application de tooyour Azure AD à l’aide de hello [infrastructure de consentement d’Azure AD](active-directory-integrating-applications.md#overview-of-the-consent-framework).</span><span class="sxs-lookup"><span data-stu-id="5e456-113">Provide instructions on how hello Azure AD team can sign in and connect an instance of Azure AD tooyour application using hello [Azure AD consent framework](active-directory-integrating-applications.md#overview-of-the-consent-framework).</span></span> 
* <span data-ttu-id="5e456-114">Fournir des instructions supplémentaires requises pour hello Azure AD de l’équipe tootest single sign-on avec votre application.</span><span class="sxs-lookup"><span data-stu-id="5e456-114">Provide any further instructions required for hello Azure AD team tootest single sign-on with your application.</span></span> 
* <span data-ttu-id="5e456-115">Spécifiez les informations de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="5e456-115">Provide hello info below:</span></span>

> <span data-ttu-id="5e456-116">Nom de l’entreprise :</span><span class="sxs-lookup"><span data-stu-id="5e456-116">Company Name:</span></span>
> 
> <span data-ttu-id="5e456-117">Site web de l’entreprise :</span><span class="sxs-lookup"><span data-stu-id="5e456-117">Company Website:</span></span>
> 
> <span data-ttu-id="5e456-118">Nom de l’application :</span><span class="sxs-lookup"><span data-stu-id="5e456-118">Application Name:</span></span>
> 
> <span data-ttu-id="5e456-119">Description de l’application (200 caractères maximum) :</span><span class="sxs-lookup"><span data-stu-id="5e456-119">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="5e456-120">Site web de l’application (pour informatif) :</span><span class="sxs-lookup"><span data-stu-id="5e456-120">Application Website (informational):</span></span>
> 
> <span data-ttu-id="5e456-121">Site web du support technique de l’application ou les informations de contact :</span><span class="sxs-lookup"><span data-stu-id="5e456-121">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="5e456-122">ID d’application de l’application hello, comme indiqué dans les détails de l’application hello à https://portal.azure.com :</span><span class="sxs-lookup"><span data-stu-id="5e456-122">Application  ID of hello application, as shown in hello application details at https://portal.azure.com:</span></span>
> 
> <span data-ttu-id="5e456-123">URL d’inscription de l’application où les clients vont toosign pour et et/ou d’achat application hello :</span><span class="sxs-lookup"><span data-stu-id="5e456-123">Application Sign-Up URL where customers go toosign up for and /or purchase hello application:</span></span>
> 
> <span data-ttu-id="5e456-124">Choisissez les catégories de toothree pour votre toobe application répertoriés sous (pour les catégories disponibles voir hello Azure Active Directory Marketplace) :</span><span class="sxs-lookup"><span data-stu-id="5e456-124">Choose up toothree categories for your application toobe listed under (for available categories see hello Azure Active Directory Marketplace):</span></span>
> 
> <span data-ttu-id="5e456-125">Attacher une petite icône d’application (fichier PNG, 45 px par 45 px, couleur d’arrière-plan unie) :</span><span class="sxs-lookup"><span data-stu-id="5e456-125">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="5e456-126">Attacher une grande icône d’application (fichier PNG, 215 px par 215 px, couleur d’arrière-plan unie) :</span><span class="sxs-lookup"><span data-stu-id="5e456-126">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="5e456-127">Attacher un grand logo d’application (fichier PNG, 150 px par 122 px, couleur d’arrière-plan unie) :</span><span class="sxs-lookup"><span data-stu-id="5e456-127">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

## <a name="saml-integration"></a><span data-ttu-id="5e456-128">Intégration de SAML</span><span class="sxs-lookup"><span data-stu-id="5e456-128">SAML Integration</span></span>
<span data-ttu-id="5e456-129">N’importe quelle application qui prend en charge SAML 2.0 peut être intégrée directement à un locataire Azure AD à l’aide de [ces tooadd instructions une application personnalisée](../active-directory-saas-custom-apps.md).</span><span class="sxs-lookup"><span data-stu-id="5e456-129">Any app that supports SAML 2.0 can be integrated directly with an Azure AD tenant using [these instructions tooadd a custom application](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="5e456-130">Une fois que vous avez testé que votre intégration d’application fonctionne avec Azure AD, envoyer hello informations suivantes trop<mailto:waadpartners@microsoft.com>.</span><span class="sxs-lookup"><span data-stu-id="5e456-130">Once you have tested that your application integration works with Azure AD, send hello following information too<mailto:waadpartners@microsoft.com>.</span></span>

* <span data-ttu-id="5e456-131">Fournissez les informations d’identification pour un compte ou un client de test avec l’application qui peut être utilisée par hello intégration d’Azure AD équipe tootest hello.</span><span class="sxs-lookup"><span data-stu-id="5e456-131">Provide credentials for a test tenant or account with your application that can be used by hello Azure AD team tootest hello integration.</span></span>  
* <span data-ttu-id="5e456-132">Fournir hello SAML URL de connexion, URL de l’émetteur (ID d’entité), et l’URL de réponse (service de consommateur d’assertion) valeurs pour votre application, comme indiqué [ici](../active-directory-saas-custom-apps.md).</span><span class="sxs-lookup"><span data-stu-id="5e456-132">Provide hello SAML Sign-On URL, Issuer URL (entity ID), and Reply URL (assertion consumer service) values for your application, as described [here](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="5e456-133">Si vous fournissez généralement ces valeurs dans un fichier de métadonnées SAML, envoyez également ce dernier.</span><span class="sxs-lookup"><span data-stu-id="5e456-133">If you typically provide these values as part of a SAML metadata file, then please send that as well.</span></span>
* <span data-ttu-id="5e456-134">Fournissent une brève description de la façon tooconfigure Azure AD comme fournisseur d’identité dans votre application à l’aide de SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="5e456-134">Provide a brief description of how tooconfigure Azure AD as an identity provider in your application using SAML 2.0.</span></span> <span data-ttu-id="5e456-135">Si votre application prend en charge la configuration d’Azure AD comme fournisseur d’identité via un portail administratif libre-service, puis vérifiez que les informations d’identification de hello fournies ci-dessus incluent hello capacité tooset cette installation.</span><span class="sxs-lookup"><span data-stu-id="5e456-135">If your application supports configuring Azure AD as an identity provider through a self-service administrative portal, then please ensure hello credentials provided above include hello ability tooset this up.</span></span>
* <span data-ttu-id="5e456-136">Spécifiez les informations de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="5e456-136">Provide hello info below:</span></span>

> <span data-ttu-id="5e456-137">Nom de l’entreprise :</span><span class="sxs-lookup"><span data-stu-id="5e456-137">Company Name:</span></span>
> 
> <span data-ttu-id="5e456-138">Site web de l’entreprise :</span><span class="sxs-lookup"><span data-stu-id="5e456-138">Company Website:</span></span>
> 
> <span data-ttu-id="5e456-139">Nom de l’application :</span><span class="sxs-lookup"><span data-stu-id="5e456-139">Application Name:</span></span>
> 
> <span data-ttu-id="5e456-140">Description de l’application (200 caractères maximum) :</span><span class="sxs-lookup"><span data-stu-id="5e456-140">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="5e456-141">Site web de l’application (pour informatif) :</span><span class="sxs-lookup"><span data-stu-id="5e456-141">Application Website (informational):</span></span>
> 
> <span data-ttu-id="5e456-142">Site web du support technique de l’application ou les informations de contact :</span><span class="sxs-lookup"><span data-stu-id="5e456-142">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="5e456-143">URL d’inscription de l’application où les clients vont toosign pour et et/ou d’achat application hello :</span><span class="sxs-lookup"><span data-stu-id="5e456-143">Application Sign-Up URL where customers go toosign up for and /or purchase hello application:</span></span>
> 
> <span data-ttu-id="5e456-144">Choisissez les catégories de toothree pour votre toobe application répertoriés sous (pour les catégories disponibles, consultez hello [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))) :</span><span class="sxs-lookup"><span data-stu-id="5e456-144">Choose up toothree categories for your application toobe listed under (for available categories see hello [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):</span></span>
> 
> <span data-ttu-id="5e456-145">Attacher une petite icône d’application (fichier PNG, 45 px par 45 px, couleur d’arrière-plan unie) :</span><span class="sxs-lookup"><span data-stu-id="5e456-145">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="5e456-146">Attacher une grande icône d’application (fichier PNG, 215 px par 215 px, couleur d’arrière-plan unie) :</span><span class="sxs-lookup"><span data-stu-id="5e456-146">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="5e456-147">Attacher un grand logo d’application (fichier PNG, 150 px par 122 px, couleur d’arrière-plan unie) :</span><span class="sxs-lookup"><span data-stu-id="5e456-147">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

