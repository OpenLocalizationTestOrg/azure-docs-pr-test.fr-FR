---
title: aaaSecurity Hubs de Notification
description: "Cette rubrique décrit la sécurité des hubs de notification Azure."
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: 6506177c-e25c-4af7-8508-a3ddca9dc07c
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: f59ad4594c2c0a2e2b22ab0b6d6bad53825a4dc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="security"></a>Sécurité
## <a name="overview"></a>Vue d'ensemble
Cette rubrique décrit le modèle de sécurité hello d’Azure Notification Hubs. Notification Hubs étant une entité Service Bus, qu’ils implémentent hello même modèle de sécurité en tant que Service Bus. Pour plus d’informations, consultez hello [authentification Service Bus](https://msdn.microsoft.com/library/azure/dn155925.aspx) rubriques.

## <a name="shared-access-signature-security-sas"></a>Sécurité Signature d'accès partagé (SAP)
Notification Hubs implémente un modèle de sécurité de niveau entité appelé SAP (Signature d'accès partagé). Ce schéma permet de messagerie toodeclare d’entités des règles d’autorisation too12 dans leur description qui accordent des droits sur cette entité.

Chaque règle contient un nom, une valeur de clé (secret partagé) et un ensemble de droits, comme expliqué dans la section de hello « Revendications de sécurité ». Lorsque vous créez un Hub de Notification, les deux règles sont créées automatiquement : un avec les droits d’écoute (qui hello client application utilise) et une avec tous les droits (hello application principal utilise).

Lors de la gestion de l’inscription des applications clientes, si les informations de hello envoyées via notifications ne sont pas sensibles (par exemple, les mises à jour de la météo), un tooaccess de manière commune un concentrateur de Notification est toogive hello la valeur clé de hello règle accès en écoute uniquement toohello application cliente et valeur de clé toogive hello du serveur principal d’application hello règle un accès complet toohello.

Il est déconseillé d’incorporer les valeur de clé hello dans les applications clientes du Windows Store. Un tooavoid de façon incorporer la valeur de clé hello est toohave hello client application récupérer à partir du serveur principal d’application hello au démarrage.

Il est important toounderstand qui hello clé avec accès en écoute permet à un client tooregister d’application à des balises. Si votre application doit limiter les clients les inscriptions toospecific balises toospecific (par exemple, lorsque les balises représentent des ID utilisateur), service principal de votre application doit effectuer les inscriptions hello. Pour plus d'informations, consultez Gestion des inscriptions. Notez que dans cette façon, hello client application ne dispose pas d’un accès direct tooNotification concentrateurs.

## <a name="security-claims"></a>Revendications de sécurité
Les entités tooother similaires, les opérations de Hub de Notification sont autorisées pour trois revendications de sécurité : écouter, envoyer et gérer.

| Revendication | Description | Opérations autorisées |
| --- | --- | --- |
| Écouter |Créer/mettre à jour, lire et supprimer des inscriptions uniques |Créer/mettre à jour une inscription<br><br>Lire une inscription<br><br>Lire toutes les inscriptions pour un handle<br><br>Supprimer une inscription |
| Envoyer |Envoyer le hub de notification de messages toohello |Envoyer un message |
| Gérer |Opérations CRUD sur Notification Hubs (y compris la mise à jour des informations d'identification PNS et les clés de sécurité) et lecture des inscriptions en fonction des balises |Créer/Mettre à jour/Lire/Supprimer des hubs de notification<br><br>Lire des inscriptions par balise |

Notification Hubs accepte les revendications accordées par les jetons de contrôle d’accès Microsoft Azure et de jetons de signature générés avec des clés partagées configurées directement sur hello Hub de Notification.

