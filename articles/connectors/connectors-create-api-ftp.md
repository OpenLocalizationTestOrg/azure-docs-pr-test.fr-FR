---
title: "aaaLearn comment toouse hello dans les applications de la logique d’un connecteur FTP | Documents Microsoft"
description: "Créez des applications logiques avec Azure App Service. Se connecter tooFTP server toomanage vos fichiers. Vous pouvez exécuter diverses actions, comme charger, mettre à jour, obtenir et supprimer des fichiers dans le serveur FTP."
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: 
tags: connectors
ms.assetid: d83c55fe-eb59-4b7b-a5ec-afac5c772616
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/22/2016
ms.author: mandia; ladocs
ms.openlocfilehash: a7020df2005ebb34fc569627ae0516b8528cc7a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-ftp-connector"></a>Prise en main connecteur FTP de hello
Utilisez hello FTP connecteur toomonitor, gérer et créer des fichiers sur un serveur FTP. 

toouse [n’importe quel connecteur](apis-list.md), vous devez tout d’abord toocreate une application logique. Vous pouvez démarrer maintenant en [créant une application logique](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooftp"></a>Se connecter tooFTP
Avant que votre application logique peut accéder à n’importe quel service, vous devez tout d’abord toocreate un *connexion* toohello service. Une [connexion](connectors-overview.md) permet d’assurer la connectivité entre une application logique et un autre service.  

### <a name="create-a-connection-tooftp"></a>Créer un tooFTP de connexion
> [!INCLUDE [Steps toocreate a connection tooFTP](../../includes/connectors-create-api-ftp.md)]
> 
> 

## <a name="use-a-ftp-trigger"></a>Utiliser un déclencheur FTP
Un déclencheur est un événement qui peut être utilisé toostart hello flux de travail défini dans une application logique. [En savoir plus sur les déclencheurs](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

> [!IMPORTANT]
> connecteur FTP Hello nécessite un serveur FTP qui est accessible à partir de hello Internet et qui est configuré toooperate avec le mode passif. En outre, le connecteur de hello FTP est **non compatible avec implicite FTPS (FTP sur SSL)**. connecteur de Hello FTP prend uniquement en charge explicite FTPS (FTP sur SSL).  
> 
> 

Dans cet exemple, je vous indiquent comment toouse hello **FTP - lorsqu’un fichier est ajouté ou modifié** déclencher tooinitiate un flux de travail logique application lorsqu’un fichier est ajouté à ou modifié sur un serveur FTP. Dans un exemple d’entreprise, vous pouvez utiliser cette toomonitor déclencheur un dossier FTP pour les nouveaux fichiers qui représentent des commandes des clients.  Vous pouvez ensuite utiliser une action de connecteur FTP comme **obtenir le contenu du fichier** contenu de hello tooget de commande hello pour poursuivre le traitement et de stockage dans votre base de données de commandes.

1. Entrez *ftp* dans la zone de recherche de hello sur le Concepteur d’applications hello logique, puis sélectionnez hello **FTP - lorsqu’un fichier est ajouté ou modifié** déclencheur   
   ![Image de déclencheur FTP 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)  
   Hello **lorsqu’un fichier est ajouté ou modifié** contrôle s’ouvre  
   ![Image de déclencheur FTP 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)  
2. Sélectionnez hello **...**  situé sur le côté droit de hello du contrôle de hello. Cette opération ouvre le contrôle de sélecteur de dossier hello  
   ![Image de déclencheur FTP 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)  
3. Sélectionnez hello  **>**  (flèche droite) et recherchez le dossier de hello toofind que vous souhaitez toomonitor pour les fichiers nouveaux ou modifiés. Sélectionnez le dossier de hello et notez le dossier de hello est maintenant affichée dans hello **dossier** contrôle.  
   ![Image de déclencheur FTP 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)   

À ce stade, votre application logique a été configurée avec un déclencheur qui commence une série de hello autres déclencheurs et les actions dans le flux de travail hello lorsqu’un fichier est modifié ou créé dans le dossier FTP hello. 

> [!NOTE]
> Pour un toobe application logique fonctionnelle, il doit contenir au moins un déclencheur et une action. Suivez les étapes de hello de hello suivant section tooadd une action.  
> 
> 

## <a name="use-a-ftp-action"></a>Utiliser une action FTP
Une action est une opération effectuée par flux de travail hello défini dans une application logique. [En savoir plus sur les actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

Maintenant que vous avez ajouté un déclencheur, suivez ces étapes de tooadd une action qui obtiennent contenu hello de fichier nouveau ou modifié hello trouvés par le déclencheur de hello.    

1. Sélectionnez **+ nouvelle étape** contenu hello tooadd hello hello action tooget du fichier hello sur le serveur de hello FTP  
2. Sélectionnez hello **ajouter une action** lien.  
   ![Image d’action FTP 1](./media/connectors-create-api-ftp/ftp-action-1.png)  
3. Entrez *FTP* toosearch pour toutes les actions liées tooFTP.
4. Sélectionnez **FTP - obtenir le contenu du fichier** comme hello action tootake lorsqu’un fichier nouveau ou modifié est trouvé dans le dossier de hello FTP.      
   ![Image d’action FTP 2](./media/connectors-create-api-ftp/ftp-action-2.png)  
   Hello **obtenir le contenu du fichier** contrôle s’ouvre. **Remarque**: vous est demandée tooauthorize votre tooaccess d’application logique votre serveur FTP de compte si vous le n'avez pas fait précédemment.  
   ![Image d’action FTP 3](./media/connectors-create-api-ftp/ftp-action-3.png)   
5. Sélectionnez hello **fichier** contrôle (hello un espace blanc situé sous **fichier***). Ici, vous pouvez utiliser une des hello différentes propriétés de fichier nouveau ou modifié hello trouvé sur le serveur FTP de hello.  
6. Sélectionnez hello **le contenu du fichier** option.  
   ![Image d’action FTP 4](./media/connectors-create-api-ftp/ftp-action-4.png)   
7. contrôle de Hello est mise à jour, indiquant que hello **FTP - obtenir le contenu du fichier** action obtiendrez hello *le contenu du fichier* du fichier de hello nouvelles ou modifiées sur le serveur de hello FTP.      
   ![Image d’action FTP 5](./media/connectors-create-api-ftp/ftp-action-5.png)     
8. Enregistrez votre travail, puis ajoutez un tootest de dossier FTP de fichiers toohello votre flux de travail.    

À ce stade, l’application de hello logique a été configuré avec un déclencheur toomonitor un dossier sur un serveur FTP et le flux de travail initier hello lorsqu’il détecte un nouveau fichier ou un fichier modifié sur le serveur de hello FTP. 

application logique de Hello a également été configurée avec une action tooget hello hello nouvelles ou modifiées fichier.

Vous pouvez maintenant ajouter une autre action, par exemple hello [SQL Server - ligne d’insertion](connectors-create-api-sqlazure.md) action tooinsert hello contenu du hello nouvelle ou modifiée dans une table de base de données SQL.  

## <a name="connector-specific-details"></a>Détails spécifiques du connecteur

Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/ftpconnector/). 

## <a name="next-steps"></a>Étapes suivantes
[Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md)

