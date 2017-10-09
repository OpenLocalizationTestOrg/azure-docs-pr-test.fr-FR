---
title: "Azure AD Connect : Fonctionnement de l’authentification directe | Microsoft Docs"
description: "Cet article décrit le fonctionnement de l’authentification directe Azure Active Directory."
services: active-directory
keywords: "Authentification directe Azure AD Connect, installation d’Active Directory, composants requis pour Azure AD, SSO, Authentification unique"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: billmath
ms.openlocfilehash: ffcebee572a9ba2840e81250651dea45599d65d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-technical-deep-dive"></a><span data-ttu-id="cd2e5-105">Authentification directe Azure Active Directory : immersion technique</span><span class="sxs-lookup"><span data-stu-id="cd2e5-105">Azure Active Directory Pass-through Authentication: Technical deep dive</span></span>

>[!IMPORTANT]
><span data-ttu-id="cd2e5-106">L’authentification directe Azure AD est actuellement en préversion.</span><span class="sxs-lookup"><span data-stu-id="cd2e5-106">Azure AD Pass-through Authentication is currently in preview.</span></span> 

## <a name="how-does-azure-active-directory-pass-through-authentication-work"></a><span data-ttu-id="cd2e5-107">Comment l’authentification directe Azure Active Directory fonctionne-t-elle ?</span><span class="sxs-lookup"><span data-stu-id="cd2e5-107">How does Azure Active Directory Pass-through Authentication work?</span></span>

<span data-ttu-id="cd2e5-108">Lorsqu’un utilisateur tente de toosign dans une application sécurisée par Azure Active Directory (Azure AD) et si l’authentification pass-through est activée sur le client de hello, hello étapes suivantes se produisent :</span><span class="sxs-lookup"><span data-stu-id="cd2e5-108">When a user attempts toosign into an application secured by Azure Active Directory (Azure AD), and if Pass-through Authentication is enabled on hello tenant, hello following steps occur:</span></span>

