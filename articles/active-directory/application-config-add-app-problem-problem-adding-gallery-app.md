---
title: "aaaProblem Ajout d’une application Azure AD galerie | Documents Microsoft"
description: "Comprendre le cadran de personnes hello courantes des problèmes lors de l’ajout d’applications de la galerie d’Azure AD et que vous pouvez faire tooresolve les"
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
ms.openlocfilehash: 654f98116176d5590563c0471b92809f8763fbd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-adding-an-azure-ad-gallery-application"></a>Problème lors de l’ajout d’une application de la galerie Azure AD

Cet article vous a-t-il face de personnes toounderstand hello courantes des problèmes lors de l’ajout d’applications de la galerie d’Azure AD et que vous pouvez faire tooresolve les.

## <a name="i-clicked-hello-add-button-and-my-application-took-a-long-time-tooappear"></a>J’ai cliqué sur hello « ajouter » bouton et mon application a eu un tooappear beaucoup de temps

Dans certaines circonstances, il peut prendre 1 à 2 minutes (et parfois plus) pour un tooappear application après l’avoir ajoutée tooyour active. Bien que cela ne soit pas performances normales hello, vous pouvez voir l’ajout d’application hello est en cours d’exécution en cliquant sur hello **Notifications** icône (clochette hello) dans hello coin supérieur droit hello [Azure Portal](https://portal.azure.com/)et en recherchant un **en cours** ou **terminé** notification étiquetée **créer l’application.**

Si votre application n’est jamais ajoutée, ou si vous rencontrez une erreur lorsque vous cliquez hello **ajouter** bouton, vous verrez un **Notification** dans un **erreur** état. Si vous souhaitez plus d’informations sur les toolearn d’erreur hello tooor plus partager avec un engingeer de prise en charge, vous pouvez voir plus d’informations sur l’erreur de hello en suivant les étapes de hello Bonjour [comment toosee les détails de hello d’une notification de portail](#how-to-see-the-details-of-a-portal-notification) section.

## <a name="i-clicked-hello-add-button-and-my-application-didnt-appear"></a>J’ai cliqué sur le bouton « Ajouter » de hello et mon application n’est pas apparu

Parfois, en raison de problèmes de tootransient, des problèmes réseau ou un bogue, ajout d’un échec de l’application. Vous pouvez indiquer cela se produit lorsque vous cliquez sur hello **Notifications** icône (clochette hello) dans hello coin supérieur droit de hello portail Azure et que vous consultez une croix rouge ( !) tooyour suivant d’icône **créer application** notification. Cela indique une erreur est survenue lors de la création d’application hello.

Si vous rencontrez une erreur lorsque vous cliquez hello **ajouter** bouton, vous verrez un **Notification** dans un **erreur** état. Si vous souhaitez plus d’informations sur les toolearn d’erreur hello tooor plus partager avec un engingeer de prise en charge, vous pouvez voir plus d’informations sur l’erreur de hello en suivant les étapes de hello Bonjour [comment toosee les détails de hello d’une notification de portail](#how-to-see-the-details-of-a-portal-notification) section.

 ## <a name="i-dont-know-how-tooset-up-my-application-once-ive-added-it"></a>Je ne sais pas comment tooset mon application une fois j’ai ajouté il

Si vous avez besoin d’aide à en savoir plus sur les applications, hello [liste de didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list) l’article est un bon point toostart.

En outre toothis, hello [Azure bibliothèque de documents des Applications AD](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) vous aider à toolearn en savoir plus sur l’authentification unique sur auprès d’Azure AD et comment il fonctionne.

## <a name="how-toosee-hello-details-of-a-portal-notification"></a>Comment toosee les détails de hello d’une notification de portail

Vous pouvez voir les détails de hello toute notification portail en suivant les étapes de hello ci-dessous :

1.  Cliquez sur hello **Notifications** icône (clochette hello) dans hello coin supérieur droit de hello portail Azure

2.  Sélectionnez une notification dans un **erreur** état (celles avec un toothem suivant rouge ( !)).

    >[!NOTE]
    >Vous ne pouvez pas cliquer sur les notifications affichant l’état **Réussi** ou **En cours**.
    >
    >

3.  Cette hello ouvrir **détails de la Notification** panneau.

4.  Utilisez ces informations vous-même toounderstand plus des détails sur le problème de hello.

5.  Si vous avez toujours besoin d’aide, vous pouvez également partager ces informations avec une prise en charge ingénieur ou hello groupe tooget aide produit avec votre problème.

6.  Cliquez sur hello **copie** **icône** toohello à droite de hello **copiez erreur** toocopy de zone de texte tous les hello tooshare détails de notification avec un ingénieur du groupe de support ou de produit

## <a name="how-tooget-help-by-sending-notification-details-tooa-support-engineer"></a>Comment tooget aider en envoyant l’ingénieur du support de notification détails tooa

Il est très important que vous partagez **tous hello détails ci-dessous** avec un ingénieur du support, si vous avez besoin d’aide, afin qu’ils peuvent vous aider à rapidement. Vous pouvez facilement en cela **prendre une capture d’écran,** ou en cliquant sur hello **icône d’erreur de copie**, trouvé toohello Hello **erreur de copie** zone de texte.

## <a name="notification-details-explained"></a>Explication des détails de la notification

Hello ci-dessous explique plus la fonction de chacun des éléments de notification hello et donne des exemples de chacun d’eux.

### <a name="essential-notification-items"></a>Éléments essentiels de la notification

-   **Titre** : hello titre descriptif de la notification de hello

  * Exemple : **Paramètres de proxy d’application**

-   **Description** – hello description de ce qui s’est produite en raison de l’opération de hello

    -   Exemple : **L’URL interne entrée est déjà utilisée par une autre application**

-   **Id de notification** – id unique de hello de notification de hello

    -   Exemple : **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**

-   **Id de demande client** – id de demande spécifique hello effectuée par votre navigateur

    -   Exemple : **302fd775-3329-4670-a9f3-bea37004f0bc**

-   **Heure UTC de marqueur** – hello horodatage au cours de laquelle hello notification s’est produite, en heure UTC

    -   Exemple : **2017-03-23T19:50:43.7583681Z**

-   **Id de Transaction interne** – hello ID interne, nous pouvons utiliser des erreurs de hello toolook dans nos systèmes

    -   Exemple : **71a2f329-ca29-402f-aa72-bc00a7aca603**

-   **UPN** – utilisateur hello qui a effectué l’opération de hello

    -   Exemple : **tperkins@f128.info**

-   **Id de locataire** – ID unique de hello du client, hello dont hello utilisateur qui a effectué l’opération de hello était membre

    -   Exemple : **7918d4b5-0442-4a97-be2d-36f9f9962ece**

-   **L’Id d’objet utilisateur** – hello ID unique de l’utilisateur hello qui a effectué l’opération de hello

    -   Exemple : **17f84be4-51f8-483a-b533-383791227a99**

### <a name="detailed-notification-items"></a>Éléments détaillés de la notification

-   **Nom d’affichage** – **(peut être vide)** un nom d’affichage plus détaillé pour l’erreur de hello

    -   Exemple : **Paramètres de proxy d’application**

-   **État** – hello état spécifique de la notification de hello

    -   Exemple : **Échec**

-   **Id d’objet** – **(peut être vide)** hello ID d’objet sur le hello opération a été effectuée

    -   Exemple : **8e08161d-f2fd-40ad-a34a-a9632d6bb599**

-   **Détails** – hello description détaillée de ce qui s’est produite en raison de l’opération de hello

    -   Exemple : **l’URL interne 'http://bing.com/' n’est pas valide car elle est déjà en cours d’utilisation**

-   **Erreur de copie** – cliquez sur hello **icône de copie** toohello à droite de hello **copiez erreur** toocopy de zone de texte tous les hello tooshare détails de notification avec un ingénieur du groupe de support ou de produit

    -   Exemple ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```

## <a name="next-steps"></a>Étapes suivantes
[Gestion des applications avec Azure Active Directory](active-directory-enable-sso-scenario.md)
