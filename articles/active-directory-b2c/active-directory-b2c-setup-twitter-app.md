---
title: "Azure Active Directory B2C : configuration Twitter | Microsoft Docs"
description: "Fournir tooconsumers d’inscription et de connexion à des comptes de Twitter dans vos applications qui sont sécurisées par Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 579a6841-9329-45b8-a351-da4315a6634e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/06/2017
ms.author: parakhj
ms.openlocfilehash: 275c5c73fd5e8e5075e77fee942cbc1b5e1586cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-twitter-accounts"></a>Azure B2C Active Directory : Fournir tooconsumers d’abonnement et connectez-vous avec des comptes de Twitter

> [!NOTE]
> Cette fonctionnalité est en préversion.
> 

## <a name="create-a-twitter-application"></a>Création d'une application Twitter
toouse Twitter comme fournisseur d’identité dans Azure Active Directory (Azure AD) B2C, vous devez toocreate une application Twitter et lui fournir les paramètres appropriés hello. Vous devez cela un toodo de compte de développeur Twitter. Si vous n’en avez pas, vous pouvez en obtenir un à l’adresse [https://dev.twitter.com/](https://dev.twitter.com/).

1. Accédez toohello [Twitter le site Web des développeurs](https://dev.twitter.com/) et connectez-vous avec vos informations d’identification.
2. Cliquez sur **My apps** (Mes applications sous **Tools & Support** (Outils et support), puis sur **Create New App** (Créer une application). 
3. Dans le formulaire de hello, fournissez une valeur pour hello **nom**, **Description**, et **site Web**.
4. Pourquoi **URL de rappel**, entrez `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`. Assurez-vous que tooreplace **{tenant}** avec le nom de votre locataire (par exemple, contosob2c.onmicrosoft.com).
5. Vérifiez hello zone tooagree toohello **contrat du développeur** et cliquez sur **créer votre application Twitter**.
6. Une fois l’application hello est créée, cliquez sur **clés et les jetons d’accès**.
7. Copiez la valeur hello **clé de consommateur** et **Secret de consommateur**. Vous devez les deux tooconfigure Twitter comme fournisseur d’identité dans votre client.

## <a name="configure-twitter-as-an-identity-provider-in-your-tenant"></a>Configurer Twitter en tant que fournisseur d’identité dans votre locataire
1. Suivez ces étapes trop[accédez Panneau de fonctionnalités toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) sur hello portail Azure.
2. Dans le panneau de fonctionnalités hello B2C, cliquez sur **fournisseurs d’identité**.
3. Cliquez sur **+ ajouter** haut hello du Panneau de hello.
4. Fournissez un nom convivial de **nom** pour la configuration du fournisseur d’identité hello. Par exemple, entrez « Twitter ».
5. Cliquez sur **Identity provider type** (Type de fournisseur d’identité), sélectionnez **Twitter**, puis cliquez sur **OK**.
6. Cliquez sur **configurer ce fournisseur d’identité** et entrez hello Twitter **clé de consommateur** pour hello **id Client** et hello Twitter **Secret de consommateur**pour hello **clé secrète Client**.
7. Cliquez sur **OK**, puis cliquez sur **créer** toosave votre configuration Twitter.

