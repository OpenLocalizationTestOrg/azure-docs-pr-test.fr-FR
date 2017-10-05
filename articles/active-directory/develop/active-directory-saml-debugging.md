---
title: "Débogage d’une authentification unique basée sur SAML aux applications dans Azure Active Directory | Microsoft Docs"
description: "Découvrez comment déboguer une authentification unique basée sur SAML aux applications dans Azure Active Directory  "
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
ms.openlocfilehash: 31447d597296bac57481dc2acb4a95ee3a104161
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-debug-saml-based-single-sign-on-to-applications-in-azure-active-directory"></a><span data-ttu-id="b2ba4-103">Débogage d’une authentification unique basée sur SAML aux applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b2ba4-103">How to debug SAML-based single sign-on to applications in Azure Active Directory</span></span>
<span data-ttu-id="b2ba4-104">Lors du débogage d’une intégration d'application basée sur SAML, il est généralement conseillé d'utiliser un outil tel que [Fiddler](http://www.telerik.com/fiddler) pour afficher la requête SAML, la réponse SAML et le jeton SAML actuel émis à l'application.</span><span class="sxs-lookup"><span data-stu-id="b2ba4-104">When debugging a SAML-based application integration, it is often helpful to use a tool like [Fiddler](http://www.telerik.com/fiddler) to see the SAML request, the SAML response, and the actual SAML token that is issued to the application.</span></span> <span data-ttu-id="b2ba4-105">En examinant le jeton SAML, vous pouvez vous assurer que tous les attributs requis, le nom d'utilisateur dans l'objet SAML et l'URI de l'émetteur vous parviennent comme prévu.</span><span class="sxs-lookup"><span data-stu-id="b2ba4-105">By examining the SAML token, you can ensure that all of the required attributes, the username in the SAML subject, and the issuer URI are coming through as expected.</span></span>

![][1]

<span data-ttu-id="b2ba4-106">La réponse d'Azure AD qui contient le jeton SAML est généralement celle qui est générée après une redirection HTTP 302 depuis https://login.windows.net et qui est envoyée à **l’URL de réponse** configurée de l'application.</span><span class="sxs-lookup"><span data-stu-id="b2ba4-106">The response from Azure AD that contains the SAML token is typically the one that occurs after an HTTP 302 redirect from https://login.windows.net, and is sent to the configured **Reply URL** of the application.</span></span> 

<span data-ttu-id="b2ba4-107">Vous pouvez afficher le jeton SAML en sélectionnant cette ligne, puis l’onglet **Inspecteurs > WebForms** dans le volet droit.</span><span class="sxs-lookup"><span data-stu-id="b2ba4-107">You can view the SAML token by selecting this line and then selecting the **Inspectors > WebForms** tab in the right panel.</span></span> <span data-ttu-id="b2ba4-108">À partir de là, cliquez sur la valeur **SAMLResponse** et sélectionnez **Send to TextWizard**.</span><span class="sxs-lookup"><span data-stu-id="b2ba4-108">From there, right-click the **SAMLResponse** value and select **Send to TextWizard**.</span></span> <span data-ttu-id="b2ba4-109">Puis sélectionnez **From Base64** à partir du menu **Transform** pour décoder le jeton et afficher son contenu.</span><span class="sxs-lookup"><span data-stu-id="b2ba4-109">Then select **From Base64** from the **Transform** menu to decode the token and see its contents.</span></span>

<span data-ttu-id="b2ba4-110">**Remarque**: pour afficher le contenu de cette requête HTTP, Fiddler peut vous inviter à configurer le déchiffrement du trafic HTTPS, que vous devez effectuer.</span><span class="sxs-lookup"><span data-stu-id="b2ba4-110">**Note**: To see the contents of this HTTP request, Fiddler may prompt you to configure decryption of HTTPS traffic, which you will need to do.</span></span>

## <a name="related-articles"></a><span data-ttu-id="b2ba4-111">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="b2ba4-111">Related Articles</span></span>
* [<span data-ttu-id="b2ba4-112">Index d’articles pour la gestion des applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b2ba4-112">Article Index for Application Management in Azure Active Directory</span></span>](../active-directory-apps-index.md)
* [<span data-ttu-id="b2ba4-113">Configuration de l'authentification unique pour les applications ne faisant pas partie de la galerie d'applications Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b2ba4-113">Configuring single sign-on to applications that are not in the Azure Active Directory application gallery</span></span>](../active-directory-saas-custom-apps.md)
* [<span data-ttu-id="b2ba4-114">Personnalisation des revendications émises dans le jeton SAML pour les applications pré-intégrées</span><span class="sxs-lookup"><span data-stu-id="b2ba4-114">How to Customize Claims Issued in the SAML Token for Pre-Integrated Apps</span></span>](active-directory-saml-claims-customization.md)

<!--Image references-->
[1]: ../media/active-directory-saml-debugging/fiddler.png