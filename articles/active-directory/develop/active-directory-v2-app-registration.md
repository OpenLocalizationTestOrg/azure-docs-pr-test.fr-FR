---
title: "aaaRegister une application avec un point de terminaison v2.0 hello Azure AD à l’aide du portail de hello | Documents Microsoft"
description: "Comment tooregister une application avec Microsoft pour l’activation de l’authentification et l’accès à Microsoft services à l’aide du point de terminaison hello v2.0"
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: 
ms.assetid: bb2f701f-3bc3-4759-94a5-8b9d53a8a0b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: lenalepa
ms.custom: aaddev
ms.openlocfilehash: c56c98906656062435516e820cb318a04c03149c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooregister-an-app-with-hello-v20-endpoint"></a>Comment tooregister une application avec un point de terminaison hello v2.0
toobuild une application qui accepte le compte de service administré et Azure AD, sign-in, vous devez tout d’abord tooregister une application avec Microsoft.  À ce stade, vous ne serez pas être en mesure de toouse toutes les applications existantes, vous auriez conclus avec Azure AD ou MSA - vous devez toocreate une marque de nouveau.

> [!NOTE]
> Pas tous les scénarios Azure Active Directory et les fonctionnalités sont prises en charge par le point de terminaison hello v2.0.  toodetermine si vous devez utiliser le point de terminaison hello v2.0, en savoir plus sur [v2.0 limitations](active-directory-v2-limitations.md).
> 
> 

## <a name="visit-hello-microsoft-app-registration-portal"></a>Visitez le portail d’inscription application hello Microsoft
Avant tout - accédez d’abord trop[https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).  Il s’agit d’un nouveau portail d’inscription des applications où vous pouvez gérer vos applications Microsoft.

Connectez-vous à l’aide d’un compte Microsoft personnel, professionnel ou scolaire.  Si vous en êtes dépourvu, inscrivez-vous pour obtenir un nouveau compte personnel. Cela ne sera pas long. Nous patientons ici.

Vous avez terminé ? À présent, consultez votre liste d’applications Microsoft, qui est probablement vide.  Nous allons y remédier.

Cliquez sur **Ajouter une application**, et attribuez-lui un nom.  portail de Hello affectera votre application un Id global unique d’Application que vous utiliserez ultérieurement dans votre code.  Si votre application inclut un composant côté serveur qui a besoin de jetons d’accès pour appeler des API (pensez : Office, Azure ou votre propre API web), vous souhaiterez toocreate un **Secret d’Application** ici.

Ensuite, ajoutez hello plateformes que votre application utilisera.

* Pour les applications basées sur le Web, fournissez une **URI de redirection** où les messages de connexion peuvent être envoyés.
* Pour les applications mobiles, copiez la valeur par défaut hello créé automatiquement pour vous des uri de redirection.

Si vous le souhaitez, vous pouvez personnaliser hello apparence de votre page de connexion Bonjour profil.  Assurez-vous que tooclick **enregistrer** avant de continuer.

> [!NOTE]
> Lorsque vous créez une application en utilisant [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), application hello est enregistrée dans le locataire d’accueil hello hello de compte de que vous utilisez toosign portail de hello.  Cela signifie que vous ne pouvez pas inscrire une application dans votre client Azure AD à l’aide d’un compte Microsoft personnel.  Si vous explicitement souhaitez tooregister une application dans un locataire particulier, connectez-vous avec un compte créé à l’origine de ce client.
> 
> 

## <a name="build-a-quick-start-app"></a>Générer une application de démarrage rapide
Maintenant que vous disposez d’une application Microsoft, vous pouvez suivre l’un de nos didacticiels de démarrage rapide de v2.0.  Voici quelques recommandations :

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

