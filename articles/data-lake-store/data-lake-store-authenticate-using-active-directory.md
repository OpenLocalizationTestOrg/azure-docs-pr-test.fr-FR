---
title: "Authentification de service à service : Data Lake Store à l’aide d’Azure Active Directory | Microsoft Docs"
description: "Découvrez comment l’authentification de service tooachieve avec Data Lake Store à l’aide d’Azure Active Directory"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 820b7c5d-4863-4225-9bd1-df4d8f515537
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: 2e56237a75f020067b3248a1e1cfaf3c8df1371c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-to-service-authentication-with-data-lake-store-using-azure-active-directory"></a>Authentification de service à service auprès de Data Lake Store à l’aide d’Azure Active Directory
> [!div class="op_single_selector"]
> * [Authentification de service à service](data-lake-store-authenticate-using-active-directory.md)
> * [Authentification de l’utilisateur final](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

Azure Data Lake Store utilise Azure Active Directory pour l’authentification. Avant la création d’une application qui fonctionne avec Azure Data Lake Store ou Analytique de LAC de données Azure, vous devez d’abord déterminer comment vous voulez tooauthenticate votre application avec Azure Active Directory (Azure AD). Hello deux options disponibles sont :

* Authentification de l’utilisateur final 
* Authentification de service à service (cet article) 

Ces deux options entraîner dans votre application qui est fournie avec un jeton OAuth 2.0, qui obtient tooeach attaché demande faite tooAzure Data Lake Store ou Analytique de LAC de données Azure.

Cet article traite de la création d’une **application web Azure AD pour l’authentification de service à service**. Pour obtenir des instructions sur la configuration de l’application Azure AD pour l’authentification de l’utilisateur final, consultez [Authentification d’utilisateur final auprès de Data Lake Store à l’aide d’Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).

## <a name="prerequisites"></a>Conditions préalables
* Un abonnement Azure. Consultez la rubrique [Obtenir une version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="step-1-create-an-active-directory-web-application"></a>Étape 1 : Créer une application web Active Directory

Créez et configurez une application web Azure AD pour l’authentification de service à service auprès d’Azure Data Lake Store à l’aide d’Azure Active Directory. Pour obtenir des instructions, consultez la page [Créer une application Azure AD](../azure-resource-manager/resource-group-create-service-principal-portal.md).

Tout en suivant les instructions de hello en hello au-dessus de lien, veillez à sélectionner **application Web / API** pour le type d’application, comme indiqué dans la capture d’écran hello ci-dessous.

![Créer une application web](./media/data-lake-store-authenticate-using-active-directory/azure-active-directory-create-web-app.png "Créer une application web")

## <a name="step-2-get-application-id-authentication-key-and-tenant-id"></a>Étape 2 : obtenir un ID d’application, une clé d’authentification et un ID de locataire
Lors de la connexion par programme, vous devez les id hello pour votre application. Si l’application hello s’exécute sous ses propres informations d’identification, vous devez également une clé d’authentification.

* Pour obtenir des instructions sur la façon dont tooretrieve ID de l’application hello et l’authentification de clé (également appelée hello question secrète du client) pour votre application, consultez [clé ID et l’authentification d’application Get](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key).

* Pour savoir comment tooretrieve hello ID client, consultez [obtenir l’ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).

## <a name="step-3-assign-hello-azure-ad-application-toohello-azure-data-lake-store-account-file-or-folder-only-for-service-to-service-authentication"></a>Étape 3 : Assigner hello Azure application toohello Azure Data Lake Store compte fichier ou dossier (uniquement pour l’authentification de service)
1. Ouverture de session toohello nouvelle [portail Azure](https://portal.azure.com) et ouvrir un compte d’Azure Data Lake Store hello que vous souhaitez tooassociate avec hello application Azure Active Directory que vous avez créé précédemment.
2. Dans le panneau de votre compte Data Lake Store, cliquez sur **Explorateur de données**.
   
    ![Créer des répertoires dans un compte Data Lake Store](./media/data-lake-store-authenticate-using-active-directory/adl.start.data.explorer.png "Créer des répertoires dans un compte Data Lake Store")
3. Bonjour **Explorateur de données** panneau, cliquez sur le fichier de hello ou un dossier pour lequel vous souhaitez tooprovide accès toohello AD Azure application, puis cliquez sur **accès**. fichier de tooa tooconfigure access, vous devez cliquer sur **accès** de hello **l’aperçu du fichier** panneau.
   
    ![Définir des ACL sur le système de fichiers Data Lake](./media/data-lake-store-authenticate-using-active-directory/adl.acl.1.png "Définir des ACL sur le système de fichiers Data Lake")
4. Hello **accès** panneau répertorie les accès standard hello et accès personnalisé déjà affecté toohello racine. Cliquez sur hello **ajouter** icône tooadd personnalisée au niveau du ACL.
   
    ![Lister les accès standard et personnalisés](./media/data-lake-store-authenticate-using-active-directory/adl.acl.2.png "Lister les accès standard et personnalisés")
5. Cliquez sur hello **ajouter** hello de tooopen icône **ajouter un accès personnalisé à** panneau. Dans ce panneau, cliquez sur **sélectionner utilisateur ou groupe**, puis dans **sélectionner utilisateur ou groupe** panneau, recherchez l’application Azure Active Directory de hello vous avez créé précédemment. Si vous avez un grand nombre de toosearch de groupes à partir de, utilisez la zone de texte de hello à toofilter supérieur de hello sur le nom du groupe hello. Cliquez sur le groupe hello tooadd et puis cliquez sur **sélectionnez**.
   
    ![Ajouter un groupe](./media/data-lake-store-authenticate-using-active-directory/adl.acl.3.png "Ajouter un groupe")
6. Cliquez sur **autorisations Select**, sélectionnez les autorisations hello et si vous souhaitez définir des autorisations hello tooassign comme une ACL par défaut, accès ACL, ou les deux. Cliquez sur **OK**.
   
    ![Affecter des autorisations toogroup](./media/data-lake-store-authenticate-using-active-directory/adl.acl.4.png "affecter des autorisations toogroup")
   
    Pour plus d’informations sur les autorisations dans Data Lake Store et sur les ACL par défaut ou d’accès, consultez [Contrôle d’accès dans Azure Data Lake Store](data-lake-store-access-control.md).
7. Bonjour **ajouter un accès personnalisé à** panneau, cliquez sur **OK**. Hello récemment ajouté de groupe, avec des autorisations hello associée, est maintenant listée dans hello **accès** panneau.
   
    ![Affecter des autorisations toogroup](./media/data-lake-store-authenticate-using-active-directory/adl.acl.5.png "affecter des autorisations toogroup")

## <a name="step-4-get-hello-oauth-20-token-endpoint-only-for-java-based-applications"></a>Étape 4 : Obtenir le point de terminaison token hello OAuth 2.0 (uniquement pour les applications Java)

1. Ouverture de session toohello nouvelle [portail Azure](https://portal.azure.com) et cliquez sur Active Directory à partir du volet de gauche hello.

2. Dans le volet gauche de hello, cliquez sur **inscriptions d’application**.

3. À partir du haut de hello du panneau des enregistrements de l’application hello, cliquez sur **points de terminaison**.

    ![Point de terminaison de jeton OAuth](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint.png "Point de terminaison de jeton OAuth")

4. À partir de la liste hello de points de terminaison, copiez le point de terminaison token hello OAuth 2.0.

    ![Point de terminaison de jeton OAuth](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint-1.png "Point de terminaison de jeton OAuth")   

## <a name="next-steps"></a>Étapes suivantes
Dans cet article vous créé une application web de Azure AD et collecté les informations de hello dans vos applications clientes, vous devez créer à l’aide du Kit de développement .NET, Java SDK, etc.. Vous pouvez maintenant toohello suivant des articles de parler de la façon dont toouse hello AD Azure web application toofirst s’authentifient avec Data Lake Store et autres opérations sur le magasin de hello.

* [Prise en main d'Azure Data Lake Store avec le Kit de développement logiciel (SDK) .NET](data-lake-store-get-started-net-sdk.md)
* [Prise en main d’Azure Data Lake Store à l’aide du Kit de développement logiciel (SDK) Java](data-lake-store-get-started-java-sdk.md)

Cet article vous a présenté via tooget nécessaires des étapes de base de hello un utilisateur principal haut et en cours d’exécution pour votre application. Vous pouvez examiner hello informations supplémentaires de tooget articles suivantes :
* [Utiliser PowerShell toocreate service principal](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [Utiliser l’authentification de certificat pour l’authentification du principal du service](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authenticate-service-principal#create-service-principal-with-certificate)
* [Autres tooAzure tooauthenticate de méthodes AD](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-authentication-scenarios)


