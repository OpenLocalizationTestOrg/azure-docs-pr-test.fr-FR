---
title: "aaaApp rubriques d’aide portail d’inscription | Documents Microsoft"
description: "Description de diverses fonctionnalités dans le portail de l’enregistrement application hello Microsoft."
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: 
ms.assetid: f0507c28-9464-4d3e-bd53-de9053fd5278
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/16/2016
ms.author: lenalepa
ms.custom: aaddev
ms.openlocfilehash: 3eb17b629577446a336152799497e7d980fb825d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="app-registration-reference"></a>Informations de référence sur l’inscription des applications
Ce document fournit un contexte et des descriptions des différentes fonctionnalités de hello portail de l’enregistrement d’application Microsoft [https://apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).

## <a name="my-applications"></a>Mes applications
Cette liste contient toutes vos applications enregistrées pour une utilisation avec le point de terminaison v2.0 hello Azure AD.  Ces applications ont hello capacité toosign dans les utilisateurs avec les deux comptes personnels à partir de compte Microsoft et comptes de travail/school à partir d’Azure Active Directory.  toolearn en savoir plus sur le point de terminaison v2.0 hello Azure AD, consultez notre [vue d’ensemble de la version 2.0](active-directory-appmodel-v2-overview.md).  Ces applications peuvent être également toointegrate utilisé avec le point de terminaison de l’authentification de hello Microsoft compte, `https://login.live.com`.

## <a name="live-sdk-applications"></a>Applications du Kit de développement logiciel (SDK) Live
Cette liste contient toutes les applications inscrites pour une utilisation uniquement avec un compte Microsoft.  Elles ne peuvent pas être utilisées avec Azure Active Directory de quelque manière que ce soit.  Il s’agit où vous trouverez toutes les applications qui avaient déjà été inscrit avec le portail des développeurs MSA hello à `https://account.live.com/developers/applications`.  Toutes les fonctions précédemment effectuées sur `https://account.live.com/developers/applications` peuvent maintenant être exécutées dans ce nouveau portail, `https://apps.dev.microsoft.com`.  Si vous avez d’autres questions concernant les applications de votre compte Microsoft, veuillez nous contacter.

## <a name="application-secrets"></a>Secrets de l’application
Les clés secrètes de l’application sont les informations d’identification qui permettent la tooperform de votre application fiable [l’authentification du client](http://tools.ietf.org/html/rfc6749#section-2.3) avec Azure AD.  Dans OAuth et OpenID Connect, un secret d’application est communément référence tooas un `client_secret`.  Dans le protocole de v2.0 hello, toute application qui reçoit un jeton de sécurité à un emplacement adressable web (à l’aide un `https` schéma) doit utiliser un tooidentify secret d’application lui-même tooAzure AD lors de l’échange de ce jeton de sécurité.  En outre, n’importe quel client natif interdit de jetons reçoit sur un périphérique à l’aide d’une application secret tooperform l’authentification du client, toodiscourage hello stockage de secrets dans des environnements non sécurisés.

Chaque application peut contenir deux secrets d’application valides à un moment donné dans le temps.  En conservant deux secrets, vous avez hello ablilty tooperform périodiques substitution de la clé sur l’intégralité de l’environnement de votre application.  Une fois que vous avez migré intégralité hello de votre application tooa nouvelle clé secrète, vous pouvez supprimer l’ancienne clé secrète de hello et configurer une nouvelle.

À ce stade, seuls deux types de secrets d’application sont autorisées dans le portail de l’enregistrement d’application hello.  En choisissant **générer un nouveau mot de passe** génère et stocker un secret partagé dans le magasin de données respectifs hello, que vous pouvez utiliser dans votre application.  En choisissant **générer une nouvelle paire de clés** créera une nouvelle paire de clés publique/privée qui peut être téléchargée et utilisée pour l’authentification de client tooAzure AD.

## <a name="profile"></a>Profil
section de profil Hello du portail de l’enregistrement d’application hello peut être utilisé toocustomize hello signe dans la page de votre application.  À ce stade vous pouvez modifier le logo de l’application de la page, les conditions de la déclaration de confidentialité et les URL du service de connexion hello.  Hello logo doit être un transparent 48 x 48 ou 50 x 50 pixels image dans un fichier GIF, PNG ou JPEG de 15 Ko ou plus petit.  Essayez de modifier les valeurs hello et hello affichage résultant de page de connexion !

## <a name="live-sdk-support"></a>Support du Kit de développement logiciel (SDK) Live
Lorsque vous activez « Support de kit de développement logiciel Live », n’importe quelle application secrets que vous créez seront déployés dans hello Azure AD et les données de Microsoft Account stocke.  Cela permettra à votre toointegrate application directement avec le service Microsoft Account (login.live.com) de hello.  Si vous le souhaitez toobuild une application à l’aide de Microsoft Account directement (en tant que point de terminaison toousing opposés hello Azure AD v2.0), il se peut que vous devez vous assurer que la prise en charge du Kit de développement logiciel de Live est activée.

La désactivation de prise en charge du Kit de développement logiciel Live garantit que secret d’application hello est uniquement écrit dans le magasin de données hello Azure AD.  magasin de données Hello Azure AD intègre des réglementations d’entreprise qui lui toomeet certaines normes, telles que la conformité de FISMA.  Si vous activez le support du Kit de développement logiciel (SDK) Live, il est possible que votre application ne soit pas conforme à certaines de ces normes.

Si vous prévoyez que point de terminaison v2.0 toouse hello Azure AD, vous pouvez désactiver en toute sécurité de prise en charge du SDK actif.

