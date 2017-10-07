---
title: "les applications à partir des Services BizTalk tooAzure Logic Apps aaaMove | Documents Microsoft"
description: "Déplacer ou de la migration d’Azure BizTalk Services MABS tooLogic applications"
services: logic-apps
documentationcenter: 
author: jonfancey
manager: anneta
editor: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: ladocs; jonfan; mandia
ms.openlocfilehash: b3b065b90a37002f72305b0fc866c24231fb5f9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-from-biztalk-services-toologic-apps"></a>Déplacer à partir des Services BizTalk tooLogic applications

Microsoft Azure BizTalk Services (MABS) fait l’objet d’une mise hors service. Utilisez cette toomove rubrique votre tooAzure de solutions d’intégration MABS Logic Apps. 

## <a name="overview"></a>Vue d'ensemble

BizTalk Services se compose de deux services secondaires :

1.  Le service Connexions hybrides Microsoft BizTalk Services
2.  L’intégration de pont IAE et EDI

Si vous recherchez des connexions hybrides toomove, puis [Azure App Service hybride connexions](../app-service/app-service-hybrid-connections.md) décrit les fonctionnalités de ce service et les modifications de hello. Le service Connexions hybrides Azure remplace le service Connexions hybrides BizTalk Services. Les connexions hybrides Azure est disponible avec le Service d’application Azure et est proposée dans hello portail Azure. Les connexions hybrides Azure fournit également un nouveau toomanage de gestionnaire de connexions hybrides existantes des connexions hybrides BizTalk Services, et les nouvelles connexions hybrides dans que vous créez hello portail. Le service Connexions hybrides Azure App Service bénéficie d’une mise à disposition générale.

Pour l’intégration basée sur le pont EAI et EDI, Logic Apps est le remplacement de hello. Logique d’applications fournit que toutes les hello les mêmes fonctionnalités que les Services BizTalk et bien plus encore. Logique d’applications fournit l’échelle du cloud basée sur la consommation du flux de travail et d’orchestration des fonctionnalités qui vous permettent de tooquickly et faciliter la génération de solutions d’intégration complexes à l’aide d’un navigateur ou à l’aide des outils dans Visual Studio.

Hello tableau suivant fournit un mappage des fonctionnalités de BizTalk Services tooLogic applications.

| BizTalk Services   | Logic Apps            | Objectif                  |
| ------------------ | --------------------- | ---------------------------- |
| Connecteur          | Connecteur             | Envoi et réception de données   |
| Pont             | Application logique             | Processeur de pipeline           |
| Étape de validation     | Action de validation XML      | Valider un document XML par rapport à un schéma             |
| Étape d’enrichissement       | Jetons de données      | Promouvoir les propriétés dans des messages ou pour des décisions de routage             |
| Étape de transformation    | Action de transformation      | Convertir les messages XML à partir d’un format tooanother             |
| Étape de décodage       | Action de décodage de fichier plat      | Convertir à partir du fichier plat tooXML             |
| Étape d’encodage       |  Action d’encodage de fichier plat      | Convertir à partir du fichier XML de tooflat             |
| Inspecteur de message       |  Azure Functions ou API Apps      | Exécuter du code personnalisé dans vos intégrations             |
| Action de routage      |  Condition ou commutateur      | Tooone de messages d’itinéraire de hello spécifié des connecteurs             |

Il existe différents types d’artefact dans BizTalk Services.

## <a name="connectors"></a>Connecteurs
Connecteurs dans BizTalk Services autoriser des ponts toosend et recevoir des données, y compris les ponts bidirectionnelles prenant des interactions de demande/réponse basée sur HTTP. Dans les applications de la logique, hello même terminologie est utilisée. Connecteurs dans les applications logique servent hello même finalité et également inclure plus 140 qui peuvent se connecter tooa une vaste gamme de technologies et services, à la fois localement à l’aide de hello passerelle de données locale (en remplaçant hello BizTalk Adapter Service utilisé par les Services BizTalk), et cloud services SaaS et PaaS tels que OneDrive, Office 365, Dynamics CRM et bien plus encore.

Sources dans les Services BizTalk sont tooFTP limité, SFTP et file d’attente du Bus de Service ou abonnement à une rubrique.

![](media/logic-apps-move-from-mabs/sources.png)

Chaque pont a un point de terminaison HTTP par défaut, ce qui est configuré avec hello adresse d’exécution et les propriétés de l’adresse Relative du pont de hello hello. tooachieve même hello avec Logic Apps, utilisez hello [demande et réponse](../connectors/connectors-native-reqres.md) actions.

