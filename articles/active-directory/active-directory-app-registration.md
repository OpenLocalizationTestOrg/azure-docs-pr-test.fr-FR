---
title: "aaaAzure inscription d’application Active Directory | Documents Microsoft"
description: "Cet article décrit comment toouse hello tooregister portail Azure, une application avec Azure Active Directory"
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: 7dc7b89f-653f-405a-b5f4-2c1288720c15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: priyamo
ms.reviewer: elisol
ms.openlocfilehash: 0134e299dcc53919a6f789a0878a1cf64a8e244d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="register-your-application-with-your-azure-active-directory-tenant"></a>Inscrire votre application avec un client Azure Active Directory

Vous pouvez utiliser hello tooregister portail Azure à votre application auprès de votre client Azure Active Directory (Azure AD). Cela crée un ID d’Application pour l’application hello et lui permet de jetons de tooreceive.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Choisissez votre locataire Azure AD en sélectionnant votre compte dans hello coin supérieur droit de la page de hello.
3. Dans le volet de navigation gauche hello, choisissez **plus Services**, cliquez sur **inscriptions d’application**, puis cliquez sur **ajouter**.
4. Suivez les invites hello et créez une nouvelle application. Si vous souhaitez des exemples spécifiques pour les applications web ou natives, consultez les [Démarrages rapides](active-directory-developers-guide.md).
  * Pour les Applications Web, indiquez hello **URL de connexion**, qui est hello les URL de base de votre application, où les utilisateurs peuvent se connecter par exemple `http://localhost:12345`.
<!--TODO: add once App ID URI is configurable: hello **App ID URI** is a unique identifier for your application. hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * Pour les Applications natives, vous devez fournir un **URI de redirection**, quels Azure AD utilise des réponses de jeton tooreturn. Entrez une application tooyour spécifique de la valeur,. exemple :`http://MyFirstAADApp`
5. Une fois que vous avez terminé l’inscription, Azure AD assigne à votre application un identificateur client unique, hello ID d’Application.

## <a name="update-application-settings-from-hello-azure-portal"></a>Mettre à jour les paramètres de l’application à partir de hello portail Azure

Vous pouvez facilement modifier les paramètres d’une application existante à l’aide de hello portail Azure. Par exemple, vous voudrez tooconfigure une URL de réponse, c'est-à-dire où Azure AD émet des réponses de jeton. Vous pouvez également tooconfigure autorisations tooother applications, pour l’instance tooallow tooaccess de votre application hello Microsoft Graph API. Vous pouvez faire tout cela via la page de paramètres d’application hello.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Choisissez votre locataire Azure AD en sélectionnant votre compte dans hello coin supérieur droit de la page de hello.
3. Dans le volet de navigation gauche hello, choisissez **plus Services**, cliquez sur **inscriptions d’application**, choisissez votre application à partir de la liste de hello.
4. Cliquez sur **paramètres** tooopen page de paramètres hello pour une application hello.
  * Hello **propriétés** page vous permet de modifier les informations générales hello pour une application hello. Cela inclut le nom de l’application hello, URL de connexion hello et URL de déconnexion hello.
  * Hello **URL de réponse** page vous permet de tooadd une URL de réponse, c'est-à-dire où Azure AD envoie des réponses de jeton.
  * Hello **propriétaires** page vous permet de propriétaires d’applications tooadd.
  * Hello **autorisations** page vous permet de tooconfigure les autorisations pour l’application hello. Par exemple, tooaccess hello Microsoft Graph API, cliquez sur **ajouter** et sélectionnez **Microsoft Graph** dans le sélecteur de hello API, puis choisissez autorisation hello requise, par exemple **données d’annuaire en lecture** .
  * Hello **clés** page vous permet de secrets d’application tooadd. Hello secret s’affiche uniquement une fois immédiatement après sa création, vous devez donc vous assurer toocopy pour une utilisation ultérieure.

## <a name="use-hello-inline-manifest-editor"></a>Utilisez l’éditeur de manifeste hello inline

Vous pouvez utiliser toomodify éditeur de manifeste inline du hello certaines propriétés ne sont pas exposées directement dans l’application hello portail Azure. Par exemple, vous pouvez l’utiliser dans URI l’application toomodify hello ID d’application ou tooenable hello OAuth2.0 le flux implicit au lieu d’autorisation par défaut de hello accorder le flux de code.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Choisissez votre locataire Azure AD en sélectionnant votre compte dans hello coin supérieur droit de la page de hello.
3. Dans le volet de navigation gauche hello, choisissez **plus Services**, cliquez sur **inscriptions d’application**, choisissez votre application à partir de la liste de hello.
4. Cliquez sur **manifeste** de hello application page tooopen hello manifeste éditeur inline.
5. Vous pouvez apporter directement les modifications toohello manifeste et l’enregistrer quand vous êtes prêt. Vous pouvez également télécharger tooopen de manifeste hello dans votre hello Favoris de l’éditeur et le téléchargement mis à jour le manifeste.

## <a name="next-steps"></a>Étapes suivantes

1. Extraire hello [Démarrages rapides](active-directory-developers-guide.md) pour les procédures pas à pas détaillé des applications d’exécution de l’authentification à l’aide d’Azure AD.
2. Consultez notre liste complète d’exemples de code dans [GitHub](https://github.com/azure-samples).
