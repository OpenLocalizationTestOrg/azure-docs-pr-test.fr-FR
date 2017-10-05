---
title: "Affichage de votre application dans la galerie d’applications Azure AD"
description: "Comment répertorier une application qui prend en charge l'authentification unique dans la galerie Azure Active Directory | Microsoft Azure"
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
ms.openlocfilehash: cf25772bd9d92b59401aa5da76e6bbd5fa5ee3e5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="listing-your-application-in-the-azure-active-directory-application-gallery"></a><span data-ttu-id="053b6-103">Affichage de votre application dans la galerie d’applications Azure AD</span><span class="sxs-lookup"><span data-stu-id="053b6-103">Listing your application in the Azure Active Directory application gallery</span></span>
<span data-ttu-id="053b6-104">Pour répertorier une application qui prend en charge l'authentification unique avec Azure Active Directory dans la [galerie Azure AD](https://azure.microsoft.com/marketplace/active-directory/all/), l'application doit tout d'abord mettre en œuvre l'un des modes d'intégration suivants :</span><span class="sxs-lookup"><span data-stu-id="053b6-104">To list an application that supports single sign-on with Azure Active Directory in the [Azure AD gallery](https://azure.microsoft.com/marketplace/active-directory/all/), the application first needs to implement one of the following integration modes:</span></span>

* <span data-ttu-id="053b6-105">**OpenID Connect** : intégration directe dans Azure AD à l'aide d'OpenID Connect pour l'authentification et l'API de consentement Azure AD pour la configuration.</span><span class="sxs-lookup"><span data-stu-id="053b6-105">**OpenID Connect** - Direct integration with Azure AD using OpenID Connect for authentication and the Azure AD consent API for configuration.</span></span> <span data-ttu-id="053b6-106">Si vous débutez une intégration et que votre application ne prend pas en charge SAML, il s'agit du mode de recommandé.</span><span class="sxs-lookup"><span data-stu-id="053b6-106">If you are just starting an integration and your application does not support SAML, then this is the recommend mode.</span></span>
* <span data-ttu-id="053b6-107">**SAML** : votre application a déjà la possibilité de configurer des fournisseurs d'identité tiers utilisant le protocole SAML.</span><span class="sxs-lookup"><span data-stu-id="053b6-107">**SAML** – Your application already has the ability to configure third-party identity providers using the SAML protocol.</span></span>

<span data-ttu-id="053b6-108">Les exigences pour chaque mode sont indiquées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="053b6-108">Listing requirements for each mode are below.</span></span>

