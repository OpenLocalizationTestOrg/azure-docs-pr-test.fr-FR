---
title: "erreur inattendue de AAA lors de l’exécution de consentement tooan application | Documents Microsoft"
description: "Traite des erreurs qui peuvent se produire pendant le processus de hello du terme autorisation tooan application et ce que vous pouvez faire à leur sujet"
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
ms.openlocfilehash: dfee35f3a10e3cc4313109cedd972499452320f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-error-when-performing-consent-tooan-application"></a>Erreur inattendue lors de l’exécution de consentement tooan application

Cet article traite des erreurs qui peuvent se produire pendant le processus de hello de terme autorisation tooan application. Si vous rencontrez des invites de consentement inattendues qui ne contiennent aucun message d’erreur, consultez [Scénarios d’authentification pour Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios).

De nombreuses applications qui s’intègrent à Azure Active Directory nécessitent d’autres ressources dans l’ordre toofunction tooaccess d’autorisations. Lorsque ces ressources sont également intégrées dans Azure Active Directory, tooaccess autorisations leur est souvent demandé à l’aide de hello courantes consentement framework. 

Cela entraîne une invite de consentement affichée, ce qui se produit généralement hello première fois, une application est utilisée, mais peut également se produire sur une utilisation ultérieure de l’application hello.

Certaines conditions doivent être remplies pour un utilisateur tooconsent toohello les autorisations une application requiert. Si ces conditions ne sont pas remplies, différentes erreurs peuvent se produire. Vous avez notamment vu les points suivants :

## <a name="requesting-not-authorized-permissions-error"></a>Erreur : demande d’autorisations dont l’octroi n’est pas autorisé
* **AADSTS90093 :** &lt;clientAppDisplayName&gt; demande à une ou plusieurs autorisations que vous n’êtes pas autorisé à toogrant. Contactez un administrateur, ce qui peut donner son consentement des application toothis à votre place.

Cette erreur se produit lorsqu’un utilisateur qui n’est pas un administrateur d’entreprise toouse une application qui demande que seul un administrateur peut accorder des autorisations. Cette erreur peut être résolue par un administrateur de l’octroi d’application toohello d’accès pour le compte de leur organisation.

## <a name="policy-prevents-granting-permissions-error"></a>Erreur : stratégie empêchant l’octroi d’autorisations
* **AADSTS90093 :** un administrateur de &lt;tenantDisplayName&gt; a défini une stratégie qui vous empêche d’octroi &lt;nom de l’application&gt; hello il demande des autorisations. Contactez un administrateur de &lt;tenantDisplayName&gt;, qui peut accorder les autorisations des applications de toothis à votre place.

Cette erreur se produit lorsqu’un administrateur d’entreprise désactive la possibilité de hello pour les utilisateurs tooconsent tooapplications, puis un utilisateur non-administrateur tente toouse une application qui requiert le consentement. Cette erreur peut être résolue par un administrateur de l’octroi d’application toohello d’accès pour le compte de leur organisation.

## <a name="intermittent-problem-error"></a>Erreur : problème intermittent
* **AADSTS90090 :** il semble que nous avons rencontré un problème intermittent l’enregistrement des autorisations hello vous avez tenté trop toogrant&lt;clientAppDisplayName&gt;. Réessayez plus tard.

Cette erreur indique qu’un problème intermittent côté service s’est produit. Il peut être résolu par une tentative d’application de toohello tooconsent à nouveau.

## <a name="resource-not-available-error"></a>Erreur : ressource non disponible
* **AADSTS65005 :** application hello &lt;clientAppDisplayName&gt; demandé autorisations tooaccess une ressource &lt;resourceAppDisplayName&gt; qui n’est pas disponible. 

Contactez le développeur de l’application hello.

##  <a name="resource-not-available-in-tenant-error"></a>Erreur : ressource non disponible dans le locataire
* **AADSTS65005 :** &lt;clientAppDisplayName&gt; demande l’accès tooa ressource &lt;resourceAppDisplayName&gt; qui n’est pas disponible dans votre organisation &lt; tenantDisplayName&gt;. 

Vérifiez que cette ressource est disponible ou contactez un administrateur de &lt;tenantDisplayName&gt;.

## <a name="permissions-mismatch-error"></a>Erreur : incompatibilité des autorisations
* **AADSTS65005 :** application hello demandé consentement tooaccess ressource &lt;resourceAppDisplayName&gt;. Cette demande a échoué car il ne correspond pas comment application hello a été préconfigurée lors de l’inscription d’application. Contactez hello application vendor.* *

Ces erreurs tous se produire lors de l’application hello un utilisateur essaie de toois tooconsent demandant des autorisations tooaccess une application de ressource qui ne figure pas dans le répertoire de l’organisation hello (client). Cela peut se produire pour plusieurs raisons :

-   développeur d’applications client Hello a configuré son application de manière incorrecte, rend la ressource non valide de toorequest accès tooan. Dans ce cas, développeur de l’application hello doit mettre à jour configuration hello de hello client application tooresolve ce problème.

-   Un Principal de Service représentant l’application de ressource hello cible n’existe pas dans l’organisation de hello, ou existait dans hello passée, mais a été supprimé. tooresolve ce problème, un Principal de Service pour l’application de ressource hello doive être configurée dans l’organisation de hello afin de l’application cliente de hello peut demander des autorisations tooit. Cela peut se produire dans un nombre de façons, en fonction de type hello d’application, y compris :

    -   L’acquisition d’un abonnement pour l’application de ressource hello (Microsoft a publié les applications)

    -   Application de la ressource toohello terme autorisation

    -   L’octroi d’autorisations d’application hello via hello portail Azure

    -   Ajout d’application hello de hello Galerie d’applications Azure AD

## <a name="next-steps"></a>Étapes suivantes 

[Applications, autorisations et consentement dans Azure Active Directory (point de terminaison v1)](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)<br>

[Les étendues, les autorisations et consentement Bonjour Azure Active Directory (point de terminaison v2.0)](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


