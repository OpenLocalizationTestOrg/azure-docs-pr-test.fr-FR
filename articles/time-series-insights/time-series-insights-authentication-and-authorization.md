---
title: "aaaConfigure l’authentification et l’autorisation pour une application personnalisée qui appelle hello Azure temps série Insights API | Documents Microsoft"
description: "Ce didacticiel explique comment tooconfigure l’authentification et l’autorisation pour une application personnalisée qui appelle hello Azure temps série Insights API"
keywords: 
services: time-series-insights
documentationcenter: 
author: dmdenmsft
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/24/2017
ms.author: dmden
ms.openlocfilehash: 5043468bfc2af3c0d27e8602508d92ba2848409e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-for-azure-time-series-insights-api"></a>Authentification et autorisation pour l’API Insights Azure Time Series

Cet article explique comment tooconfigure une application personnalisée qui appelle hello Azure temps série Insights API.

## <a name="service-principal"></a>Principal du service

Cette section explique comment tooconfigure un tooaccess application hello temps série Insights API au nom de l’application hello. application Hello pouvez interroger les données ou publier les données de référence d’environnement d’heure série Insights hello avec les informations d’identification de l’application et les informations d’identification hello utilisateur pas.

Lorsque vous avez une application qui doit tooaccess temps série Insights, vous devez configurer une application Azure Active Directory et affecter des stratégies d’accès données hello dans l’environnement de temps série Insights hello. Cette approche est préférable toorunning hello application vos propres informations d’identification, car :

* Vous pouvez affecter des autorisations identité d’application toohello différents de vos propres autorisations. En règle générale, ces autorisations sont limitée tooexactly quelle application hello doit toodo. Par exemple, vous pouvez autoriser hello application tooonly lire les données dans un environnement de temps série Insights particulier.
* Vous n’avez les informations d’identification de l’application toochange hello si vos responsabilités changent.
* Vous pouvez utiliser un certificat ou une authentification de clé tooautomate application lorsque vous exécutez un script sans assistance.

Cet article explique comment tooperform celles parcourt hello portail Azure. Il se concentre sur une application à locataire unique où application hello est prévue toorun dans une seule organisation. Les applications à client unique sont généralement utilisées pour des applications métier exécutées au sein de votre organisation.

flux de programme d’installation Hello se compose de trois étapes principales :

1. Créer une application dans Azure Active Directory.
2. Autoriser cet environnement de temps série Insights application tooaccess hello.
3. Utiliser les ID de l’application hello et clé tooacquire un jeton toohello `"https://api.timeseries.azure.com/"` audience ou une ressource. jeton de Hello peut ensuite être utilisé toocall hello temps série Insights API.

Voici les étapes détaillées de hello :

1. Bonjour portail Azure, sélectionnez **Azure Active Directory** > **inscriptions d’application** > **nouvelle inscription de l’application**.

   ![Nouvelle inscription d’application dans Azure Active Directory](media/authentication-and-authorization/active-directory-new-application-registration.png)  

2. Permettre à application hello un toobe de type hello nom, sélectionnez **application Web / API**, sélectionnez n’importe quel URI valide pour **URL de connexion**, puis cliquez sur **créer**.

   ![Créer l’application hello dans Azure Active Directory](media/authentication-and-authorization/active-directory-create-web-api-application.png)

3. Sélectionnez votre application nouvellement créée et copiez son éditeur de texte favori application ID tooyour.

   ![Copiez l’ID de l’application hello](media/authentication-and-authorization/active-directory-copy-application-id.png)

4. Sélectionnez **clés**, entrez le nom de clé hello, d’expiration hello sélectionnez, puis cliquez sur **enregistrer**.

   ![sélectionner des clés d’application](media/authentication-and-authorization/active-directory-application-keys.png)

   ![Entrez l’expiration et le nom de la clé hello et cliquez sur Enregistrer](media/authentication-and-authorization/active-directory-application-keys-save.png)

5. Éditeur de texte hello tooyour clé copie.

   ![Copiez la clé de l’application hello](media/authentication-and-authorization/active-directory-copy-application-key.png)

6. Pour un environnement de temps série Insights hello, sélectionnez **des stratégies d’accès données** et cliquez sur **ajouter**.

   ![Ajouter nouveau données accès stratégie toohello temps série Insights environnement](media/authentication-and-authorization/time-series-insights-data-access-policies-add.png)

7. Bonjour **sélectionner un utilisateur** boîte de dialogue, nom de l’application hello Coller (de l’étape 2) ou ID de l’application (à l’étape 3).

   ![Rechercher une application dans la boîte de dialogue Sélectionner un utilisateur hello](media/authentication-and-authorization/time-series-insights-data-access-policies-select-user.png)

8. Rôle de hello Select (**lecteur** pour interroger des données, **collaborateur** pour l’interrogation de données et la modification des données de référence) et cliquez sur **Ok**.

   ![Choisir le lecteur ou contributeur dans la boîte de dialogue Sélectionner un rôle hello](media/authentication-and-authorization/time-series-insights-data-access-policies-select-role.png)

9. Enregistrer la stratégie de hello en cliquant sur **Ok**.

10. Utiliser l’ID d’application hello (à l’étape 3) et jeton de hello application tooacquire clé (à l’étape 5) au nom de l’application hello. Hello jeton peut ensuite être transmis dans hello `Authorization` en-tête lors de l’application hello appelle hello temps série Insights API.

    Si vous utilisez c#, vous pouvez utiliser hello suivant le jeton de hello tooacquire de code pour le compte d’application hello. Pour obtenir un exemple complet, voir [Interroger des données à l’aide de C#](time-series-insights-query-data-csharp.md).

    ```csharp
    var authenticationContext = new AuthenticationContext(
        "https://login.microsoftonline.com/common",
        TokenCache.DefaultShared);

    AuthenticationResult token = await authenticationContext.AcquireTokenAsync(
        // Set hello resource URI toohello Azure Time Series Insights API
        resource: "https://api.timeseries.azure.com/", 
        clientCredential: new ClientCredential(
            // Application ID of application registered in Azure Active Directory
            clientId: "1bc3af48-7e2f-4845-880a-c7649a6470b8", 
            // Application key of hello application that's registered in Azure Active Directory
            clientSecret: "aBcdEffs4XYxoAXzLB1n3R2meNCYdGpIGBc2YC5D6L2="));

    string accessToken = token.AccessToken;
    ```

## <a name="next-steps"></a>Étapes suivantes

Utiliser l’ID de l’application hello et la clé dans votre application. Pour un exemple de code qui appelle hello temps série Insights API, consultez [interroger des données à l’aide de C#](time-series-insights-query-data-csharp.md).

## <a name="see-also"></a>Voir aussi

* [API de requête](/rest/api/time-series-insights/time-series-insights-reference-queryapi) pour la référence complète de l’API de requête de hello
* [Créer un service principal Bonjour portail Azure](../azure-resource-manager/resource-group-create-service-principal-portal.md)
