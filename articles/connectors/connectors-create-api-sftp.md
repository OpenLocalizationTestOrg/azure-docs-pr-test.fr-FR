---
title: aaaLearn comment toouse hello connecteur SFTP dans vos applications logiques | Documents Microsoft
description: "Créez des applications logiques avec Azure App Service. Se connecter tooSFTP API toosend et recevoir des fichiers. Vous pouvez effectuer diverses opérations, telles que créer, mettre à jour, obtenir ou supprimer des fichiers."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 697eb8b0-4a66-40c7-be7b-6aa6b131c7ad
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/20/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 3f50570191c9b9339fe6584b9056b2549512b789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sftp-connector"></a>Prise en main connecteur SFTP hello
Utilisez hello SFTP connecteur tooaccess un toosend de compte SFTP et recevoir des fichiers. Vous pouvez effectuer diverses opérations, telles que créer, mettre à jour, obtenir ou supprimer des fichiers.  

toouse [n’importe quel connecteur](apis-list.md), vous devez tout d’abord toocreate une application logique. Vous pouvez démarrer maintenant en [créant une application logique](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-toosftp"></a>Se connecter tooSFTP
Avant que votre application logique peut accéder à n’importe quel service, vous devez tout d’abord toocreate un *connexion* toohello service. Une [connexion](connectors-overview.md) permet d’assurer la connectivité entre une application logique et un autre service.  

### <a name="create-a-connection-toosftp"></a>Créer un tooSFTP de connexion
> [!INCLUDE [Steps toocreate a connection tooSFTP](../../includes/connectors-create-api-sftp.md)]
> 
> 

## <a name="use-an-sftp-trigger"></a>Utiliser un déclencheur SFTP
Un déclencheur est un événement qui peut être utilisé toostart hello flux de travail défini dans une application logique. [En savoir plus sur les déclencheurs](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

Dans cet exemple, hello **SFTP - lorsqu’un fichier est ajouté ou modifié** déclencheur est tooinitiate utilisé un flux de travail logique application lorsqu’un fichier est ajouté à ou modifié sur un serveur SFTP. Vous ajoutez également une condition qui vérifie le contenu de hello du fichier nouveau ou modifié de hello et le rend une décision tooextract hello si son contenu indique qu’il doit être extrait avant d’utiliser le contenu de hello. Enfin, ajouter un contenu de hello tooextract action d’un fichier et placer le contenu de hello extrait dans un dossier sur le serveur SFTP de hello. 

Dans un exemple d’entreprise, vous pouvez utiliser cette toomonitor déclencheur un dossier SFTP pour les nouveaux fichiers qui représentent des commandes client.  Vous pouvez ensuite utiliser une action de connecteur SFTP, tel que **obtenir le contenu du fichier**, contenu de hello tooget de commande hello pour poursuivre le traitement et de stockage dans une base de données de commandes.

> [!INCLUDE [Steps toocreate an SFTP trigger](../../includes/connectors-create-api-sftp-trigger.md)]
> 
> 

## <a name="add-a-condition"></a>Ajouter une condition
> [!INCLUDE [Steps tooadd a condition](../../includes/connectors-create-api-sftp-condition.md)]
> 
> 

## <a name="use-an-sftp-action"></a>Utiliser une action SFTP
Une action est une opération effectuée par flux de travail hello défini dans une application logique. [En savoir plus sur les actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

> [!INCLUDE [Steps toocreate an SFTP action](../../includes/connectors-create-api-sftp-action.md)]
> 
> 

## <a name="connector-specific-details"></a>Détails spécifiques du connecteur

Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/sftpconnector/).

## <a name="more-connectors"></a>Autres connecteurs
Revenir en arrière toohello [liste des API](apis-list.md).
