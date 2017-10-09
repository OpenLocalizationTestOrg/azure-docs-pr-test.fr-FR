---
title: "aaaAzure AD vue d’ensemble du protocole .NET | Documents Microsoft"
description: "Comment toouse HTTP messages tooauthorize accéder tooweb applications et API web dans votre client à l’aide d’Azure AD."
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/21/2016
ms.author: priyamo
ms.openlocfilehash: 5bd54af028c445afd3f35d67d47d7c84b476c757
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## Inscrire votre application avec votre client AD
Tout d’abord, vous devez tooregister votre application auprès de votre client Azure Active Directory (Azure AD). Cela sera vous fournir un ID d’Application pour votre application, ainsi que tooreceive jetons l’activer.

* Connectez-vous à toohello [Azure Portal](https://portal.azure.com).
* Choisissez votre locataire Azure AD en cliquant sur votre compte dans hello coin supérieur droit de la page de hello.
* Dans le volet de navigation de gauche hello, cliquez sur **Azure Active Directory**.
* Cliquez sur **Inscriptions des applications**, puis sur **Ajouter**.
* Suivez les invites hello et créez une nouvelle application. Pour ce didacticiel, il peut s’agir d’une application web ou d’une application native. Cependant, si vous souhaitez obtenir des exemples spécifiques pour les applications web ou les applications natives, consultez nos rubriques de [démarrage rapide](../articles/active-directory/develop/active-directory-developers-guide.md).
  * Pour les Applications Web, indiquez hello **URL de connexion** qui est hello les URL de base de votre application, où les utilisateurs peuvent se connecter par exemple `http://localhost:12345`.
<!--TODO: add once App ID URI is configurable: hello **App ID URI** is a unique identifier for your application. hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * Pour les Applications natives, vous devez fournir un **URI de redirection**, de la publicité Azure utilisera les réponses jeton tooreturn. Entrez une application tooyour spécifique de la valeur,. exemple :`http://MyFirstAADApp`
* Une fois que vous avez terminé l’inscription, Azure AD s’attribuer à votre application un identificateur client unique, hello ID d’Application. Vous devez cette valeur dans les sections suivantes hello, par conséquent, copiez-le à partir de la page de l’application hello.
