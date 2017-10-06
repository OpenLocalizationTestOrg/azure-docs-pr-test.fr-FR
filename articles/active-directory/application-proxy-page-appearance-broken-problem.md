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
# <a name="application-page-does-not-display-correctly-for-an-application-proxy-application"></a>La page d’application ne s’affiche pas correctement pour une application de proxy d’application

Cet article vous a-t-il tootroubleshoot des problèmes avec les applications du Proxy d’Application Azure Active Directory lorsque vous accédez toohello page, mais un élément de page de hello ne ressemble pas correct.

## <a name="overview"></a>Vue d'ensemble
Lorsque vous publiez une application de Proxy d’Application, seules les pages sous la racine sont accessibles lors de l’accès d’application hello. Si la page de hello n’affiche pas correctement, hello racine une URL interne utilisée pour l’application hello manque peut-être des ressources de la page. tooresolve, assurez-vous que vous avez publié *tous les* hello des ressources pour hello page dans le cadre de votre application.

Vous pouvez vérifier cela est un problème de hello en ouvrant votre dispositif de suivi réseau (tel que Fiddler ou F12 outils dans Internet Explorer/Edge), le chargement de page de hello et recherchez les 404 erreurs. Qui indique les pages hello actuellement impossible de trouver et devrez peut-être toobe publié.

Un exemple de ce cas, supposons que vous avez publié une application de dépenses à l’aide d’une URL interne de <http://myapps/expenses>, mais utilise l’application hello hello stylesheet <http://myapps/style.css>. Dans ce cas, feuille de style hello n’est pas publié dans votre application, afin de chargement hello dépenses application lève une erreur 404 lors des style.css tooload lors de la tentative. Dans cet exemple, le problème de hello serait être résolu en publiant l’application hello avec une URL interne de <http://myapp/> à la place.

## <a name="problems-with-publishing-as-one-application"></a>Problèmes liés à la publication d’une seule application

S’il n’est pas possible de toopublish toutes les ressources dans hello même application, vous devez toopublish plusieurs applications et activez des liens entre eux.

toodo par conséquent, nous vous recommandons d’utiliser hello [des domaines personnalisés](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solution. Toutefois, cette solution exige que vous possédez le certificat de hello pour votre domaine et vos applications utilisent des noms de domaine complet (FQDN). Pour les autres options, consultez hello [résoudre les liens rompus documentation](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).

## <a name="next-steps"></a>Étapes suivantes
[Publier des applications avec le Proxy d’application Azure AD](application-proxy-publish-azure-portal.md)
