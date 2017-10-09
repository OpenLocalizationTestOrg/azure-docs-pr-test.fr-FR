---
title: "contenu d’aaaSync à partir d’un tooAzure de dossier du Service d’applications cloud"
description: "En savoir plus toodeploy votre tooAzure d’application du Service d’applications via le contenu de la synchronisation à partir d’un dossier de cloud."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 88d3a670-303a-4fa2-9de9-715cc904acec
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: e1c6d53a427c36126d9cdb33cc21b4126b9d9c2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sync-content-from-a-cloud-folder-tooazure-app-service"></a>Contenu de synchronisation à partir d’un tooAzure de dossier du Service d’applications cloud
Ce didacticiel vous montre comment toodeploy trop[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) en synchronisant votre contenu à partir des services de stockage cloud populaires tels que Dropbox et OneDrive. 

## <a name="overview"></a>Vue d’ensemble du déploiement de la synchronisation de contenu
déploiement de la demande de synchronisation de contenu Hello est rendue possible par hello [moteur de déploiement Kudu](https://github.com/projectkudu/kudu/wiki) intégré avec le Service d’applications. Bonjour [Azure Portal](https://portal.azure.com), vous pouvez désigner un dossier dans votre stockage cloud, travailler avec votre code d’application et le contenu dans ce dossier et synchronisation tooApp Service avec hello sur un bouton. Synchronisation de contenu utilise des processus de Kudu hello pour la génération et de déploiement. 

## <a name="contentsync"></a>Déploiement de la synchronisation tooenable contenu
tooenable de synchronisation de contenu à partir de hello [Azure Portal](https://portal.azure.com), procédez comme suit :

1. Dans le panneau de votre application Bonjour portail Azure, cliquez sur **paramètres** > **Source du déploiement**. Cliquez sur **choisir la Source de**, puis sélectionnez **OneDrive** ou **Dropbox** en tant que source de hello pour le déploiement. 
   
    ![Synchronisation de contenu](./media/app-service-deploy-content-sync/deployment_source.png)
   
   > [!NOTE]
   > En raison des différences sous-jacentes Bonjour API, **OneDrive entreprise** n’est pas prise en charge pour l’instant. 
   > 
   > 
2. Hello complète d’autorisation workflow tooenable tooaccess du Service d’applications spécifique prédéfinies chemin d’accès désigné pour OneDrive ou Dropbox où tout votre contenu du Service d’applications sera stocké.  
    Après hello d’autorisation vous donne une plateforme de Service de l’application hello option toocreate un dossier de contenu sous hello désignée chemin d’accès au contenu ou toochoose un dossier de contenu existant dans ce chemin de contenu désigné. les chemins de contenu Hello désigné sous vos comptes de stockage cloud utilisés pour la synchronisation du Service d’applications sont les suivants de hello :  
   
   * **OneDrive** : `Apps\Azure Web Apps` 
   * **Dropbox** : `Dropbox\Apps\Azure`
3. Après avoir hello de synchronisation de contenu hello initiale de synchronisation de contenu peut être lancée à la demande de hello portail Azure. L’historique de déploiement est disponible avec hello **déploiements** panneau.
   
    ![Historique des déploiements](./media/app-service-deploy-content-sync/onedrive_sync.png)

Vous trouverez plus d’informations pour le déploiement Dropbox sous [Déployer à partir de Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx). 

