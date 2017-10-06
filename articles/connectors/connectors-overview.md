---
title: "aaaOverview des connecteurs d’applications logique | Documents Microsoft"
description: "Vue d’ensemble des connecteurs pouvant être utilisés dans une application logique"
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: ca8dab2e-9b69-4b1e-865d-1facd9f0cdac
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/15/2016
ms.author: jehollan
ms.openlocfilehash: dc4cac4c0dfaa2f9fd218ffc04414fa8e52a91d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-connectors-in-a-logic-app"></a>Utilisation des connecteurs dans une application logique
Les connecteurs fournissent tooevents d’accès rapide, les données et les actions sur les plates-formes, les protocoles et les services.  la liste complète des connecteurs qui prend en charge de Logic Apps Hello peut [se trouve ici](apis-list.md).  Connecteurs peut être utilisés comme un déclencheur ou une action dans une application de la logique et peuvent nécessiter une configuration *connexion* toouse (par exemple : autoriser un Twitter compte tooaccess ou valider à votre place).

## <a name="basics"></a>Concepts de base
Les connecteurs sont des services hébergés, vous pouvez accéder dans le cadre d’un toointegrate d’application logique avec d’autres services tels que Dynamics, Azure, Salesforce, [plus](apis-list.md).  Ils sont déployés et gérés par Microsoft, ce qui signifie que vous pouvez créer vos flux de travail d’intégration sans avoir à vous soucier de la mise à l’échelle, du débit ou de la sécurité.  Vous pouvez ajouter une application de la logique de connecteur tooa par la recherche et en sélectionnant une action de connecteur ou déclencher sous **Microsoft d’afficher les API managées**.

![Menu Action pour la sélection de déclencheurs][1]

Chaque action de connecteur ou un déclencheur aura son jeu de propriétés tooconfigure.  Vous pouvez cliquer sur hello info boutons toolearn en savoir plus sur l’action, ou sa documentation de référence [toolearn plus](apis-list.md).

Si vous souhaitez toointegrate avec un service ou d’une API qui n’est pas encore d’un connecteur, vous pouvez également étendre la logique d’applications via un [lien personnalisé](../logic-apps/logic-apps-create-api-app.md) ou simplement appeler directement toohello service via un protocole tel que HTTP.

## <a name="triggers"></a>Déclencheurs
Certains liens n’ont un déclencheur, ce qui signifie un événement à partir de ce connecteur déclenche une application logique, transmettre des données en tant que partie d’un déclencheur de hello.  Un déclencheur est toujours hello première étape dans une application logique.  Les déclencheurs populaires incluent des opérations telles que :

* Périodicité - exécution toutes les heures
* Quand une requête HTTP est reçue
* Lorsqu’un élément est ajouté à la file d’attente de tooa
* Lors de la réception d’un message électronique

Certains déclencheurs hello instantanée un événement se produit via une application de la logique de toohello de notification et d’autres nécessitent un intervalle de périodicité configuré sur la fréquence à laquelle hello application logique vérifiera service hello pour un événement (haut tooevery 15 secondes).  

Une fois qu’un événement est reçu, application de la logique de hello exécuter se déclenche et actions hello dans le flux de travail hello démarre.  Vous serez également en mesure de tooaccess toutes les données à partir de hello déclenchent tout au long du flux de travail hello (pour hello exemple 'sur un nouveau tweet' déclencheur passera hello tweet dans hello exécuter).

## <a name="actions"></a>Actions
La plupart des connecteurs ont une ou plusieurs actions qui peuvent être exécutées dans le cadre du flux de travail hello.  Les actions sont toutes les étapes qui se produisent après l’exécution de hello a été déclenché à partir d’un déclencheur.  tooadd une action Cliquez sur hello **nouvelle étape** bouton et rechercher de connecteur souhaité toouse hello.  Une fois sélectionné (et après avoir configuré les [connexions](#connections) qui peuvent être nécessaires) vous verrez une carte d’action hello que vous pouvez configurer.  Vous pouvez sélectionner des données à partir des étapes précédentes en cliquant sur un des jetons hello pour les sorties, ou entrer dans une autre configuration en fonction des besoins.

![Configuration d’une action de connecteur][2]

## <a name="connections"></a>Connexions
La plupart des connecteurs nécessitent un tooconfigure un *connexion* avant de pouvoir utiliser des connecteurs hello.  A *connexion* est n’importe quelle connexion ou de configuration de la connexion nécessaire de connecteur de hello tooaccess.  Pour les connecteurs qui utilisent OAuth, de créer une connexion signifie la signature en service hello (comme Office 365, Salesforce ou GitHub) où votre jeton d’accès permettre être chiffré et stocké en toute sécurité dans un magasin des secrets Azure.  D’autres connecteurs (tels que FTP et SQL) nécessitent une connexion configurée à l’aide de paramètres tels que l’adresse du serveur, le nom d’utilisateur et mot de passe.  Ces informations de configuration de connexion sont également chiffrées et stockées de manière sécurisée.  Connexions seront en mesure de tooaccess service hello pour tant que service de hello permet.  Pour les connexions Azure Active Directory OAuth (par exemple, Office 365 et Dynamics) nous puissions continuer indéfiniment le jeton d’accès toorefresh hello.  D’autres services peuvent limiter la durée au cours de laquelle nous pouvons utiliser un jeton sans synchronisation.  En général, certaines actions, telles que la modification d’un mot de passe, invalident tous les jetons d’accès.  

Vous pouvez consulter et gérer les connexions dans Azure en cliquant sur **Parcourir**, puis en sélectionnant **Connexions API**.  À partir de hello ressources des connexions d’API, vous pouvez afficher, modifier, mettre à jour ou renouveler l’autorisation de toutes les connexions que vous avez créé.

## <a name="next-steps"></a>Étapes suivantes
* [Créez votre première application logique](../logic-apps/logic-apps-create-a-logic-app.md)
* [Découvrez des utilisations et des exemples courant(e)s d’applications logiques](../logic-apps/logic-apps-examples-and-scenarios.md)
* [Commencez à utiliser les déclencheurs et actions d’intégration d’entreprise](../logic-apps/logic-apps-enterprise-integration-overview.md)

<!--Image References -->
[1]: ./media/connectors-overview/addAction.png
[2]: ./media/connectors-overview/configureAction.png
