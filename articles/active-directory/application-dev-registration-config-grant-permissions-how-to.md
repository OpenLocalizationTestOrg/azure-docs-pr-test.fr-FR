---
title: "applications personnalisées aaaHow toogrant autorisations tooa | Documents Microsoft"
description: "Comment toogrant autorisations tooyour personnalisées à l’aide de l’application hello portail Azure AD ou un paramètre d’URL"
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
ms.openlocfilehash: e43a105fff60fbf912bdf4f60260f86ee289328d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogrant-permissions-tooa-custom-developed-application"></a>Comment toogrant autorisations tooa personnalisées application

Si vous souhaitez toogrant consentement de manière préemptive sur votre application ou que vous rencontrez une erreur que vous n’avez pas accepté tooan application, essayez les étapes suivantes ci-dessous.

## <a name="how-tooperform-admin-consent-for-your-application"></a>Comment tooperform consentement de l’administrateur de votre application

Cela influe hello d’octroi d’application toohello de consentement pour tous les utilisateurs de votre organisation.

1. Accédez toohello **inscriptions d’application** panneau comme un **administrateur global**, puis sélectionnez application hello.

2. Sélectionnez **autorisations requises**et enfin cliquez sur hello **accorder des autorisations** bouton en haut de hello du panneau des hello.

Ou bien, vous pouvez construire une demande trop*login.microsoftonline.com* avec votre application des configurations et ajoutera *& invite = admin\_consentement*. Après la connexion avec informations d’identification d’administrateur, application hello a reçu un consentement pour tous les utilisateurs.

## <a name="how-tooforce-user-consent-for-your-application"></a>Comment tooforce le consentement de l’utilisateur pour votre application

* Ajouter sur les demandes d’authentification *& invite = consentement* qui nécessitent des utilisateurs finaux tooconsent chaque fois qu’ils s’authentifient.

## <a name="next-steps"></a>Étapes suivantes

[Intégration des applications et consentement tooAzureAD](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications)

[Consentement et octroi d’autorisations pour les applications convergées Azure AD v2.0](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-scopes)<br>

[AzureAD StackOverflow](http://stackoverflow.com/questions/tagged/azure-active-directory)
