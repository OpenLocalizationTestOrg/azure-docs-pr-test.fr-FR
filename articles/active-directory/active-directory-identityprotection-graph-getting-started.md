---
title: "aaaGet a démarré avec la Protection d’identité Azure Active Directory et Microsoft Graph | Documents Microsoft"
description: "Fournit un tooquery présentation Microsoft Graph pour obtenir la liste des événements à risque et des informations associées à partir d’Azure Active Directory."
services: active-directory
keywords: "azure active directory identity protection, événement à risque, vulnérabilité, stratégie de sécurité, Microsoft Graph"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: fa109ba7-a914-437b-821d-2bd98e681386
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 75b8b7629a0120d8101f6fde0d9163122503d276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-identity-protection-and-microsoft-graph"></a>Prise en main d’Azure Active Directory Identity Protection et de Microsoft Graph
Microsoft Graph est hello Microsoft unified point de terminaison API et hello domestique de [Azure Active Directory Identity Protection](active-directory-identityprotection.md) API. Hello première API, **identityRiskEvents**, vous permet de tooquery Microsoft Graph pour obtenir la liste de [risque d’événements](active-directory-identityprotection-risk-events-types.md) et des informations associées. Cet article vous permet de vous familiariser avec l’interrogation de cette API. Pour une présentation approfondie, la documentation complète et accès toohello Explorateur graphique, consultez hello [site de Microsoft Graph](https://graph.microsoft.io/).

> [!IMPORTANT]
> Microsoft recommande de gérer Azure AD en utilisant hello [centre d’administration Azure AD](https://aad.portal.azure.com) Bonjour portail Azure au lieu d’utiliser hello portail Azure classic référencée dans cet article.

Il existe trois étapes tooaccessing identité Protection données via Microsoft Graph :

1. Ajouter une application avec une clé secrète client. 
2. Utilisez ce mot de passe et quelques autres éléments d’informations tooauthenticate tooMicrosoft graphique, lorsque vous recevez un jeton d’authentification. 
3. Utiliser ce point de terminaison de jeton toomake demandes toohello API et obtenir des données de Protection de l’identité.

Avant de commencer, vous aurez besoin des éléments suivants :

* Application hello toocreate du privilèges administrateur dans Azure AD
* nom Hello du domaine de votre locataire (par exemple, contoso.onmicrosoft.com)

## <a name="add-an-application-with-a-client-secret"></a>Ajouter une application avec une clé secrète client
1. [Connectez-vous](https://manage.windowsazure.com) tooyour portail classique Azure en tant qu’administrateur. 
2. Sur dans le volet de navigation gauche hello, cliquez sur **Active Directory**. 
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_01.png)
3. À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.
4. Dans le menu hello haut de hello, cliquez sur **Applications**.
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_02.png)
5. Cliquez sur **ajouter** bas hello de page de hello.
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_03.png)
6. Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application développée par mon organisation**.
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_04.png)
7. Sur hello **Parlez-nous de votre application** boîte de dialogue, effectuer hello comme suit :
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_05.png)
   
    a. Bonjour **nom** zone de texte, tapez un nom pour votre application (par exemple : Application de l’API événement AADIP risque).
   
    b. Pour **Type**, sélectionnez **Application web et/ou API web**.
   
    c. Cliquez sur **Suivant**.
8. Sur hello **propriétés de l’application** boîte de dialogue, effectuer hello comme suit :
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_06.png)
   
    a. Bonjour **URL de connexion** zone de texte, type `http://localhost`.
   
    b. Bonjour **URI ID d’application** zone de texte, type `http://localhost`.
   
    c. Cliquez sur **Terminé**.

Vous pouvez à présent configurer votre application.

![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_07.png)

## <a name="grant-your-application-permission-toouse-hello-api"></a>Accorder votre hello de toouse autorisation application API
1. Dans la page de votre application, dans le menu hello haut de hello, cliquez sur **configurer**. 
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_08.png)
2. Bonjour **autorisations tooother applications** , cliquez sur **ajouter application**.
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_09.png)
3. Sur hello **autorisations tooother applications** boîte de dialogue, effectuer hello comme suit :
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_10.png)
   
    a. Sélectionnez **Microsoft Graph**.
   
    b. Cliquez sur **Terminé**.
4. Cliquez sur **Autorisations d’application : 0**, puis sélectionnez **Read all identity risk event information** (Lire toutes les informations sur les événements à risque concernant l’identité).
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_11.png)
5. Cliquez sur **enregistrer** bas hello de page de hello.
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)

