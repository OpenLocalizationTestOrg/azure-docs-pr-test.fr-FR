---
title: "vue d’ensemble des connexions aaaHybrid | Documents Microsoft"
description: "Découvrez les connexions hybrides, la sécurité, les ports TCP et les configurations prises en charge. MABS, WABS."
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: erikre
editor: 
ms.assetid: 216e4927-6863-46e7-aa7c-77fec575c8a6
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/18/2016
ms.author: ccompy
ms.openlocfilehash: f092c6019aae761e1e73f13d1af8446a896515c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-connections-overview"></a>Aperçu des connexions hybrides

> [!IMPORTANT]
> Les connexions hybrides BizTalk ont été supprimées et remplacées par les connexions hybrides App Service. Pour plus d’informations, y compris comment toomanage vos connexions hybrides BizTalk existant, consultez [connexions hybrides de Azure App Service](../app-service/app-service-hybrid-connections.md).

Introduction tooHybrid connexions, répertorie les configurations de hello pris en charge, et les listes hello aux ports TCP requis.

## <a name="what-is-a-hybrid-connection"></a>Présentation des connexions hybrides
Les connexions hybrides sont une fonctionnalité d’Azure BizTalk Services : Connexions hybrides fournissent une fonctionnalité de façon simple et pratique tooconnect hello Web Apps dans Azure App Service (anciennement sites Web) et la fonctionnalité des applications mobiles hello dans les ressources du Service d’applications Azure (anciennement Mobile Services) local tooon derrière votre pare-feu.

![les connexions hybrides][HCImage]

Les avantages des connexions hybrides sont les suivants :

* Les applications Web Apps et Mobile Apps peuvent accéder aux données et aux services locaux existants en toute sécurité.
* Plusieurs applications Web ou des applications mobiles peuvent partager un tooaccess de connexion hybride une ressource locale.
* Les ports TCP minimales sont requises tooaccess votre réseau.
* Applications à l’aide de connexions hybrides accéder uniquement hello spécifique ressource locale qui est publiée via hello connexion hybride.
* Peut se connecter ressource locale tooany qui utilise un port TCP statique, telles que SQL Server, MySQL, API Web de HTTP et la plupart des Services Web personnalisés.
  
  > [!NOTE]
  > Actuellement, les services TCP qui utilisent des ports dynamiques (tels que le mode FTP passif ou le mode passif étendu) ne sont pas pris en charge. Le protocole LDAP n’est pas non plus pris en charge. Celui-ci utilise un port TCP statique, mais il peut également utiliser un port UDP. Par conséquent, il n’est pas pris en charge.
  > 
  > 
* Elles peuvent être utilisées avec toutes les infrastructures prises en charge par Web Apps (.NET, PHP, Java, Python, Node.js) et Mobile Apps (Node.js, .NET).
* Applications Web et des applications mobiles peuvent accéder à des ressources locales dans exactement hello même façon que si hello Web ou application Mobile se trouve sur votre réseau local. Par exemple, hello même chaîne de connexion utilisés sur site peuvent également être utilisés sur Azure.

Connexions hybrides fournissent également des administrateurs d’entreprise avec le contrôle et la visibilité des ressources d’entreprise de hello accessibles par des applications hybrides, y compris :

* Paramètres de stratégie de groupe, les administrateurs peuvent autoriser des connexions hybrides sur le réseau de hello et désignez également les ressources qui sont accessibles par les applications hybrides.
* Journaux d’événements et d’audit sur le réseau d’entreprise de hello offrent une visibilité en ressources hello accédé par les connexions hybrides.

## <a name="example-scenarios"></a>Exemples de scénarios
Connexions hybrides prennent en charge hello suivant des combinaisons d’infrastructure et d’application :

* .NET framework accès tooSQL Server
* Services de .NET framework accès tooHTTP/HTTPS avec WebClient
* PHP accès tooSQL Server, MySQL
* Java accès tooSQL Server, MySQL et Oracle
* Services de Java accès tooHTTP/HTTPS

Lors de l’aide de connexions hybrides tooaccess sur site SQL Server, considérez les éléments de hello suivants :

