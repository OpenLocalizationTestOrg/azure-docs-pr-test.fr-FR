---
title: "aaaDebugging un rapport publié un Azure cloud service avec Visual Studio et IntelliTrace | Documents Microsoft"
description: "Découvrez comment toodebug un cloud service avec Visual Studio et d’IntelliTrace"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5e6662fc-b917-43ea-bf2b-4f2fc3d213dc
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 60734a71d5499de72e1ca81a3ab0ab9f34bc303a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-a-published-azure-cloud-service-with-visual-studio-and-intellitrace"></a>Débogage d’un service cloud Azure publié avec Visual Studio et IntelliTrace
Avec IntelliTrace, vous pouvez enregistrer des informations de débogage détaillées pour une instance de rôle exécutée dans Azure. Si vous avez besoin d’origine de hello toofind d’un problème, vous pouvez utiliser toostep de journaux IntelliTrace hello dans votre code à partir de Visual Studio comme s’il s’exécutait dans Azure. En effet, IntelliTrace enregistre code de touche d’exécution et l’environnement les données lorsque votre application Azure s’exécute comme un service cloud dans Azure et vous permet de relire les données de hello enregistrée à partir de Visual Studio. 

Vous pouvez utiliser IntelliTrace si Visual Studio Enterprise est installé et que votre application Azure cible .NET Framework 4 ou une version ultérieure. IntelliTrace collecte des informations pour vos rôles Azure. machines virtuelles de Hello pour ces rôles s’exécutent toujours des systèmes d’exploitation 64 bits.

En guise d’alternative, vous pouvez utiliser [débogage distant](http://go.microsoft.com/fwlink/p/?LinkId=623041) tooattach directement les service de cloud de tooa qui s’exécute dans Azure.

> [!IMPORTANT]
> IntelliTrace est conçu uniquement pour des scénarios de débogage et ne doit pas être utilisé dans le cadre d’un déploiement de production.
> 

## <a name="configure-an-azure-application-for-intellitrace"></a>Configurer une application Azure pour IntelliTrace
tooenable IntelliTrace pour une application Windows Azure, vous devez créer et publier l’application hello à partir d’un projet Windows Azure Visual Studio. Avant de le publier tooAzure, vous devez configurer IntelliTrace pour votre application Windows Azure. Si vous publiez votre application sans configurer IntelliTrace, vous devez le projet de hello toorepublish. Pour plus d’informations, voir [Publication d’un projet Azure Cloud Services à l’aide de Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623012).

1. Lorsque vous êtes prêt à toodeploy votre application Windows Azure, vérifiez que votre projet cible de build est trop**déboguer**.

1. Dans **l’Explorateur de solutions**, cliquez sur le projet et, dans le menu contextuel de hello, sélectionnez **publier**.
   
1. Bonjour **publier l’Application Azure** boîte de dialogue, sélectionnez hello abonnement Azure, puis sélectionnez **suivant**.

1. Bonjour **paramètres** page, sélectionnez hello **paramètres avancés** onglet.

1. Activer hello **activer IntelliTrace** option toocollect les fichiers journaux IntelliTrace pour votre application lorsqu’elle est publiée dans le cloud de hello.
   
1. toocustomize hello IntelliTrace configuration de base, sélectionnez **paramètres** suivant trop**activer IntelliTrace**.

    ![Lien Paramètres IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/intellitrace-settings-link.png)
   
1. Bonjour **paramètres IntelliTrace** boîte de dialogue, vous pouvez spécifier le toolog d’événements, si toocollect informations sur les appels, le toocollect modules et processus ouvre une session, la quantité d’espace tooallocate toohello enregistrement et. Pour plus d’informations sur IntelliTrace, consultez [Débogage avec IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=214468).
   
    ![Paramètres IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC519063.png)

fichier journal IntelliTrace Hello est un fichier journal circulaire de taille maximale de hello spécifié dans les paramètres IntelliTrace hello (taille de hello par défaut est 250 Mo). Les fichiers journaux IntelliTrace sont collectés tooa fichier hello système de fichiers d’ordinateur virtuel de hello. Lorsque vous demandez les journaux hello, un instantané est effectuée à ce stade dans le temps et téléchargé tooyour les ordinateur local.

Une fois hello service cloud Azure a été publiée tooAzure, vous pouvez déterminer si IntelliTrace a été activé à partir de hello Azure nœud dans **l’Explorateur de serveurs**, comme indiqué dans hello suivant image :

![Explorateur de serveurs - IntelliTrace activé](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC744134.png)

## <a name="download-intellitrace-logs-for-a-role-instance"></a>Télécharger les journaux IntelliTrace pour une instance de rôle
À l’aide de Visual Studio, vous pouvez télécharger les journaux IntelliTrace pour une instance de rôle en procédant comme suit :

1. Dans **l’Explorateur de serveurs**, développez hello **Services de cloud computing** nœud, puis recherchez l’instance de rôle dont vous souhaitez toodownload les journaux. 

1. Droit d’instance de rôle hello sur, puis dans le menu contextuel de hello s, sélectionnez **afficher les journaux IntelliTrace**. 

    ![Option de menu Afficher les fichiers journaux IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/view-intellitrace-logs.png)

1. les fichiers journaux IntelliTrace Hello sont tooa téléchargé les fichiers dans un répertoire sur votre ordinateur local. Chaque fois que vous demandez les journaux IntelliTrace hello, un nouvel instantané est créé. Pendant le téléchargement des journaux de hello, Visual Studio affiche la progression de hello d’opération de hello dans hello **journal des activités Azure** fenêtre. Comme indiqué dans la figure suivante de hello, vous pouvez développer hello élément hello opération toosee plus en détail.

![VST_IntelliTraceDownloadProgress](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC745551.png)

Vous pouvez continuer toowork dans Visual Studio pendant le téléchargement des fichiers journaux IntelliTrace hello. Lorsque le journal de hello a terminé le téléchargement, il s’ouvre dans Visual Studio.

> [!NOTE]
> Hello les fichiers journaux IntelliTrace peuvent contenir des exceptions qui framework hello génère et gère par la suite. Le code de l’infrastructure interne génère ces exceptions dans le cadre normal du démarrage d’un rôle. Vous pouvez donc les ignorer en toute sécurité.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
- [Options de débogage d’Azure Cloud Services](vs-azure-tools-debugging-cloud-services-overview.md)
- [Publication d’un service cloud Azure à l’aide de Visual Studio](vs-azure-tools-publishing-a-cloud-service.md)