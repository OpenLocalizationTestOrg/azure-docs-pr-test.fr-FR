---
title: "aaaIssuer nom et clé de l’émetteur dans BizTalk Services | Documents Microsoft"
description: "Découvrez comment tooretrieve nom de l’émetteur et la clé de l’émetteur pour Service Bus ou Access Control (ACS) dans les Services BizTalk. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 067fe356-d1aa-420f-b2f2-1a418686470a
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: cc84c2820724ae3e7fc7c40ddbcd83a169add911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-issuer-name-and-issuer-key"></a>Nom et clé de l'émetteur dans BizTalk Services

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Les Services BizTalk Azure utilise hello nom de l’émetteur de Bus de Service et clé de l’émetteur et hello nom de l’émetteur de contrôle de l’accès et clé de l’émetteur. Plus précisément :

| Task | Nom et clé de l'émetteur |
| --- | --- |
| Déploiement de votre application à partir de Visual Studio |Nom et clé de l'émetteur Access Control |
| Configuration hello le portail Azure BizTalk Services |Nom et clé de l'émetteur Access Control |
| Création de relais LOB avec hello Services de l’adaptateur BizTalk dans Visual Studio |Nom et clé de l'émetteur Service Bus |

Cette rubrique répertorie hello étapes tooretrieve hello nom de l’émetteur et la clé de l’émetteur. 

## <a name="access-control-issuer-name-and-issuer-key"></a>Nom et clé de l'émetteur Access Control
Hello, nom de l’émetteur de contrôle de l’accès et la clé d’émetteur sont utilisés par suivant de hello :

* Votre application Azure BizTalk Service créée dans Visual Studio : toosuccessfully déployer votre application de BizTalk Service dans Visual Studio tooAzure, vous entrez hello nom de l’émetteur de contrôle de l’accès et la clé de l’émetteur. 
* Hello le portail Azure BizTalk Services : lorsque vous créez un BizTalk Service et ouvrez hello portail BizTalk Services, votre nom de l’émetteur de contrôle de l’accès et la clé de l’émetteur sont automatiquement enregistrés pour vos déploiements avec hello les mêmes valeurs de contrôle d’accès.

### <a name="get-hello-access-control-issuer-name-and-issuer-key"></a>Obtenir hello du nom de l’émetteur de contrôle de l’accès et la clé de l’émetteur

ACS toouse pour l’authentification et get hello les valeurs de nom de l’émetteur et la clé de l’émetteur, hello étapes incluent :

1. Installer hello [applets de commande Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).
2. Ajoutez votre compte Azure : `Add-AzureAccount`
3. Retournez le nom de votre abonnement : `get-azuresubscription`
4. Sélectionnez votre abonnement : `select-azuresubscription <name of your subscription>` 
5. Créez un espace de noms : `new-azuresbnamespace <name for hello service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`

    Exemple :`new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`
      
5. Lors de la création d’espace de noms ACS de hello (qui peut prendre plusieurs minutes), les valeurs de nom de l’émetteur et la clé de l’émetteur de hello sont répertoriées dans la chaîne de connexion hello : 

    ```
    Name                  : biztalksbnamespace
    Region                : South Central US
    DefaultKey            : abcdefghijklmnopqrstuvwxyz
    Status                : Active
    CreatedAt             : 10/18/2016 9:36:30 PM
    AcsManagementEndpoint : https://biztalksbnamespace-sb.accesscontrol.windows.net/
    ServiceBusEndpoint    : https://biztalksbnamespace.servicebus.windows.net/
    ConnectionString      : Endpoint=sb://biztalksbnamespace.servicebus.windows.net/;SharedSecretIssuer=owner;SharedSecretValue=abcdefghijklmnopqrstuvwxyz
    NamespaceType         : Messaging
    ```

toosummarize :  
Nom de l’émetteur = SharedSecretIssuer  
Clé de l’émetteur = SharedSecretKey

D’autres informations sur hello [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) applet de commande. 

## <a name="service-bus-issuer-name-and-issuer-key"></a>Nom et clé de l'émetteur Service Bus
Le nom et la clé de l'émetteur Service Bus sont utilisés par BizTalk Adapter Services. Dans votre projet BizTalk Services dans Visual Studio, vous utilisez système de hello Services de l’adaptateur BizTalk tooconnect tooan local de métier (LOB). tooconnect, vous créez des hello relais LOB et entrez les détails de votre système métier. Ce faisant, vous entrez également hello nom de l’émetteur de Bus de Service et la clé de l’émetteur.

### <a name="tooretrieve-hello-service-bus-issuer-name-and-issuer-key"></a>tooretrieve hello nom de l’émetteur de Bus de Service et la clé de l’émetteur
1. Connectez-vous à toohello [portail Azure classic](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Dans le volet de navigation gauche hello, sélectionnez **Service Bus**.
3. Sélectionnez votre espace de noms. Dans la barre des tâches hello, sélectionnez **les informations de connexion**. Cela affiche hello **émetteur par défaut** (nom de l’émetteur) et **clé par défaut** (clé d’émetteur). Leurs valeurs peuvent être copiées.  

toosummarize :  
Nom de l'émetteur = émetteur par défaut  
Clé de l'émetteur = clé par défaut

## <a name="next"></a>Suivant
Autres rubriques Azure BizTalk Services :

* [Lors de l’installation Bonjour Azure BizTalk Services SDK](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [Didacticiels : Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [Comment puis-je démarrer à l’aide de hello SDK des Services BizTalk Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a>Voir aussi
* [Comment : utiliser le Service Gestion des services ACS tooConfigure identités de Service](http://go.microsoft.com/fwlink/p/?LinkID=303942)<br/>
* [Tableau comparatif des éditions Développeur, De base, Standard et Premium de BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [BizTalk Services : approvisionnement à l’aide du portail Azure Classic](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [Tableau comparatif des états d'approvisionnement BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [Onglets Tableau de bord, Surveiller et Mettre à l'échelle dans BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [Sauvegarde et restauration de BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [Limitation dans BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>

