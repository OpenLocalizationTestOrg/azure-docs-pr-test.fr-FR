---
title: "toofill aaaHow les champs spécifiques pour une application personnalisée | Documents Microsoft"
description: "Des conseils sur la manière dont les champs toofill out spécifiques lorsque vous inscrivez une application personnalisée avec Azure AD"
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
ms.openlocfilehash: 7e07bc45c58542edb3863db5aad7c845f1a1772e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofill-out-specific-fields-for-a-custom-developed-application"></a>Comment toofill les champs spécifiques pour une application personnalisée

Cet article vous donner une brève description de tous les champs disponibles hello dans le formulaire de l’inscription d’application hello hello [portail Azure](https://portal.azure.com).

## <a name="register-a-new-application"></a>Inscrire une nouvelle application

-   tooregister une nouvelle application, accédez à toohello [portail Azure](https://portal.azure.com).

-   Dans le volet de navigation gauche hello, cliquez sur **Azure Active Directory.**

-   Choisissez **Inscriptions des applications**, puis cliquez sur **Ajouter**.

-   Ouvrez le formulaire de l’inscription d’application hello.

## <a name="fields-in-hello-application-registration-form"></a>Champs de formulaire d’inscription application hello


| Champ            | Description                                                                              |
|------------------|------------------------------------------------------------------------------------------|
| Nom             | nom Hello de l’application hello. Il doit être composé de quatre caractères minimum.                |
| Type d’application | **Application/API web** : une application qui représente une application web, une API web, ou les deux. 
| |**Natif** : une application qui peut être installée sur l'appareil ou l'ordinateur d'un utilisateur           |
| URL de connexion      | URL de Hello où les utilisateurs peuvent signer dans toouse, votre application                                  |

Une fois que vous avez rempli hello au-dessus des champs, application hello enregistrés dans hello portail Azure, et vous être redirigé toohello page d’application. Hello **paramètres** bouton dans le volet de l’application hello s’ouvre, page Paramètres de hello, qui comporte plus de champs pour vous toocustomize, votre application. tableau Hello ci-dessous décrit tous les champs hello dans la page des paramètres hello. Notez que vous voyez uniquement un sous-ensemble de ces champs, selon que vous avez créez une application web ou une application native.

| Champ           | Description                                                                                                                                                                                                                                                                                                     |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ID de l'application  | Lorsque vous inscrivez une application, Azure AD attribue un ID d’application à votre application. ID de l’application Hello peut servir toouniquely identifier votre application dans tooAzure de demandes d’authentification Active Directory, ainsi que des ressources tooaccess comme hello API Graph.                                                          |
| URI ID d’application      | Cela doit être un URI unique, généralement d’écran de hello **https://&lt;client\_nom&gt;/&lt;application\_nom&gt;.** Il est utilisé pendant le flux d’octroi d’autorisation de hello, comme une ressource de hello toospecify identificateur unique quel jeton hello doit être émis pour. Il devient également la revendication hello 'aud' dans le jeton d’accès hello émis. |
| Charger un nouveau logo | Vous pouvez utiliser cette tooupload un logo pour votre application. logo de Hello doit être au format .bmp, .jpg ou .png et hello la taille doit être inférieure à 100 Ko. dimensions Hello pour l’image de hello doivent être 215 x 215 pixels, avec les dimensions de l’image centrale de 94 x 94 pixels.                                                       |
| URL de la page d’accueil   | Il s’agit de hello URL d’authentification spécifié lors de l’inscription d’application.                                                                                                                                                                                                                                              |
| URL de déconnexion      | Cette URL de déconnexion de déconnexion unique hello. Azure AD envoie une URL de toothis de demande de fermeture de session utilisateur de hello efface leur session avec Azure AD à l’aide de toute autre application inscrite.                                                                                                                                       |
| Mutualisé  | Ce paramètre spécifie si l’application hello peut être utilisée par plusieurs clients. En règle générale, cela signifie que les organisations externes puissent utiliser votre application en inscrivant dans leur locataire et en accordant des données de l’organisation accès tootheir.                                                                   |
| URL de réponse      | URL de réponse Hello sont des points de terminaison hello où Azure AD renvoyer des jetons qui demande de votre application.                                                                                                                                                                                                          |
| URI de redirection   | Pour les applications natives, il s’agit où l’utilisateur de hello être envoyé toofollowing des autorisation réussie. Vérification Active Directory Azure qui hello rediriger URI fournitures de votre application Bonjour OAuth 2.0 demande correspond à l’une des valeurs hello inscrit dans le portail de hello.                                                            |
| Clés            | Vous pouvez créer des clés tooprogrammatically Web access web API sécurisé par Azure AD sans intervention de l’utilisateur. À partir de hello \* \*clés\* \* page, entrez une date d’expiration hello et description clée et enregistrer la clé de hello toogenerate. Assurez-vous que toosave il sécuriser quelque part, car vous ne serez pas en mesure de tooaccess plus tard.             |

## <a name="next-steps"></a>Étapes suivantes
[Gestion des applications avec Azure Active Directory](active-directory-enable-sso-scenario.md)
