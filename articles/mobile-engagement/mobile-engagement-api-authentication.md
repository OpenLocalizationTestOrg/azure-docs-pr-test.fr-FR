---
title: aaaAuthenticate avec les API REST Mobile Engagement
description: "Décrit comment tooauthenticate avec l’API REST de Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: da82cb36-957a-4e19-a805-b44733cf6597
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/05/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: 9b54aa5ec3da4bcf55ffe5b7e8d1759095d0c486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis"></a>Authentifier avec l’API REST de Mobile Engagement
## <a name="overview"></a>Vue d'ensemble
Ce document décrit comment tooget un Oauth AAD valide de jeton tooauthenticate par hello Mobile Engagement REST API. 

Il suppose que vous disposez d’un abonnement Azure valide et que vous avez créé une application Mobile Engagement à l'aide d'un de nos [didacticiels pour les développeurs](mobile-engagement-windows-store-dotnet-get-started.md).

## <a name="authentication"></a>Authentification
Un jeton OAuth basé sur Microsoft Azure Active Directory est utilisé pour l’authentification. 

Dans la requête d’ordre de tooauthentication une API, un en-tête d’autorisation doit être ajouté demande tooevery de hello suivant du formulaire :

    Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGmJlNmV2ZWJPamg2TTNXR1E...

> [!NOTE]
> Les jetons Azure Active Directory expirent dans 1 heure.
> 
> 

Il existe plusieurs façons tooget un jeton. Depuis hello Qu'api est généralement appelées à partir d’un service cloud, vous souhaitez toouse une clé d’API. Dans la terminologie Azure, une clé d’API est appelée mot de passe principal de du service. Hello procédure suivante décrit une façon toosetting il configurer manuellement.

### <a name="one-time-setup-using-script"></a>Installation unique (à l'aide d’un script)
Vous devez suivez hello instructions sous le programme d’installation hello tooperform à l’aide d’un script PowerShell qui consomme du temps hello minimale pour le programme d’installation, mais utilise hello les valeurs par défaut plus autorisées. Si vous le souhaitez, vous pouvez également suivre les instructions hello Bonjour [le programme d’installation manuelle](mobile-engagement-api-authentication-manual.md) par le biais de hello directement le portail Azure et de configuration plus précie de faire. 