## <a name="openid-connect-integration"></a><span data-ttu-id="053b6-109">Intégration d'OpenID Connect</span><span class="sxs-lookup"><span data-stu-id="053b6-109">OpenID Connect Integration</span></span>
<span data-ttu-id="053b6-110">Pour intégrer votre application dans Azure AD, suivez les [instructions pour développeurs](active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="053b6-110">To integrate your application with Azure AD, following the [developer instructions](active-directory-authentication-scenarios.md).</span></span> <span data-ttu-id="053b6-111">Puis répondez aux questions ci-dessous et adressez vos réponses à waadpartners@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="053b6-111">Then complete the questions below and send to waadpartners@microsoft.com.</span></span>

* <span data-ttu-id="053b6-112">Fournissez des informations d'identification pour votre application pour un locataire ou un compte de test pouvant être utilisées par l'équipe Azure AD pour tester l'intégration.</span><span class="sxs-lookup"><span data-stu-id="053b6-112">Provide credentials for a test tenant or account with your application that can be used by the Azure AD team to test the integration.</span></span>  
* <span data-ttu-id="053b6-113">Fournissez des instructions sur la manière dont l'équipe Azure AD peut se connecter et connecter une instance d'Azure AD à votre application à l'aide de l' [infrastructure de consentement d'Azure AD](active-directory-integrating-applications.md#overview-of-the-consent-framework).</span><span class="sxs-lookup"><span data-stu-id="053b6-113">Provide instructions on how the Azure AD team can sign in and connect an instance of Azure AD to your application using the [Azure AD consent framework](active-directory-integrating-applications.md#overview-of-the-consent-framework).</span></span> 
* <span data-ttu-id="053b6-114">Fournissez toute instruction supplémentaire nécessaire pour permettre à l'équipe Azure AD de tester l'authentification unique avec votre application.</span><span class="sxs-lookup"><span data-stu-id="053b6-114">Provide any further instructions required for the Azure AD team to test single sign-on with your application.</span></span> 
* <span data-ttu-id="053b6-115">Fournissez les informations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="053b6-115">Provide the info below:</span></span>

> <span data-ttu-id="053b6-116">Nom de l’entreprise :</span><span class="sxs-lookup"><span data-stu-id="053b6-116">Company Name:</span></span>
> 
> <span data-ttu-id="053b6-117">Site web de l’entreprise :</span><span class="sxs-lookup"><span data-stu-id="053b6-117">Company Website:</span></span>
> 
> <span data-ttu-id="053b6-118">Nom de l’application :</span><span class="sxs-lookup"><span data-stu-id="053b6-118">Application Name:</span></span>
> 
> <span data-ttu-id="053b6-119">Description de l’application (200 caractères maximum) :</span><span class="sxs-lookup"><span data-stu-id="053b6-119">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="053b6-120">Site web de l’application (pour informatif) :</span><span class="sxs-lookup"><span data-stu-id="053b6-120">Application Website (informational):</span></span>
> 
> <span data-ttu-id="053b6-121">Site web du support technique de l’application ou les informations de contact :</span><span class="sxs-lookup"><span data-stu-id="053b6-121">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="053b6-122">ID d’application de l’application, comme indiqué dans les détails de l’application à https://portal.azure.com :</span><span class="sxs-lookup"><span data-stu-id="053b6-122">Application  ID of the application, as shown in the application details at https://portal.azure.com:</span></span>
> 
> <span data-ttu-id="053b6-123">URL d’inscription d’application à laquelle les clients accèdent pour s’inscrire et/ou acheter l’application :</span><span class="sxs-lookup"><span data-stu-id="053b6-123">Application Sign-Up URL where customers go to sign up for and /or purchase the application:</span></span>
> 
> <span data-ttu-id="053b6-124">Sélectionnez jusqu’à trois catégories répertoriées pour votre application (pour connaître les catégories disponibles, consultez l'Azure Active Directory Marketplace) :</span><span class="sxs-lookup"><span data-stu-id="053b6-124">Choose up to three categories for your application to be listed under (for available categories see the Azure Active Directory Marketplace):</span></span>
> 
> <span data-ttu-id="053b6-125">Attacher une petite icône d’application (fichier PNG, 45 px par 45 px, couleur d’arrière-plan unie) :</span><span class="sxs-lookup"><span data-stu-id="053b6-125">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="053b6-126">Attacher une grande icône d’application (fichier PNG, 215 px par 215 px, couleur d’arrière-plan unie) :</span><span class="sxs-lookup"><span data-stu-id="053b6-126">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="053b6-127">Attacher un grand logo d’application (fichier PNG, 150 px par 122 px, couleur d’arrière-plan unie) :</span><span class="sxs-lookup"><span data-stu-id="053b6-127">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

## <a name="saml-integration"></a><span data-ttu-id="053b6-128">Intégration de SAML</span><span class="sxs-lookup"><span data-stu-id="053b6-128">SAML Integration</span></span>
<span data-ttu-id="053b6-129">Toute application prenant en charge SAML 2.0 peut être intégrée directement dans un locataire Azure AD à l'aide de [ces instructions pour ajouter une application personnalisée](../active-directory-saas-custom-apps.md).</span><span class="sxs-lookup"><span data-stu-id="053b6-129">Any app that supports SAML 2.0 can be integrated directly with an Azure AD tenant using [these instructions to add a custom application](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="053b6-130">Une fois que vous avez testé que l'intégration de votre application fonctionne avec Azure AD, envoyez les informations suivantes à l'adresse <mailto:waadpartners@microsoft.com>.</span><span class="sxs-lookup"><span data-stu-id="053b6-130">Once you have tested that your application integration works with Azure AD, send the following information to <mailto:waadpartners@microsoft.com>.</span></span>

* <span data-ttu-id="053b6-131">Fournissez des informations d'identification pour votre application pour un locataire ou un compte de test pouvant être utilisées par l'équipe Azure AD pour tester l'intégration.</span><span class="sxs-lookup"><span data-stu-id="053b6-131">Provide credentials for a test tenant or account with your application that can be used by the Azure AD team to test the integration.</span></span>  
* <span data-ttu-id="053b6-132">Fournissez l'URL de connexion SAML, l'URL de l'émetteur (ID d'entité) et l'URL de réponse (Assertion Consumer Service) pour votre application, comme indiqué [ici](../active-directory-saas-custom-apps.md).</span><span class="sxs-lookup"><span data-stu-id="053b6-132">Provide the SAML Sign-On URL, Issuer URL (entity ID), and Reply URL (assertion consumer service) values for your application, as described [here](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="053b6-133">Si vous fournissez généralement ces valeurs dans un fichier de métadonnées SAML, envoyez également ce dernier.</span><span class="sxs-lookup"><span data-stu-id="053b6-133">If you typically provide these values as part of a SAML metadata file, then please send that as well.</span></span>
* <span data-ttu-id="053b6-134">Fournissez une brève description de la configuration d'Azure AD comme fournisseur d'identité dans votre application à l'aide de SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="053b6-134">Provide a brief description of how to configure Azure AD as an identity provider in your application using SAML 2.0.</span></span> <span data-ttu-id="053b6-135">Si votre application prend en charge la configuration d'Azure AD comme fournisseur d'identité via un portail d'administration en libre-service, assurez-vous que les informations d'identification fournies vous le permettent.</span><span class="sxs-lookup"><span data-stu-id="053b6-135">If your application supports configuring Azure AD as an identity provider through a self-service administrative portal, then please ensure the credentials provided above include the ability to set this up.</span></span>
* <span data-ttu-id="053b6-136">Fournissez les informations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="053b6-136">Provide the info below:</span></span>

> <span data-ttu-id="053b6-137">Nom de l’entreprise :</span><span class="sxs-lookup"><span data-stu-id="053b6-137">Company Name:</span></span>
> 
> <span data-ttu-id="053b6-138">Site web de l’entreprise :</span><span class="sxs-lookup"><span data-stu-id="053b6-138">Company Website:</span></span>
> 
> <span data-ttu-id="053b6-139">Nom de l’application :</span><span class="sxs-lookup"><span data-stu-id="053b6-139">Application Name:</span></span>
> 
> <span data-ttu-id="053b6-140">Description de l’application (200 caractères maximum) :</span><span class="sxs-lookup"><span data-stu-id="053b6-140">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="053b6-141">Site web de l’application (pour informatif) :</span><span class="sxs-lookup"><span data-stu-id="053b6-141">Application Website (informational):</span></span>
> 
> <span data-ttu-id="053b6-142">Site web du support technique de l’application ou les informations de contact :</span><span class="sxs-lookup"><span data-stu-id="053b6-142">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="053b6-143">URL d’inscription d’application à laquelle les clients accèdent pour s’inscrire et/ou acheter l’application :</span><span class="sxs-lookup"><span data-stu-id="053b6-143">Application Sign-Up URL where customers go to sign up for and /or purchase the application:</span></span>
> 
> <span data-ttu-id="053b6-144">Sélectionnez jusqu'à trois catégories à répertorier pour votre application sous (pour connaître les catégories disponibles, consultez le site [Marketplace Azure Active Directory](https://azure.microsoft.com/marketplace/active-directory/)) :</span><span class="sxs-lookup"><span data-stu-id="053b6-144">Choose up to three categories for your application to be listed under (for available categories see the [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):</span></span>
> 
> <span data-ttu-id="053b6-145">Attacher une petite icône d’application (fichier PNG, 45 px par 45 px, couleur d’arrière-plan unie) :</span><span class="sxs-lookup"><span data-stu-id="053b6-145">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="053b6-146">Attacher une grande icône d’application (fichier PNG, 215 px par 215 px, couleur d’arrière-plan unie) :</span><span class="sxs-lookup"><span data-stu-id="053b6-146">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="053b6-147">Attacher un grand logo d’application (fichier PNG, 150 px par 122 px, couleur d’arrière-plan unie) :</span><span class="sxs-lookup"><span data-stu-id="053b6-147">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

