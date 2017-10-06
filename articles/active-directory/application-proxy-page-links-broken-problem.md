---
title: "aaaLinks sur la page de hello ne fonctionnent pas pour une application de Proxy d’Application | Documents Microsoft"
description: "Comment tootroubleshoot problèmes avec des liens rompus sur les applications du Proxy d’Application que vous avez intégré avec Azure AD"
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
ms.openlocfilehash: 77c1e22d27c7a6436d8e57e105037c2328180481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="links-on-hello-page-dont-work-for-an-application-proxy-application"></a>Liens sur la page de hello ne fonctionnent pas pour une application de Proxy d’Application

Cet article vous a-t-il tootroubleshoot pourquoi les liens de votre application de Proxy d’Application Azure Active Directory ne fonctionnent pas correctement.

## <a name="overview"></a>Vue d'ensemble 
Après la publication d’une application de Proxy d’Application, seuls les liens hello que le travail par défaut dans l’application hello sont toodestinations liens contenues dans hello publié URL racine. liens Hello dans les applications hello ne fonctionnent pas, une URL interne pour l’application hello hello probablement n’inclut pas toutes les destinations hello de liens dans l’application hello.

**Pourquoi cela se produit-il ?** Lorsque vous cliquez sur un lien dans une application, le Proxy d’Application tentatives tooresolve hello l’URL soit une URL interne dans hello même application, ou comme une URL disponible en externe. Si le lien de hello pointe tooan URL interne qui n’est pas dans hello même application, il n’appartiennent tooeither de ces compartiments et provoque une erreur introuvable.

## <a name="ways-you-can-resolve-broken-links"></a>Comment résoudre les liens rompus

Il existe trois façons tooresolve ce problème. choix de Hello ci-dessous sont de complexité croissante répertoriée dans.

1.  Assurez-vous que les URL interne hello est une racine qui contient tous les liens pertinents hello pour une application hello. Cela permet à tous les liens toobe résolu comme le contenu publié dans hello même application.

    Si vous modifiez une URL interne hello mais que vous ne souhaitez pas hello toochange page pour les utilisateurs de lancement, modification hello URL de la page d’accueil toohello précédemment publié une URL interne. Cela est possible en accédant trop « Azure Active Directory » -&gt; inscriptions d’application -&gt; sélectionnez application hello -&gt; propriétés. Dans cet onglet de propriétés, vous voyez le champ de hello « Page d’accueil URL », vous pouvez toutefois ajuster toobe hello souhaité page d’accueil.

2.  Si vos applications utilisent des noms de domaine complet (FQDN), utilisez [des domaines personnalisés](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) toopublish vos applications. Cette fonctionnalité permet hello même URL toobe utilisé en interne et externe.

    Cette option garantit que les liens hello dans votre application sont en externe accessibles via le Proxy d’Application, car les liens hello hello application toointernal URL sont également reconnus en externe. Notez que tous les liens dispensent toobelong tooa publié l’application. Cependant, avec cette hello option liens n’ont pas toobelong toohello même application et peut appartenir toomultiple applications.

3.  Si aucune de ces options sont envisageables, vous joignez aperçu hello pour une nouvelle fonctionnalité qui effectuent la traduction/réécriture d’URL. Avec cette option, les URL interne ou des liens qui existent dans le corps de hello HTML de vos applications être traduits, ou « mappé », toohello publié URL de Proxy d’application externe. Cela fonctionne uniquement pour les liens Bonjour HTML ou CSS, et cela n'aide pas si votre liaison est générée via JS. 

Par conséquent, nous recommandons à l’aide de hello [des domaines personnalisés](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solution si possible. Si vous ne souhaitez pas que la version préliminaire de hello toojoin, envoyez un e-mail < aadapfeedback@microsoft.com > avec hello applicationId(s).

## <a name="next-steps"></a>Étapes suivantes
[Travailler avec des serveurs proxy locaux existants](application-proxy-working-with-proxy-servers.md)

