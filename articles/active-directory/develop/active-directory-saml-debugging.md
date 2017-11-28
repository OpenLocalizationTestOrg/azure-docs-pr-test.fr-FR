---
title: "aaaHow toodebug basé sur SAML uniques authentification tooapplications dans Azure Active Directory | Documents Microsoft"
description: "Découvrez comment toodebug basé sur SAML uniques authentification tooapplications dans Azure Active Directory "
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: edbe492b-1050-4fca-a48a-d1fa97d47815
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: asmalser
ms.custom: aaddev
ms.reviewer: dastrock
ms.openlocfilehash: 846c7b3497c8842947c5b406f4362b9e06785b14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodebug-saml-based-single-sign-on-tooapplications-in-azure-active-directory"></a><span data-ttu-id="e0bd3-103">Comment toodebug basé sur SAML uniques authentification tooapplications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e0bd3-103">How toodebug SAML-based single sign-on tooapplications in Azure Active Directory</span></span>
<span data-ttu-id="e0bd3-104">Lors du débogage d’une intégration d’application basée sur SAML, il est souvent utile toouse un outil tel que [Fiddler](http://www.telerik.com/fiddler) toosee hello demande SAML, réponse SAML hello et hello réel jeton SAML qui est émise toohello application.</span><span class="sxs-lookup"><span data-stu-id="e0bd3-104">When debugging a SAML-based application integration, it is often helpful toouse a tool like [Fiddler](http://www.telerik.com/fiddler) toosee hello SAML request, hello SAML response, and hello actual SAML token that is issued toohello application.</span></span> <span data-ttu-id="e0bd3-105">En examinant le jeton SAML de hello, vous pouvez vous assurer que tous les hello attributs requis, hello nom d’utilisateur dans l’objet SAML hello et hello émetteur URI arrivent via comme prévu.</span><span class="sxs-lookup"><span data-stu-id="e0bd3-105">By examining hello SAML token, you can ensure that all of hello required attributes, hello username in hello SAML subject, and hello issuer URI are coming through as expected.</span></span>

![][1]

<span data-ttu-id="e0bd3-106">Hello réponse Azure AD, qui contient le jeton SAML de hello est généralement hello qui a lieu après une redirection HTTP 302 de https://login.windows.net et toohello envoyé n’est configuré **URL de réponse** de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="e0bd3-106">hello response from Azure AD that contains hello SAML token is typically hello one that occurs after an HTTP 302 redirect from https://login.windows.net, and is sent toohello configured **Reply URL** of hello application.</span></span> 

<span data-ttu-id="e0bd3-107">Vous pouvez afficher le jeton SAML de hello en sélectionnant cette ligne, puis en sélectionnant hello **inspecteurs > WebForms** onglet dans le panneau droit hello.</span><span class="sxs-lookup"><span data-stu-id="e0bd3-107">You can view hello SAML token by selecting this line and then selecting hello **Inspectors > WebForms** tab in hello right panel.</span></span> <span data-ttu-id="e0bd3-108">À partir de là, avec le bouton droit hello **SAMLResponse** valeur et sélectionnez **envoyer tooTextWizard**.</span><span class="sxs-lookup"><span data-stu-id="e0bd3-108">From there, right-click hello **SAMLResponse** value and select **Send tooTextWizard**.</span></span> <span data-ttu-id="e0bd3-109">Puis sélectionnez **à partir de Base64** de hello **transformer** menu toodecode hello jeton et afficher son contenu.</span><span class="sxs-lookup"><span data-stu-id="e0bd3-109">Then select **From Base64** from hello **Transform** menu toodecode hello token and see its contents.</span></span>

<span data-ttu-id="e0bd3-110">**Remarque**: demande de contenu de hello toosee cette HTTP, Fiddler peut vous demander de déchiffrement tooconfigure du trafic HTTPS, vous devez toodo.</span><span class="sxs-lookup"><span data-stu-id="e0bd3-110">**Note**: toosee hello contents of this HTTP request, Fiddler may prompt you tooconfigure decryption of HTTPS traffic, which you will need toodo.</span></span>

## <a name="related-articles"></a><span data-ttu-id="e0bd3-111">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="e0bd3-111">Related Articles</span></span>
* [<span data-ttu-id="e0bd3-112">Index d’articles pour la gestion des applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e0bd3-112">Article Index for Application Management in Azure Active Directory</span></span>](../active-directory-apps-index.md)
* [<span data-ttu-id="e0bd3-113">Configuration uniques tooapplications ouverture de session qui ne sont pas dans la galerie d’applications Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="e0bd3-113">Configuring single sign-on tooapplications that are not in hello Azure Active Directory application gallery</span></span>](../active-directory-saas-custom-apps.md)
* [<span data-ttu-id="e0bd3-114">Comment tooCustomize les revendications émises dans hello du jeton SAML pour les applications Pre-Integrated</span><span class="sxs-lookup"><span data-stu-id="e0bd3-114">How tooCustomize Claims Issued in hello SAML Token for Pre-Integrated Apps</span></span>](active-directory-saml-claims-customization.md)

<!--Image references-->
[1]: ../media/active-directory-saml-debugging/fiddler.png