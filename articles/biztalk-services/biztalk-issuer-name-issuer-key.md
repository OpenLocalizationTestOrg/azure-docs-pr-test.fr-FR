---
title: "Nom et clé de l’émetteur dans BizTalk Services | Microsoft Docs"
description: "Découvrez comment récupérer le nom et la clé de l'émetteur pour le bus des services ou le contrôle d'accès (ACS) dans BizTalk Services. MABS, WABS"
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
ms.openlocfilehash: b9fd985c23558596408e78eadae00dd0f95c4214
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="biztalk-services-issuer-name-and-issuer-key"></a>Nom et clé de l'émetteur dans BizTalk Services

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Azure BizTalk Services utilise le nom et la clé de l'émetteur Service Bus, ainsi que le nom et la clé de l'émetteur Access Control. Plus précisément :

| Task | Nom et clé de l'émetteur |
| --- | --- |
| Déploiement de votre application à partir de Visual Studio |Nom et clé de l'émetteur Access Control |
| Configuration du portail Azure BizTalk Services |Nom et clé de l'émetteur Access Control |
| Création de relais métier avec les services d'adaptateur BizTalk dans Visual Studio |Nom et clé de l'émetteur Service Bus |

La présente rubrique répertorie les étapes permettant de récupérer le nom et la clé de l’émetteur. 

## <a name="access-control-issuer-name-and-issuer-key"></a>Nom et clé de l'émetteur Access Control
Le nom et la clé de l'émetteur Access Control sont utilisés par les éléments suivants :

* Votre application Azure BizTalk Service créée dans Visual Studio : pour déployer correctement votre application BizTalk Service dans Visual Studio sur Azure, entrez le nom et la clé de l’émetteur Access Control. 
* Portail Azure BizTalk Services : lorsque vous créez un service BizTalk et que vous ouvrez le portail BizTalk Services, votre nom et votre clé de l’émetteur Access Control sont automatiquement inscrits pour vos déploiements avec les mêmes valeurs Access Control.

### <a name="get-the-access-control-issuer-name-and-issuer-key"></a>Obtenir le nom et la clé de l’émetteur Access Control

Pour utiliser ACS pour l’authentification et obtenir les valeurs de nom et de clé de l’émetteur, les étapes générales sont les suivantes :

1. Installez les [applets de commande Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).
2. Ajoutez votre compte Azure : `Add-AzureAccount`
3. Retournez le nom de votre abonnement : `get-azuresubscription`
4. Sélectionnez votre abonnement : `select-azuresubscription <name of your subscription>` 
5. Créez un espace de noms : `new-azuresbnamespace <name for the service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`

    Exemple :`new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`
      
5. Lorsque le nouvel espace de noms ACS est créé (ce qui peut prendre plusieurs minutes), les valeurs de nom et de clé de l’émetteur sont répertoriées dans la chaîne de connexion : 

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

Pour résumer :  
Nom de l’émetteur = SharedSecretIssuer  
Clé de l’émetteur = SharedSecretKey

Informations complémentaires sur l’applet de commande [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx). 

## <a name="service-bus-issuer-name-and-issuer-key"></a>Nom et clé de l'émetteur Service Bus
Le nom et la clé de l'émetteur Service Bus sont utilisés par BizTalk Adapter Services. Dans votre projet BizTalk Services dans Visual Studio, vous utilisez les services d'adaptateur BizTalk pour vous connecter à un système métier local. Pour vous connecter, vous créez le relais métier et entrez les détails relatifs à votre système métier. À cette occasion, vous entrez également le nom et la clé de l'émetteur Service Bus.

### <a name="to-retrieve-the-service-bus-issuer-name-and-issuer-key"></a>Pour récupérer le nom et la clé de l'émetteur Service Bus
1. Connectez-vous au [portail Azure Classic](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Dans le volet de navigation de gauche, sélectionnez **Service Bus**.
3. Sélectionnez votre espace de noms. Dans la barre des tâches, sélectionnez **Informations de connexion**. Cette action affiche **l’Émetteur par défaut** (Nom de l’émetteur) et la **Clé par défaut** (Clé de l’émetteur). Leurs valeurs peuvent être copiées.  

Pour résumer :  
Nom de l'émetteur = émetteur par défaut  
Clé de l'émetteur = clé par défaut

## <a name="next"></a>Suivant
Autres rubriques Azure BizTalk Services :

* [Installation du Kit de développement logiciel (SDK) Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [Didacticiels : Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [Utilisation du Kit de développement logiciel (SDK) Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a>Voir aussi
* [Utilisation du service de gestion ACS pour configurer des identités de service](http://go.microsoft.com/fwlink/p/?LinkID=303942)<br/>
* [Tableau comparatif des éditions Développeur, De base, Standard et Premium de BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [BizTalk Services : approvisionnement à l’aide du portail Azure Classic](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [Tableau comparatif des états d'approvisionnement BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [Onglets Tableau de bord, Surveiller et Mettre à l'échelle dans BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [Sauvegarde et restauration de BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [Limitation dans BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>

