---
title: "Azure Active Directory B2C : création d’un client Azure Active Directory B2C | Microsoft Docs"
description: Une rubrique sur comment toocreate un Active Directory B2C du Azure locataire
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: patricka
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/07/2017
ms.author: swkrish
ms.openlocfilehash: e8b257d66c1f66ffb84f5d3d21b30b42eddcbac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-active-directory-b2c-tenant-in-hello-azure-portal"></a>Créer un locataire Azure Active Directory B2C Bonjour portail Azure

Modifié par Sipi.

Ce démarrage rapide vous aide à créer un locataire Microsoft Azure Active Directory (Azure AD) B2C en seulement quelques minutes. Lorsque vous avez terminé, vous avez un toouse du locataire B2C pour inscrire les applications B2C.

## <a name="prerequisites"></a>Composants requis

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

##  <a name="log-in-tooazure"></a>Connectez-vous à tooAzure

Connectez-vous à toohello [portail Azure](https://portal.azure.com/).

## <a name="create-an-azure-ad-b2c-tenant"></a>Créer un client Azure AD B2C

Les fonctionnalités B2C ne peuvent pas être activées dans vos locataires existants. Vous devez toocreate un locataire Azure AD B2C.

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

Félicitations, vous avez créé un locataire Azure Active Directory B2C. Vous êtes un administrateur Global du client de hello. Vous pouvez ajouter d’autres administrateurs généraux en fonction des besoins. tooyour tooswitch nouveau client, cliquez sur hello *gérer votre nouvelle liaison de client*.

![Lien permettant de gérer votre nouveau locataire](./media/active-directory-b2c-get-started/manage-new-b2c-tenant-link.png)

> [!IMPORTANT]
> Si vous envisagez de toouse un locataire B2C pour une application de production, lisez l’article de hello sur [production à l’échelle par rapport aux locataires de la version préliminaire B2C](active-directory-b2c-reference-tenant-type.md). Il sont problèmes connus lorsque vous supprimez un B2C existant du locataire et recréez-la avec hello même nom de domaine. Vous devez toocreate un locataire B2C avec un nom de domaine différent.
>
>

## <a name="link-your-tenant-tooyour-subscription"></a>Lier votre abonnement de tooyour client

Vous devez toolink votre B2C de AD Azure locataire tooyour abonnement Azure tooenable toutes les fonctionnalités B2C et payer des frais d’utilisation. toolearn plus, lisez [cet article](active-directory-b2c-how-to-enable-billing.md). Si vous ne liez pas votre tooyour de locataire Azure AD B2C abonnement Azure, certaines fonctionnalités sont bloquée et, vous voyez un message d’avertissement (« aucun abonnement liés toothis B2C locataire ou hello abonnement ne nécessite votre attention. ») dans les paramètres de hello B2C. Il est important d’effectuer cette étape avant de passer vos applications en production.

## <a name="easy-access-toosettings"></a>Un accès facile toosettings

[!INCLUDE [active-directory-b2c-find-service-settings](../../includes/active-directory-b2c-find-service-settings.md)]

Vous pouvez également accéder à panneau de hello en entrant `Azure AD B2C` dans **recherche les ressources** haut hello du portail de hello. Dans la liste des résultats hello, sélectionnez **Azure AD B2C** tooaccess hello Panneau de paramètres B2C.

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Azure Active Directory B2C : inscription de votre application](active-directory-b2c-app-registration.md)
