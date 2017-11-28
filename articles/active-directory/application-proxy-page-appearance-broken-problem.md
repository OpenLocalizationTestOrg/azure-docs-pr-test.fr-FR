---
title: "aaaApplication page ne s’affiche pas correctement pour une application de Proxy d’Application | Documents Microsoft"
description: "Guide de page de hello n’affiche pas correctement dans une Application de Proxy d’Application que vous avez intégré à Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: f4abaa4e94c512868f2085affe59cac443784a56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-page-does-not-display-correctly-for-an-application-proxy-application"></a><span data-ttu-id="140a1-103">La page d’application ne s’affiche pas correctement pour une application de proxy d’application</span><span class="sxs-lookup"><span data-stu-id="140a1-103">Application page does not display correctly for an Application Proxy application</span></span>

<span data-ttu-id="140a1-104">Cet article vous a-t-il tootroubleshoot des problèmes avec les applications du Proxy d’Application Azure Active Directory lorsque vous accédez toohello page, mais un élément de page de hello ne ressemble pas correct.</span><span class="sxs-lookup"><span data-stu-id="140a1-104">This article help you tootroubleshoot issues with Azure Active Directory Application Proxy applications when you navigate toohello page, but something on hello page doesn't look correct.</span></span>

## <a name="overview"></a><span data-ttu-id="140a1-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="140a1-105">Overview</span></span>
<span data-ttu-id="140a1-106">Lorsque vous publiez une application de Proxy d’Application, seules les pages sous la racine sont accessibles lors de l’accès d’application hello.</span><span class="sxs-lookup"><span data-stu-id="140a1-106">When you publish an Application Proxy app, only pages under your root are accessible when accessing hello application.</span></span> <span data-ttu-id="140a1-107">Si la page de hello n’affiche pas correctement, hello racine une URL interne utilisée pour l’application hello manque peut-être des ressources de la page.</span><span class="sxs-lookup"><span data-stu-id="140a1-107">If hello page isn’t displaying correctly, hello root internal URL used for hello application may be missing some page resources.</span></span> <span data-ttu-id="140a1-108">tooresolve, assurez-vous que vous avez publié *tous les* hello des ressources pour hello page dans le cadre de votre application.</span><span class="sxs-lookup"><span data-stu-id="140a1-108">tooresolve, make sure you have published *all* hello resources for hello page as part of your application.</span></span>

<span data-ttu-id="140a1-109">Vous pouvez vérifier cela est un problème de hello en ouvrant votre dispositif de suivi réseau (tel que Fiddler ou F12 outils dans Internet Explorer/Edge), le chargement de page de hello et recherchez les 404 erreurs.</span><span class="sxs-lookup"><span data-stu-id="140a1-109">You can verify this is hello issue by opening your network tracker (such as Fiddler, or F12 tools in Internet Explorer/Edge), loading hello page, and looking for 404 errors.</span></span> <span data-ttu-id="140a1-110">Qui indique les pages hello actuellement impossible de trouver et devrez peut-être toobe publié.</span><span class="sxs-lookup"><span data-stu-id="140a1-110">That indicates hello pages that currently cannot be found and may still need toobe published.</span></span>

<span data-ttu-id="140a1-111">Un exemple de ce cas, supposons que vous avez publié une application de dépenses à l’aide d’une URL interne de <http://myapps/expenses>, mais utilise l’application hello hello stylesheet <http://myapps/style.css>.</span><span class="sxs-lookup"><span data-stu-id="140a1-111">As an example of this case, assume you have published an expenses application using an internal URL of <http://myapps/expenses>, but hello app uses hello stylesheet <http://myapps/style.css>.</span></span> <span data-ttu-id="140a1-112">Dans ce cas, feuille de style hello n’est pas publié dans votre application, afin de chargement hello dépenses application lève une erreur 404 lors des style.css tooload lors de la tentative.</span><span class="sxs-lookup"><span data-stu-id="140a1-112">In this case, hello stylesheet is not published in your application, so loading hello expenses app throw a 404 error while trying tooload style.css.</span></span> <span data-ttu-id="140a1-113">Dans cet exemple, le problème de hello serait être résolu en publiant l’application hello avec une URL interne de <http://myapp/> à la place.</span><span class="sxs-lookup"><span data-stu-id="140a1-113">In this example, hello problem would be resolved by publishing hello application with an internal URL of <http://myapp/> instead.</span></span>

## <a name="problems-with-publishing-as-one-application"></a><span data-ttu-id="140a1-114">Problèmes liés à la publication d’une seule application</span><span class="sxs-lookup"><span data-stu-id="140a1-114">Problems with publishing as one application</span></span>

<span data-ttu-id="140a1-115">S’il n’est pas possible de toopublish toutes les ressources dans hello même application, vous devez toopublish plusieurs applications et activez des liens entre eux.</span><span class="sxs-lookup"><span data-stu-id="140a1-115">If it is not possible toopublish all resources within hello same application, you need toopublish multiple applications and enable links between them.</span></span>

<span data-ttu-id="140a1-116">toodo par conséquent, nous vous recommandons d’utiliser hello [des domaines personnalisés](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solution.</span><span class="sxs-lookup"><span data-stu-id="140a1-116">toodo so, we recommend using hello [custom domains](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solution.</span></span> <span data-ttu-id="140a1-117">Toutefois, cette solution exige que vous possédez le certificat de hello pour votre domaine et vos applications utilisent des noms de domaine complet (FQDN).</span><span class="sxs-lookup"><span data-stu-id="140a1-117">However, this solution requires that you own hello certificate for your domain and your applications use fully qualified domain names (FQDNs).</span></span> <span data-ttu-id="140a1-118">Pour les autres options, consultez hello [résoudre les liens rompus documentation](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span><span class="sxs-lookup"><span data-stu-id="140a1-118">For other options, see hello [troubleshoot broken links documentation](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span></span>

## <a name="next-steps"></a><span data-ttu-id="140a1-119">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="140a1-119">Next steps</span></span>
[<span data-ttu-id="140a1-120">Publier des applications avec le Proxy d’application Azure AD</span><span class="sxs-lookup"><span data-stu-id="140a1-120">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