* Instances nommées de SQL Express doit être configuré toouse les ports statiques. Par défaut, les instances nommées SQL Express utilisent des ports dynamiques.
* Les instances par défaut de SQL Express utilisent un port statique, mais TCP doit être activé. Par défaut, TCP n’est pas activé.
* Lorsque vous utilisez la gestion de clusters ou des groupes de disponibilité, hello `MultiSubnetFailover=true` mode n’est actuellement pas pris en charge.
* Hello `ApplicationIntent=ReadOnly` n’est actuellement pas pris en charge.
* L’authentification SQL peut être requise comme méthode d’autorisation de bout en bout de hello pris en charge par hello application Windows Azure et SQL server sur site de hello.

## <a name="security-and-ports"></a>Ports et sécurité
Connexions hybrides utilisent des connexions de Signature d’accès partagé (SAS) d’autorisation toosecure hello de hello Azure hello et les applications sur site Gestionnaire de connexions hybrides toohello la connexion hybride. Clés de connexion distincts sont créés pour une application hello et hello Gestionnaire de connexions hybrides sur site. Ces clés de connexion peuvent être substituées et révoquées indépendamment.

Fournissent des connexions hybrides pour la distribution transparente et sécurisée d’applications de toohello clés hello hello locaux et Gestionnaire de connexions hybrides.

Consultez la page [Création et gestion des connexions hybrides](integration-hybrid-connection-create-manage.md).

*Autorisation de l’application est distincte de la connexion hybride de hello*. Toute méthode d'autorisation appropriée peut être utilisée. méthode d’autorisation Hello dépend des méthodes d’autorisation de bout en bout hello prises en charge sur hello cloud Azure et hello des composants locaux. Par exemple, votre application Azure accède à un serveur SQL local. Dans ce scénario, l’autorisation de SQL peut être méthode hello d’autorisation qui est pris en charge de bout en bout.

#### <a name="tcp-ports"></a>Ports TCP
Les connexions hybrides nécessitent seulement une connectivité TCP ou HTTP sortante à partir de votre réseau privé. Ne pas besoin tooopen de ports de pare-feu ou de modifier votre tooallow de configuration de périmètre réseau toute connectivité entrante à votre réseau.

Hello suivant les ports TCP est utilisé par les connexions hybrides :

| Port | Raison |
| --- | --- |
| 9350 - 9354 |Ces ports sont utilisés pour la transmission de données. Gestionnaire de relais Service Bus Hello sondes port 9350 toodetermine si la connexion TCP est disponible. Si elle est disponible, il suppose que le port 9352 est également disponible. Le trafic de données passe par le port 9352. <br/><br/>Autoriser les connexions sortantes des ports de toothese. |
| 5671 |Lorsque le port 9352 est utilisé pour le trafic de données, port 5671 est utilisé en tant que canal de contrôle hello. <br/><br/>Autoriser les connexions sortantes toothis port. |
| 80, 443 |Ces ports sont utilisés pour certaines tooAzure de demandes de données. Également, si les ports 9352 et 5671 ne sont pas utilisables, *puis* ports 80 et 443 sont des ports de secours hello utilisés pour la transmission de données et le canal de contrôle hello.<br/><br/>Autoriser les connexions sortantes des ports de toothese. <br/><br/>**Remarque** n’est pas recommandé de toouse ces comme hello secours ports à la place de hello autres ports TCP. Hello HTTP/WebSocket est utilisé en tant que protocole hello au lieu de TCP natif pour les canaux de données. Cela peut entraîner une dégradation des performances. |

## <a name="next-steps"></a>Étapes suivantes
[Create and manage Hybrid Connections](integration-hybrid-connection-create-manage.md)<br/>
[Connecter des applications Web Azure tooan ressource locale](../app-service-web/web-sites-hybrid-connection-get-started.md)<br/>
[Se connecter tooon local SQL Server à partir d’une application web Azure](../app-service-web/web-sites-hybrid-connection-connect-on-premises-sql-server.md)<br/>

## <a name="see-also"></a>Voir aussi
[API REST pour gérer BizTalk Services sur Microsoft Azure](http://msdn.microsoft.com/library/azure/dn232347.aspx)
[Tableau comparatif des éditions de BizTalk Services](biztalk-editions-feature-chart.md)<br/>
[Créer un service BizTalk à l’aide du portail Azure](biztalk-provision-services.md)<br/>
[Onglets Tableau de bord, Surveiller et Mettre à l’échelle dans BizTalk Services](biztalk-dashboard-monitor-scale-tabs.md)<br/>

[HCImage]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionImage.png
[HybridConnectionTab]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionTab.png
[HCOnPremSetup]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionOnPremSetup.png
[HCManageConnection]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionManageConn.png
