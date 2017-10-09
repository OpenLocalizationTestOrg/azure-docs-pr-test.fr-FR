---
title: "Authentification d’utilisateur final : Data Lake Store à l’aide d’Azure Active Directory | Microsoft Docs"
description: "Découvrez comment l’authentification de l’utilisateur final de tooachieve avec Data Lake Store à l’aide d’Azure Active Directory"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ec586ecd-1b42-459e-b600-fadbb7b80a9b
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: fd58f4f2d8fc915b8bc51d9e5b040d2cee34047e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="end-user-authentication-with-data-lake-store-using-azure-active-directory"></a>Authentification d’utilisateur final auprès de Data Lake Store à l’aide d’Azure Active Directory
> [!div class="op_single_selector"]
> * [Authentification de service à service](data-lake-store-authenticate-using-active-directory.md)
> * [Authentification de l’utilisateur final](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

Azure Data Lake Store utilise Azure Active Directory pour l’authentification. Avant la création d’une application qui fonctionne avec Azure Data Lake Store ou Analytique de LAC de données Azure, vous devez d’abord déterminer comment vous voulez tooauthenticate votre application avec Azure Active Directory (Azure AD). Hello deux options disponibles sont :

* Authentification de l’utilisateur final (cet article)
* Authentification de service à service

Ces deux options entraîner dans votre application qui est fournie avec un jeton OAuth 2.0, qui obtient tooeach attaché demande faite tooAzure Data Lake Store ou Analytique de LAC de données Azure.

Cet article traite de la création d’une **application native Azure AD pour l’authentification de l’utilisateur final**. Pour obtenir des instructions sur la configuration de l’application Azure AD pour l’authentification de service à service, voir [Authentification de service à service avec Data Lake Store à l’aide d’Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).

## <a name="prerequisites"></a>Composants requis
* Un abonnement Azure. Consultez [Obtenir une version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).

* Votre ID d’abonnement. Vous pouvez le récupérer à partir de hello portail Azure. Par exemple, il est disponible à partir du Panneau de compte Data Lake Store hello.
  
    ![Obtenir l’ID d’abonnement](./media/data-lake-store-end-user-authenticate-using-active-directory/get-subscription-id.png)

* Votre nom de domaine Azure AD. Vous pouvez le récupérer par pointage de souris hello en hello en haut à droite de hello portail Azure. À partir de la capture d’écran de hello ci-dessous, nom de domaine hello est **contoso.onmicrosoft.com**, et hello GUID entre crochets est l’ID de client hello. 
  
    ![Obtenir le domaine AAD](./media/data-lake-store-end-user-authenticate-using-active-directory/get-aad-domain.png)

## <a name="end-user-authentication"></a>Authentification de l’utilisateur final
Il s’agit de hello approche recommandée si vous souhaitez une toolog par l’utilisateur dans l’application tooyour via Azure AD. Votre application peut être en mesure de tooaccess ressources Windows Azure avec hello même niveau d’accès en tant qu’utilisateur final hello qui connecté. Vos utilisateurs finaux devez tooprovide leurs informations d’identification régulièrement dans l’ordre pour votre application l’accès toomaintain.

résultat de Hello d’avoir à l’utilisateur final hello connectez-vous est que votre application reçoit un jeton d’accès et un jeton d’actualisation. jeton d’accès Hello obtient demande attaché tooeach tooData Lake Store ou Analytique lac de données, et il n’est valide pendant une heure par défaut. jeton d’actualisation Hello peut être utilisé tooobtain un nouveau jeton d’accès et il n’est valide pour les semaines tootwo par défaut, si utiliser régulièrement. Vous pouvez utiliser deux approches différentes pour la connexion de l’utilisateur final.

### <a name="using-hello-oauth-20-pop-up"></a>À l’aide de la fenêtre contextuelle de hello OAuth 2.0
Votre application peut déclencher une fenêtre de d’autorisation OAuth 2.0, les Bonjour par l’utilisateur peut entrer leurs informations d’identification. Cette fenêtre contextuelle fonctionne également avec les processus d’authentification à deux facteurs Azure AD (2FA) hello, si nécessaire. 

> [!NOTE]
> Cette méthode n’est pas encore prise en charge dans la bibliothèque d’authentification Azure AD (ADAL) de hello pour Python ou Java.
> 
> 

### <a name="directly-passing-in-user-credentials"></a>Transmission directe des informations d’identification de l’utilisateur
Votre application peut fournir directement tooAzure des informations d’identification utilisateur Active Directory. Cette méthode fonctionne uniquement avec les comptes d’utilisateur dotés d’ID d’organisation. Elle n’est pas compatible avec les comptes d’utilisateur personnels ou « live ID », notamment ceux se terminant par @outlook.com ou @live.com. En outre, cette méthode n’est pas compatible avec les comptes d’utilisateur qui nécessitent l’authentification à 2 facteurs Azure AD (TFA).

### <a name="what-do-i-need-toouse-this-approach"></a>Comment dois-je toouse cette approche ?
* Votre nom de domaine Azure AD. Cette figure déjà dans la condition préalable de hello de cet article.
* Application native **Azure AD**
* ID d’application pour l’application native de hello Azure AD
* URI de redirection de hello application native d’Azure AD
* Définir des autorisations déléguées


## <a name="step-1-create-an-active-directory-native-application"></a>Étape 1 : Créer une application native Active Directory

Créez et configurez une application native Azure AD pour l’authentification de l’utilisateur final auprès d’Azure Data Lake Store à l’aide d’Azure Active Directory. Pour obtenir des instructions, consultez la page [Créer une application Azure AD](../azure-resource-manager/resource-group-create-service-principal-portal.md).

Tout en suivant les instructions de hello en hello au-dessus de lien, veillez à sélectionner **natif** pour le type d’application, comme indiqué dans la capture d’écran hello ci-dessous.

![Créer une application web](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Créer une application native")

## <a name="step-2-get-application-id-and-redirect-uri"></a>Étape 2 : Obtenir l’ID et l’URI de redirection de l’application

Consultez [obtenir l’ID de l’application hello](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) tooretrieve hello id d’application (également appelé ID de client hello Bonjour portail Azure classic) d’application native de hello Azure AD.

tooretrieve hello URI de redirection, suivez les étapes de hello ci-dessous.

1. À partir de hello portail Azure, sélectionnez **Azure Active Directory**, cliquez sur **inscriptions d’application**, recherchez et cliquez sur application native hello Azure AD que vous venez de créer.

2. À partir de hello **paramètres** panneau pour l’application hello, cliquez sur **URI de redirection**.

    ![Obtenir un URI de redirection](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-redirect-uri.png)

3. Copiez la valeur hello affichée.


## <a name="step-3-set-permissions"></a>Étape 3 : Définir des autorisations

1. À partir de hello portail Azure, sélectionnez **Azure Active Directory**, cliquez sur **inscriptions d’application**, recherchez et cliquez sur application native hello Azure AD que vous venez de créer.

2. À partir de hello **paramètres** panneau pour l’application hello, cliquez sur **autorisations requises**, puis cliquez sur **ajouter**.

    ![ID CLIENT](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-1.png)

3. Bonjour **ajouter l’accès aux API** panneau, cliquez sur **sélectionner une API**, cliquez sur **Azure Data Lake**, puis cliquez sur **sélectionnez**.

    ![ID CLIENT](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-2.png)
 
4.  Bonjour **ajouter l’accès aux API** panneau, cliquez sur **sélectionner les autorisations**, sélectionnez hello case à cocher toogive **accès total tooData Lake Store**, puis cliquez sur **sélectionner** .

    ![ID CLIENT](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-3.png)

    Cliquez sur **Done**.

5. Répétition hello dernières étapes de deux autorisations toogrant pour **API de gestion Windows Azure** également.
   
## <a name="next-steps"></a>Étapes suivantes
Dans cet article vous créé une application native d’Azure AD et collecté les informations de hello que vous avez besoin dans vos applications clientes que vous créez à l’aide du Kit de développement .NET, Java SDK, les API REST, etc.. Vous pouvez maintenant toohello suivant des articles de parler de la façon dont toouse hello AD Azure web application toofirst s’authentifient avec Data Lake Store et autres opérations sur le magasin de hello.

* [Prise en main d'Azure Data Lake Store avec le Kit de développement logiciel (SDK) .NET](data-lake-store-get-started-net-sdk.md)
* [Prise en main d’Azure Data Lake Store à l’aide du Kit de développement logiciel (SDK) Java](data-lake-store-get-started-java-sdk.md)
* [Prise en main d’Azure Data Lake Store à l’aide de l’API REST](data-lake-store-get-started-rest-api.md)