## <a name="xml-processing-and-bridges"></a>Traitement XML et ponts
Un pont dans BizTalk Services est un pipeline de traitement tooa analogue. Un pont peut prendre les données reçues à partir d’un connecteur, et effectuez certaines des données de hello, puis envoyez-le tooanother système. Logique d’applications hello même prise en charge de hello même pipeline-interaction avec des modèles en tant que les Services BizTalk et fournit également un nombre d’autres modèles d’intégration. Hello [pont demande-réponse XML](https://msdn.microsoft.com/library/azure/hh689781.aspx) dans BizTalk Services est appelé un pipeline VETER composé d’étapes qui peuvent :

* (V) Valider
* (E) Enrichir
* (T) Transformer
* (E) Enrichir
* (R) Router

Comme indiqué dans hello suivant l’image, le traitement hello est fractionné entre la demande et la réponse et permet de contrôler les demande hello et hello les chemins de réponse séparément (par exemple, à l’aide des mappages différents pour chaque) :

![](media/logic-apps-move-from-mabs/xml-request-reply.png)

En outre, un pont unidirectionnel XML ajoute les étapes décoder et encoder au début de hello et à la fin du traitement, et hello pont intermédiaire contient une seule étape d’enrichissement.

### <a name="message-processing-and-decodingencoding"></a>Traitement et décodage/encodage des messages
Dans BizTalk Services, vous recevez les messages XML de types différents et déterminez le schéma correspondant de hello pour le message de salutation reçu. Cette opération est effectuée dans hello **Types de messages** étape Hello le traitement pipeline de réception. Hello phase de décodage utilise ensuite toodecode de type de message hello détecté à l’aide du schéma de hello fourni. Si le schéma de hello est un schéma flatfile, il convertit hello entrants flatfile tooXML. 

Logic Apps offre des fonctionnalités similaires. Vous recevez un flatfile sur une multitude de différents protocoles, à l’aide de déclencheurs de connecteur différents hello (système de fichiers, FTP, HTTP et ainsi de suite) et utiliser hello [décoder de fichier plat](../logic-apps/logic-apps-enterprise-integration-flatfile.md) tooconvert action hello entrants tooXML de données. Vous pouvez déplacer vos schémas de fichier plat existant directement toologic des applications sans nécessiter une change et télécharger schémas tooyour compte d’intégration.

### <a name="validation"></a>Validation
Une fois hello les données entrantes tooXML converti (ou si le code XML est format de message de salutation reçu), la validation s’exécute toodetermine si le message de type hello respecte le schéma XSD tooyour. toodo dans Logic Apps, utilisez hello [Validation XML](../logic-apps/logic-apps-enterprise-integration-xml-validation.md) action. Là encore, vous pouvez utiliser hello les mêmes schémas des Services BizTalk sans aucune modification.

### <a name="transform-messages"></a>Transformer des messages
Dans les Services BizTalk, phase de transformation hello convertit un tooanother de format de message basée sur XML. Pour cela, en appliquant un mappage, à l’aide du mappeur de base TRFM hello. Dans les applications de la logique, les processus de hello est similaire. Hello action transformer exécute un mappage à partir de votre compte d’intégration. Hello principale différence est que les mappages dans les applications logique sont au format XSLT. XSLT inclut tooreuse de capacité hello existant XSLT que vous avez déjà, y compris les mappages créés pour BizTalk Server qui contiennent des fonctoids. 

### <a name="routing-rules"></a>Règles de routage
Les Services BizTalk prend une décision de routage sur les point de terminaison/connecteur toosend messages/données entrantes. Hello capacité tooselect, un d’un nombre de points de terminaison préconfigurés est possible à l’aide d’option de filtre de routage hello :

![](media/logic-apps-move-from-mabs/route-filter.png)

Logic Apps offre des fonctionnalités de logique plus sophistiquées avec les options de [condition](../logic-apps/logic-apps-use-logic-app-features.md) et de [commutateur](../logic-apps/logic-apps-switch-case.md), permettant un flux de contrôle et un routage avancés. La conversion des filtres de routage dans BizTalk Services est mieux obtenue en utilisant une **condition** *si* uniquement deux options sont disponibles. S’il en existe plus de deux, utilisez un **commutateur**.

### <a name="enrich"></a>Enrichissement
Hello phase d’enrichissement dans le traitement des Services BizTalk ajoute le contexte du message toohello propriétés associée aux données hello reçues. Par exemple, promouvoir un toouse de propriété pour le routage (voir ci-dessous) à partir d’une recherche de base de données ou en extrayant une valeur à l’aide d’une expression XPath. Logique d’applications fournit l’accès tooall des données contextuelles sorties à partir de la précédente actions, rendant tooreplicate simple hello même comportement. Par exemple, à l’aide de hello `Get Row` action de connexion SQL, vous retournez les données à partir d’une base de données SQL Server et utiliser les données hello dans une action de l’arbre de décision pour le routage. De même, les propriétés sur le Bus de Service entrant en file d’attente des messages par un déclencheur sont adressable, ainsi que de XPath à l’aide d’expressions de langage de définition hello xpath du flux de travail.

### <a name="use-custom-code"></a>Utiliser un code personnalisé
Les Services BizTalk fournit la possibilité de hello trop[exécuter du code personnalisé](https://msdn.microsoft.com/library/azure/dn232389.aspx) téléchargé dans vos propres assemblys. L’implémentation hello [IMessageInspector](https://msdn.microsoft.com/library/microsoft.biztalk.services.imessageinspector.aspx) interface. Chaque étape du pont de hello inclut deux propriétés (inspecteur d’entrée et inspecteur de sortie) qui fournissent le type de .net hello créé qui implémente cette interface. Code personnalisé vous permet de tooperform plus complexes de traitement sur les données de salutation, ainsi que la réutilisation de code existant dans les assemblys qui effectuent une logique métier commune. 

Logique d’applications fournit deux façons principales tooexecute un code personnalisé : fonctions d’Azure et les applications API. Les fonctions Azure Functions peuvent être créées et appelées à partir d’applications logiques. Consultez [Ajout et exécution d’un code personnalisé pour des applications logiques avec Azure Functions](../logic-apps/logic-apps-azure-functions.md). Utilisez les applications API, partie du Service d’applications Azure, toocreate vos propres déclencheurs et les actions. En savoir plus sur [création d’un toouse API personnalisée avec Logic Apps](../logic-apps/logic-apps-create-api-app.md). 

Si vous avez un code personnalisé dans assmeblies que vous appelez des Services BizTalk, vous pouvez déplacer ce code tooAzure fonctions, ou créer des API personnalisées avec API Apps ; selon ce que vous implémentez. Par exemple, si vous disposez du code qui inclut un autre service que Logic Apps n’a pas un connecteur, puis créer une application API et utiliser des actions hello que votre application API fournit au sein de votre application logique. Si vous avez des fonctions d’assistance ou bibliothèques, les fonctions Azure est probablement hello le mieux adapté.

### <a name="edi-processing-and-trading-partner-management"></a>Traitement EDI et gestion des partenaires commerciaux
BizTalk Services inclut le traitement EDI et B2B avec prise en charge d’AS2 (Applicability Statement 2), X12 et EDIFACT. Logic Apps également. Dans BizTalk Services, votre créer des ponts EDI et créez et gérez des partenaires commerciaux et des accords dans le portail de gestion et de suivi dédié hello.

Dans les applications de la logique, cette fonctionnalité est fournie avec hello [Pack d’intégration Enterprise](../logic-apps/logic-apps-enterprise-integration-overview.md). Il s’agit des actions de compte d’intégration et B2B hello pour le traitement EDI et B2B. Hello [compte d’intégration](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) est toocreate utilisé et de gérer [des partenaires commerciaux](../logic-apps/logic-apps-enterprise-integration-partners.md) et [accords](../logic-apps/logic-apps-enterprise-integration-agreements.md). Une fois que vous créez un compte d’intégration, vous pouvez associer un ou plusieurs comptes de toohello logique applications. Une fois qu’associé, vous pouvez utiliser hello B2B actions tooaccess commerciaux d’informations sur le partenaire au sein de votre application logique. Hello suit les actions est fournie :

* Encodage AS2
* Décodage AS2
* Encodage X12
* Décodage X12
* Encodage EDIFACT
* Décodage EDIFACT

Contrairement aux Services de BizTalk, ces actions sont dissociées de protocoles de transport hello. Par conséquent, lorsque vous créez vos applications logiques, vous avez davantage de flexibilité sur les connecteurs, vous utilisez toosend et recevez des données. Par exemple, il est possible tooreceive X12 fichiers comme des pièces jointes de messagerie et ensuite traiter ces fichiers dans une application logique. 

## <a name="manage-and-monitor"></a>Gestion et surveillance
Ainsi que la gestion des partenaires commerciaux, hello dédié au portail BizTalk Services fournies toomonitor des fonctionnalités de suivi et de résoudre les problèmes. 

Logique d’applications fournit le suivi et l’analyse des capacités de hello plus riche [portail Azure](../logic-apps/logic-apps-monitor-your-logic-apps.md)et avec hello [Operations Management Suite B2B solution](../logic-apps/logic-apps-monitor-b2b-message.md), notamment une application mobile pour conserver un œil sur les éléments Lorsque vous êtes sur hello déplacer.

## <a name="high-availability"></a>Haute disponibilité
tooachieve haute disponibilité (HA) dans les Services BizTalk, vous utilisez plusieurs instances dans un Bonjour tooshare de région donnée charge de traitement. Avec les applications logiques, la haute disponibilité dans une région est intégrée et est fournie sans coût supplémentaire. Pour une récupération d’urgence hors région d’un traitement B2B dans BizTalk Services, un processus de sauvegarde et de restauration est requis. Dans les applications de la logique, un entre régions actif/passif [capacité de récupération d’urgence](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md) est fourni ; qui permet de synchroniser les données B2B hello sur plusieurs comptes d’intégration dans des régions différentes pour la continuité d’activité.

## <a name="next"></a>Suivant
* [Qu’est-ce qu’une application logique ?](logic-apps-what-are-logic-apps.md)
* [Créez votre première application logique](logic-apps-create-a-logic-app.md), ou devenez rapidement opérationnel à l’aide d’un [modèle prédéfini](logic-apps-use-logic-app-templates.md)  
* [Afficher tous les hello connecteurs disponibles](../connectors/apis-list.md) que vous pouvez utiliser dans une application de logique