1. <span data-ttu-id="cd2e5-109">utilisateur de Hello tente tooaccess une application (par exemple, hello Outlook Web App - https://outlook.office365.com/owa/).</span><span class="sxs-lookup"><span data-stu-id="cd2e5-109">hello user tries tooaccess an application (for example, hello Outlook Web App - https://outlook.office365.com/owa/).</span></span>
2. <span data-ttu-id="cd2e5-110">Si l’utilisateur de hello n’est pas déjà inscrit, utilisateur de hello est redirigé toohello Azure AD-page de connexion.</span><span class="sxs-lookup"><span data-stu-id="cd2e5-110">If hello user is not already signed in, hello user is redirected toohello Azure AD sign-in page.</span></span>
3. <span data-ttu-id="cd2e5-111">utilisateur de Hello conclut leur nom d’utilisateur et un mot de passe hello Azure AD-page de connexion et clique sur le bouton « Connexion » de hello.</span><span class="sxs-lookup"><span data-stu-id="cd2e5-111">hello user enters their username and password into hello Azure AD sign-in page and clicks hello "Sign in" button.</span></span>
4. <span data-ttu-id="cd2e5-112">Azure AD, à la réception de demande de connexion hello, place le nom d’utilisateur hello et le mot de passe (chiffré à l’aide d’une clé publique) sur une file d’attente.</span><span class="sxs-lookup"><span data-stu-id="cd2e5-112">Azure AD, on receiving hello sign-in request, places hello username and password (encrypted  using a public key) on a queue.</span></span>
5. <span data-ttu-id="cd2e5-113">Un agent d’authentification directe local rend une file d’attente de toohello appel sortant et récupère le nom d’utilisateur hello et le mot de passe chiffré.</span><span class="sxs-lookup"><span data-stu-id="cd2e5-113">An on-premises Pass-through Authentication agent makes an outbound call toohello queue and retrieves hello username and encrypted password.</span></span>
6. <span data-ttu-id="cd2e5-114">l’agent de Hello déchiffre un mot de passe hello à l’aide de sa clé privée.</span><span class="sxs-lookup"><span data-stu-id="cd2e5-114">hello agent decrypts hello password using its private key.</span></span>
7. <span data-ttu-id="cd2e5-115">l’agent de Hello valide alors le nom d’utilisateur hello et un mot de passe dans Active Directory à l’aide des API Windows standard (un toowhat mécanisme similaire est utilisé par Active Directory Federation Services).</span><span class="sxs-lookup"><span data-stu-id="cd2e5-115">hello agent then validates hello username and password against Active Directory using standard Windows APIs (a similar mechanism toowhat is used by Active Directory Federation Services).</span></span> <span data-ttu-id="cd2e5-116">Hello nom d’utilisateur peut être un nom d’utilisateur de hello local par défaut (généralement `userPrincipalName`) ou un autre attribut configuré dans Azure AD Connect (appelé `Alternate ID`).</span><span class="sxs-lookup"><span data-stu-id="cd2e5-116">hello username can be either hello on-premises default username (usually `userPrincipalName`) or another attribute configured in Azure AD Connect (known as `Alternate ID`).</span></span>
8. <span data-ttu-id="cd2e5-117">Hello contrôleur de domaine Active Directory (DC) local, puis évalue hello demande et renvoie hello réponse appropriée (succès, échec, mot de passe expiré ou utilisateur verrouillé) toohello agent.</span><span class="sxs-lookup"><span data-stu-id="cd2e5-117">hello on-premises Active Directory Domain Controller (DC) then evaluates hello request and returns hello appropriate response (success, failure, password expired or user locked out) toohello agent.</span></span>
9. <span data-ttu-id="cd2e5-118">l’agent Hello, retourne à son tour, cette tooAzure arrière de réponse AD.</span><span class="sxs-lookup"><span data-stu-id="cd2e5-118">hello agent, in turn, returns this response back tooAzure AD.</span></span>
10. <span data-ttu-id="cd2e5-119">Azure AD évalue la réponse de hello et répond utilisateur toohello selon le cas : par exemple, il connecte les utilisateur hello immédiatement ou demande de multi-Factor Authentication (MFA).</span><span class="sxs-lookup"><span data-stu-id="cd2e5-119">Azure AD evaluates hello response and responds toohello user as appropriate - for example, it either signs hello user in immediately or requests for Multi-Factor Authentication (MFA).</span></span>
11. <span data-ttu-id="cd2e5-120">Si l’authentification utilisateur hello dans réussit, utilisateur de hello est application hello de tooaccess en mesure de.</span><span class="sxs-lookup"><span data-stu-id="cd2e5-120">If hello user sign-in is successful, hello user is able tooaccess hello application.</span></span>

<span data-ttu-id="cd2e5-121">Hello diagramme suivant illustre tous les composants de hello et étapes hello.</span><span class="sxs-lookup"><span data-stu-id="cd2e5-121">hello following diagram illustrates all hello components and hello steps involved.</span></span>

![Authentification directe](./media/active-directory-aadconnect-pass-through-authentication/pta2.png)

## <a name="next-steps"></a><span data-ttu-id="cd2e5-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cd2e5-123">Next steps</span></span>
- <span data-ttu-id="cd2e5-124">[**Limitations actuelles**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) : cette fonctionnalité est actuellement en préversion.</span><span class="sxs-lookup"><span data-stu-id="cd2e5-124">[**Current limitations**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - This feature is currently in preview.</span></span> <span data-ttu-id="cd2e5-125">Découvrez les scénarios pris en charge et ceux qui ne le sont pas.</span><span class="sxs-lookup"><span data-stu-id="cd2e5-125">Learn which scenarios are supported and which ones are not.</span></span>
- <span data-ttu-id="cd2e5-126">[**Démarrage rapide**](active-directory-aadconnect-pass-through-authentication-quick-start.md) : soyez opérationnel avec l’authentification directe Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cd2e5-126">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="cd2e5-127">[**Forum aux Questions** ](active-directory-aadconnect-pass-through-authentication-faq.md) -réponses elles sonttrop aux questions.</span><span class="sxs-lookup"><span data-stu-id="cd2e5-127">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="cd2e5-128">[**Résoudre les problèmes** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -en savoir comment tooresolve commun problèmes avec la fonctionnalité de hello.</span><span class="sxs-lookup"><span data-stu-id="cd2e5-128">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="cd2e5-129">[**Authentification unique transparente Azure AD**](active-directory-aadconnect-sso.md) : explorez en détail cette fonctionnalité complémentaire.</span><span class="sxs-lookup"><span data-stu-id="cd2e5-129">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="cd2e5-130">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) : pour formuler des demandes de nouvelles fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="cd2e5-130">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
