---
title: "aaaUsing hello Visual Studio Assistant Publication d’Azure Application | Documents Microsoft"
description: "Découvrez comment tooconfigure hello divers paramètres Bonjour publier Azure Application Assistant de Visual Studio"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7d8f1ac9-e439-47e0-a183-0642c4ea1920
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 3f0b580d0054cc246372597660d8ae317d9b8686
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-visual-studio-publish-azure-application-wizard"></a>À l’aide de Visual Studio Assistant Publication d’Azure Application de hello
Après avoir développé une application web dans Visual Studio, vous pouvez publier ce tooan application service cloud Azure à l’aide de hello **publier l’Application Azure** Assistant. 

> [!NOTE]
> Cette rubrique est sur le déploiement de services toocloud, pas les sites tooweb. Pour plus d’informations sur le déploiement de sites de tooweb, consultez [comment tooDeploy un Site Web Azure](https://social.msdn.microsoft.com/Search/windowsazure?query=How%20to%20Deploy%20an%20Azure%20Web%20Site&Refinement=138&ac=4#refinementChanges=117&pageNumber=1&showMore=false).
> 
> 

## <a name="accessing-hello-publish-azure-application-wizard"></a>L’accès à Assistant de publication d’Application Azure hello

Vous pouvez accéder à Assistant de publier l’Application Azure hello de deux manières en fonction de type hello de projet Visual Studio que vous avez.

**Si vous avez un projet de service cloud Azure :**

1. Créez ou ouvrez un projet de service cloud Azure dans Visual Studio.

1. Dans **l’Explorateur de solutions**, cliquez sur le projet de hello et, dans le menu contextuel de hello, sélectionnez **publier**.

**Si vous avez un projet d’application web qui n’est pas activé pour Azure :**

1. Créez ou ouvrez un projet de service cloud Azure dans Visual Studio.

1. Dans **l’Explorateur de solutions**, cliquez sur le projet de hello et, dans le menu contextuel de hello, sélectionnez **convertir** > **convertir tooAzure projet de Service Cloud**. 

1. Dans **l’Explorateur de solutions**, avec le bouton droit de projet Windows Azure de hello qui vient d’être créé et, à partir du menu contextuel de hello, sélectionnez **publier**.

## <a name="sign-in-page"></a>page de connexion

![page de connexion](./media/vs-azure-tools-publish-azure-application-wizard/sign-in.png)

**Compte** - sélectionnez un compte ou **ajouter un compte** dans la liste déroulante de compte hello.

**Choisissez votre abonnement** -choisissez toouse d’abonnement hello pour votre déploiement.
   
## <a name="settings-page---common-settings-tab"></a>Page Paramètres - Onglet Paramètres communs   

![Paramètres courants](./media/vs-azure-tools-publish-azure-application-wizard/settings-common-settings.png)

**Service de cloud computing** -à l’aide de la liste déroulante de hello, sélectionnez un cloud existant service, ou sélectionnez  **&lt;créer un nouveau >**et créer un service cloud. Centre de données Hello s’affiche entre parenthèses pour chaque service cloud. Il est recommandé que hello emplacement du centre de données pour être hello service cloud hello même en tant qu’emplacement de centre de données hello pour le compte de stockage hello (paramètres avancés).  

**Environnement** : sélectionnez **Production** ou **Intermédiaire**. Choisissez hello environnement intermédiaire si vous souhaitez toodeploy votre application dans un environnement de test. 

**Configuration de build** : sélectionnez **Déboguer** ou **Version finale**.

**Configuration de service** : sélectionnez **Cloud** ou **Local**.
   
**Activer le Bureau à distance pour tous les rôles** -Vérifiez que cette option si vous souhaitez toobe les tooremotely en mesure de se connecter toohello service. Cette option est principalement utilisée pour le dépannage. Lorsque vous sélectionnez cette case à cocher, hello **Configuration Bureau à distance** boîte de dialogue s’affiche. Choisissez hello **paramètres** configuration hello toochange du lien.
   
**Activer Web Deploy pour tous les rôles web** -vérifier cette option, le déploiement de web tooenable pour le service de hello. Vous devez sélectionner hello **activer le Bureau à distance pour tous les rôles** option toouse cette fonctionnalité. Pour plus d’informations, consultez [[Publishing a Azure cloud service using Visual Studio (Publication d’un service cloud Azure à l’aide de Visual Studio)](https://msdn.microsoft.com/library/azure/ff683672.aspx)](https://msdn.microsoft.com/library/azure/ff683672.aspx). 

## <a name="settings-page---advanced-settings-tab"></a>Page Paramètres - Onglet Paramètres avancés

![Paramètres avancés](./media/vs-azure-tools-publish-azure-application-wizard/settings-advanced-settings.png)

**Étiquette de déploiement** -acceptez le nom par défaut de hello, ou entrez un nom de votre choix. tooappend hello date toohello étiquette de déploiement, laissez le champ hello case à cocher. 
   
**Compte de stockage** : sélectionnez hello toouse de compte de stockage pour ce déploiement, **&lt;créer un nouveau > toocreate un compte de stockage. Centre de données Hello s’affiche entre parenthèses pour chaque compte de stockage. Il est recommandé que hello emplacement du centre de données pour être hello compte de stockage hello même en tant qu’emplacement de centre de données hello pour le service cloud hello (paramètres courants).  
   
Hello compte de stockage Azure stocke le package hello pour le déploiement de l’application hello. Après le déployée de l’application hello, package de hello est supprimé à partir du compte de stockage hello.

**Supprimer le déploiement en cas d’échec** -Sélectionnez ce déploiement de hello toohave option supprimé si des erreurs se produisent lors de la publication. Cela doit être désactivée si vous souhaitez toomaintain une adresse IP virtuelle constante pour votre service cloud.

**Mise à jour de déploiement** -Sélectionnez cette option si vous souhaitez toodeploy mise à jour uniquement les composants. Ce type de déploiement peut être plus rapide qu'un déploiement complet. Cela doit être vérifiée si vous souhaitez toomaintain une adresse IP virtuelle constante pour votre service cloud. 

**Mise à jour de déploiement - paramètres** -sert de cette boîte de dialogue toofurther Indiquez de quelle manière hello rôles toobe est mis à jour. Si vous choisissez **mise à jour incrémentielle**, chaque instance de votre application est mis à jour après l’autre, afin que cette application hello soit toujours disponible. Si vous choisissez **mise à jour simultanée**, toutes les instances de votre application sont mises à jour à hello même temps. Mise à jour simultanée est plus rapide, mais votre service ne soient pas disponible pendant le processus de mise à jour hello. 

![Paramètres de déploiement](./media/vs-azure-tools-publish-azure-application-wizard/deployment-settings.png)

**Activer IntelliTrace** -spécifier si vous voulez tooenable IntelliTrace. Avec IntelliTrace, vous pouvez enregistrer des informations de débogage détaillées pour une instance de rôle exécutée dans Azure. Si vous avez besoin d’origine de hello toofind d’un problème, vous pouvez utiliser toostep de journaux IntelliTrace hello dans votre code à partir de Visual Studio comme s’il s’exécutait dans Azure. Pour plus d’informations sur l’utilisation d’IntelliTrace, consultez l’article [Débogage d’un service cloud publié avec IntelliTrace et Visual Studio](./vs-azure-tools-intellitrace-debug-published-cloud-services.md). 

**Activer le profilage** -spécifiez si vous souhaitez que le profilage des performances tooenable. Générateur de profils Visual Studio Hello permet tooget une analyse approfondie des aspects de calcul de hello de la façon dont votre service cloud s’exécute. Pour plus d’informations sur l’utilisation du Générateur de profils Visual Studio hello, consultez [tester les performances de hello d’un service cloud Azure](./vs-azure-tools-performance-profiling-cloud-services.md).

**Activer le débogueur distant pour tous les rôles** -spécifier si vous voulez tooenable le débogage distant. Pour plus d’informations sur le débogage des services cloud à l’aide de Visual Studio, consultez l’article [Débogage d’un service cloud ou d’une machine virtuelle Azure dans Visual Studio](./vs-azure-tools-debug-cloud-services-virtual-machines.md).

## <a name="diagnostics-settings-page"></a>Page Paramètres de diagnostic

![Paramètres de diagnostic](./media/vs-azure-tools-publish-azure-application-wizard/diagnostic-settings.png)

Diagnostics vous permet de tootroubleshoot un service cloud Azure (ou une machine virtuelle Azure). Pour en savoir plus sur les diagnostics, consultez [Configuration de Diagnostics pour les services cloud et les machines virtuelles Azure](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md). Pour plus d’informations sur Application Insights, consultez [Présentation d’Application Insights](./application-insights/app-insights-overview.md).

## <a name="summary-page"></a>Page de résumé

![Résumé](./media/vs-azure-tools-publish-azure-application-wizard/summary.png)

**Cibler profile** -vous pouvez choisir un profil de publication toocreate à partir des paramètres hello que vous avez choisi. Par exemple, vous pouvez créer un profil pour un environnement de test et un autre pour la production. toosave ce profil, choisissez hello **enregistrer** icône. Assistant de Hello crée un profil de hello et l’enregistre dans un projet de Visual Studio hello. nom du profil toomodify hello, ouvrez hello **cibler profile** liste, puis choisissez **< gérer... >**.
   
   > [!NOTE]
   > profil de publication Hello s’affiche dans l’Explorateur de solutions dans Visual Studio, et les paramètres de profil hello sont écrites tooa les fichiers portant l’extension .azurePubxml. Les paramètres sont enregistrés en tant qu'attributs de balises XML.
   > 
   > 

## <a name="publishing-your-application"></a>Publication de votre application

Une fois que vous configurez tous les paramètres de hello pour le déploiement de votre projet, sélectionnez **publier** bas hello de boîte de dialogue hello. Vous pouvez surveiller le statut du processus hello Bonjour **sortie** fenêtre dans Visual Studio.

## <a name="next-steps"></a>Étapes suivantes
- [Migrer et publier une Application Web de tooan service cloud Azure depuis Visual Studio](./vs-azure-tools-migrate-publish-web-app-to-cloud-service.md)
- [Découvrez comment toouse Visual Studio toopublish Azure cloud service](./vs-azure-tools-publishing-a-cloud-service.md)
- [Débogage d’un service cloud publié avec IntelliTrace et Visual Studio](./vs-azure-tools-intellitrace-debug-published-cloud-services.md)
- [Tester les performances d’un service cloud Azure hello](./vs-azure-tools-performance-profiling-cloud-services.md)
- [Configuration de Diagnostics pour les services cloud et les machines virtuelles Azure](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) 
- [Présentation d’Application Insights](./application-insights/app-insights-overview.md)