## <a name="get-an-access-key"></a>Obtenir une clé d’accès
1. Sur la page de votre application, Bonjour **clés** , sélectionnez 1 an en tant que la durée.
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_13.png)
2. Cliquez sur **enregistrer** bas hello de page de hello.
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)
3. dans la section « clés » hello, copier la valeur hello de votre clé nouvellement créée, puis collez-le dans un emplacement sûr.
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_14.png)
   
   > [!NOTE]
   > Si vous perdez cette clé, vous avez tooreturn toothis section et créer une nouvelle clé. Gardez cette clé secrète : toute personne la possédant peut accéder à vos données.
   > 
   > 
4. Bonjour **propriétés** section, hello de copie **ID Client**, puis collez-la dans un emplacement sûr. 

## <a name="authenticate-toomicrosoft-graph-and-query-hello-identity-risk-events-api"></a>Authentifier tooMicrosoft graphique et hello de requête API d’événements risque identité
À ce stade, vous devez avoir :

* ID de client Hello vous avez copié ci-dessus
* clé Hello que vous avez copié ci-dessus
* nom de Hello du domaine de votre client

tooauthenticate, l’envoi d’une publication demande trop`https://login.microsoft.com` avec hello paramètres dans le corps de hello suivants :

* grant_type : « **client_informationsidentification** »
* resource: “**https://graph.microsoft.com**”
* client_id : <your client ID>
* client_secret : <your key>

> [!NOTE]
> Vous avez besoin de valeurs de tooprovide pour hello **client_id** et hello **client_secret** paramètre.
> 
> 

Si l’opération réussit, elle retourne un jeton d’authentification.  
toocall hello API, créez un en-tête avec hello suivant paramètre :

    `Authorization`=”<token_type> <access_token>"


Lors de l’authentification, vous pouvez trouver le type de jeton hello et le jeton d’accès Bonjour renvoyé un jeton.

Envoyer cet en-tête comme un toohello de demande suivant l’URL de l’API :`https://graph.microsoft.com/beta/identityRiskEvents`

réponse de Hello, en cas de réussite, est une collection d’identité événements à risque et des données associées dans hello format JSON OData, qui peut être analysé et géré convenance.

Voici un exemple de code pour l’authentification et l’appel de l’API hello à l’aide de Powershell.  
Il suffit d’ajouter l’ID client, la clé ainsi que le domaine client.

    $ClientID       = "<your client ID here>"        # Should be a ~36 hex character string; insert your info here
    $ClientSecret   = "<your client secret here>"    # Should be a ~44 character string; insert your info here
    $tenantdomain   = "<your tenant domain here>"    # For example, contoso.onmicrosoft.com

    $loginURL       = "https://login.microsoft.com"
    $resource       = "https://graph.microsoft.com"

    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    Write-Output $oauth

    if ($oauth.access_token -ne $null) {
        $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

        $url = "https://graph.microsoft.com/beta/identityRiskEvents"
        Write-Output $url

        $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)

        foreach ($event in ($myReport.Content | ConvertFrom-Json).value) {
            Write-Output $event
        }

    } else {
        Write-Host "ERROR: No Access Token"
    } 


## <a name="next-steps"></a>Étapes suivantes
Félicitations, vous venez de créer votre première tooMicrosoft d’appel de graphique.  
Maintenant, vous pouvez interroger les événements à risque identité et utilisent les données hello. Toutefois, vous le souhaitez.

toolearn en savoir plus sur Microsoft Graph et comment les applications toobuild à l’aide de hello API Graph, consultez hello [documentation](https://graph.microsoft.io/docs) et bien plus encore sur hello [site de Microsoft Graph](https://graph.microsoft.io/). En outre, assurez-vous que toobookmark hello [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) page qui répertorie toutes les API de Protection d’identité disponibles dans le graphique de hello. Comme nous ajoutons de nouvelles façons toowork, avec la Protection d’identité via l’API, vous verrez les sur cette page.

## <a name="additional-resources"></a>Ressources supplémentaires
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md)
* [Types d’événements à risque détectés par Azure Active Directory Identity Protection](active-directory-identityprotection-risk-events-types.md)
* [Microsoft Graph](https://graph.microsoft.io/)
* [Overview of Microsoft Graph (Vue d’ensemble de Microsoft Graph)](https://graph.microsoft.io/docs)
* [Azure AD Identity Protection Service Root (Racine de service d’Azure AD Identity Protection)](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root)