1. Obtenir la version la plus récente d’Azure PowerShell à partir de hello [ici](http://aka.ms/webpi-azps). Pour plus d’informations sur les instructions de téléchargement hello, vous pouvez voir cela [lien](/powershell/azure/overview).  
2. Une fois Azure PowerShell est installé, suivant de hello utilisez commandes tooensure que vous avez hello **module Azure** installé :
   
    a. Assurez-vous que le module Azure PowerShell de hello est disponible dans la liste hello des modules disponibles. 
   
        Get-Module –ListAvailable 
   
    ![Modules Azure disponibles][1]
   
    b. Si vous ne trouvez pas le module Azure PowerShell de hello Bonjour au-dessus de liste puis toorun hello éléments suivants sont nécessaires :
   
        Import-Module Azure 
3. Connexion toohello Azure Resource Manager à partir de PowerShell en exécutant hello la commande suivante et en fournissant votre nom d’utilisateur et un mot de passe pour votre compte Azure : 
   
        Login-AzureRmAccount
4. Si vous avez plusieurs abonnements, puis vous devez exécuter les éléments suivants de hello :
   
    a. Obtenir une liste de tous vos abonnements et hello de copie SubscriptionId d’abonnement hello toouse. Assurez-vous que cet abonnement est hello identique à celui qui a hello l’application Mobile Engagement qui vous toointeract à l’utilisation de hello API. 
   
        Get-AzureRmSubscription
   
    b. La commande suivante d’exécution hello les toobe abonnement d’hello de tooconfigure du SubscriptionId hello fournissant utilisé.
   
        Select-AzureRmSubscription –SubscriptionId <subscriptionId>
5. Copier le texte hello pour hello [New-AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) ordinateur local de tooyour de script et l’enregistrer en tant qu’une applet de commande PowerShell (par exemple, `APIAuth.ps1`) et de l’exécuter `.\APIAuth.ps1`. 
6. Hello script vous demandera tooprovide une entrée pour **principal**. Fournir un nom approprié que vous souhaitez toouse toocreate votre application Active Directory (par exemple, APIAuth). 
7. Une fois hello script terminé, il affiche hello suivant quatre valeurs dont vous aurez besoin tooauthenticate par programme avec Active Directory a donc pas vraiment toocopy les. 
   
    **TenantId**, **SubscriptionId**, **ApplicationId** et **Secret**.
   
    Vous utilisez la valeur TenantId `{TENANT_ID}`, la valeur ApplicationId `{CLIENT_ID}` et la valeur Secret `{CLIENT_SECRET}`.
   
   > [!NOTE]
   > Votre stratégie de sécurité par défaut peut vous empêche d'exécuter un script PowerShell. Dans ce cas, vous configurez temporairement votre exécution stratégie tooallow l’exécution du script à l’aide de hello de commande suivante :
   > 
   > Set-ExecutionPolicy RemoteSigned
   > 
   > 
8. Voici comment ensemble hello d’applets de commande PS ressemble à. 
   
    ![][3]
9. Vérifiez dans le portail de gestion Azure hello qu’une application AD a été créée avec le nom de hello vous fourni toohello script appelé **principal** sous **afficher les Applications que ma société possède**.
   
    ![][4]

#### <a name="steps-tooget-a-valid-token"></a>Étapes tooget un jeton valide
1. Appeler des API de hello avec les paramètres suivants de hello et assurez-vous que tooreplace hello client\_ID, le CLIENT\_ID et le CLIENT\_SECRET :
   
   * **URL de la demande** sous la forme *https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token*
   * **En-tête Content-Type HTTP** sous la forme *application/x-www-form-urlencoded*
   * **Corps de la requête HTTP** sous la forme *grant\_type=client\_credentials&amp;client_id={CLIENT\_ID}&amp;client_secret={CLIENT\_SECRET}&amp;resource=https%3A%2F%2Fmanagement.core.windows.net%2F*
     
     Hello Voici un exemple de demande :
     
       POST /{TENANT_ID}/oauth2/token HTTP/1.1   Host: login.microsoftonline.com   Content-Type: application/x-www-form-urlencoded   grant_type=client_credentials&client_id={CLIENT_ID}&client_secret={CLIENT_SECRET}&reso   urce=https%3A%2F%2Fmanagement.core.windows.net%2F
     
     Voici un exemple de réponse :
     
       HTTP/1.1 200 OK   Content-Type: application/json; charset=utf-8   Content-Length: 1234
     
       {"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}
     
     Cet exemple montre comment inclure encodage URL des paramètres de publication de hello, `resource` valeur est en réalité `https://management.core.windows.net/`. Veillez à coder par URL de tooalso `{CLIENT_SECRET}` comme il peut contenir des caractères spéciaux.
     
     > [!NOTE]
     > Pour le test, vous pouvez utiliser un outil client HTTP comme [Fiddler](http://www.telerik.com/fiddler) ou [l’extension Postman sur Chrome](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop) 
     > 
     > 
2. Dans chaque appel d’API, incluent désormais en-tête de demande d’autorisation hello :
   
        Authorization: Bearer {ACCESS_TOKEN}
   
    Si vous obtenez un code de 401 état retourné, cocher hello corps de la réponse, il peut vous dire à hello jeton a expiré. Dans ce cas, récupérez un nouveau jeton.

## <a name="using-hello-apis"></a>À l’aide des API de hello
Maintenant que vous avez un jeton valide, vous êtes prêt toomake hello API appels.

1. Dans chaque demande d’API, vous devez toopass un jeton valide, non expiré, que vous avez obtenu dans la section précédente de hello.
2. Vous devez tooplug dans certains paramètres dans la demande de hello URI qui identifie votre application. URI de demande Hello ressemble à hello suivant
   
        https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/
        providers/Microsoft.MobileEngagement/appcollections/{app-collection}/apps/{app-resource-name}/
   
    paramètres de hello tooget, cliquez sur le nom de votre application et cliquez sur le tableau de bord et une page s’affiche comme suit hello avec tous les hello 3 paramètres.
   
   * **1**`{subscription-id}`
   * **2**`{app-collection}`
   * **3**`{app-resource-name}`
   * **4** nom de votre groupe de ressources est en train de toobe **MobileEngagement** , sauf si vous avez créé un nouveau. 
     
     ![Paramètres URI d’API Mobile Engagement][2]

> [!NOTE]
> <br/>
> 
> 1. Ignorer hello API racine adresse car il s’agissait de hello API précédentes.<br/>
> 2. Si vous avez créé l’application hello à l’aide du portail Azure Classic vous devez nom de ressource de l’Application hello toouse qui n’a pas de nom de l’Application hello lui-même. Si vous avez créé l’application hello Bonjour portail Azure vous devez utiliser hello nom de l’application elle-même (il n’existe aucune distinction entre le nom de ressource de l’Application et le nom de l’application pour les applications créées dans le nouveau portail de hello).  
> 
> 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication/azure-module.png
[2]: ./media/mobile-engagement-api-authentication/mobile-engagement-api-uri-params.png
[3]: ./media/mobile-engagement-api-authentication/ps-cmdlets.png
[4]: ./media/mobile-engagement-api-authentication/ad-app-creation.png



