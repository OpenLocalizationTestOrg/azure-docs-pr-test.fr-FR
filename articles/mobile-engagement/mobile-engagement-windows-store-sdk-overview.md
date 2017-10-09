---
title: "aaaAzure intégration du Kit de développement logiciel Universal Mobile Engagement Windows | Documents Microsoft"
description: "Intégration de Windows Universal pour le Kit de développement logiciel (SDK) pour Azure Engagement Mobile"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 9ded187d-5c07-4377-a41c-ce205dd38b50
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 11/03/2016
ms.author: piyushjo
ms.openlocfilehash: 2f88e58adb349a2a4eb43b0f182f99b3e8b8cfd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-sdk-integration-for-azure-mobile-engagement"></a>Intégration du Kit de développement logiciel (SDK) Windows Universal pour Azure Engagement Mobile
Ce document décrit tous les hello intégration et configuration options disponibles pour hello SDK universelle de Windows Azure Mobile Engagement.

## <a name="prerequisites"></a>Composants requis
Avant de commencer ce didacticiel, vous devez suivre notre [didacticiel de 15 minutes](mobile-engagement-windows-store-dotnet-get-started.md).

## <a name="advanced-features"></a>Fonctionnalités avancées
### <a name="reporting-features"></a>Fonctionnalités de génération de rapports
Vous pouvez ajouter les fonctionnalités suivantes :

1. [Options de génération de rapports avancés](mobile-engagement-windows-store-advanced-reporting.md)
2. [Options de configuration avancées](mobile-engagement-windows-store-advanced-configuration.md)

### <a name="notifications"></a>Notifications
[Comment toointegrate portée (Notifications) dans votre application Windows universelle](mobile-engagement-windows-store-integrate-engagement-reach.md)

### <a name="tag-plan-implementation"></a>Implémentation du plan de balise :
[Comment toouse hello avancé Mobile Engagement marquage API dans votre application Windows universelle](mobile-engagement-windows-store-use-engagement-api.md)

## <a name="release-notes"></a>Notes de publication
### <a name="341-11032016"></a>3.4.1 (11/03/2016)

* Améliorations de la stabilité.

Pour les versions antérieures, consultez hello [terminer les notes de publication](mobile-engagement-windows-store-release-notes.md)

## <a name="upgrade-procedures"></a>Procédures de mise à niveau
Si vous avez déjà intégré une version antérieure d’implication dans votre application, vous avez hello tooconsider hello Kit de développement logiciel de la mise à niveau les points suivants.

Si vous avez manqué plusieurs versions du Kit de développement logiciel de hello, vous avez peut-être toofollow plusieurs procédures. Consultez hello complète [mise à niveau des procédures](mobile-engagement-windows-store-upgrade-procedure.md). Par exemple, si vous migrez à partir de 0.10.1 too0.11.0 avoir toofirst suivez hello » à partir de 0.9.0 too0.10.1 « procédure puis hello » à partir de 0.10.1 too0.11.0 « procédure.

### <a name="from-330-too340"></a>À partir de 3.3.0 too3.4.0
#### <a name="test-logs"></a>Journaux des tests
Journaux de la console produits par hello SDK peuvent être activé/désactivé/filtrées. toocustomize, propriété hello de mise à jour `EngagementAgent.Instance.TestLogEnabled` tooone de valeurs hello disponibles à partir de hello `EngagementTestLogLevel` énumération, par exemple :

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

#### <a name="resources"></a>Ressources
segment de recouvrement Hello portée a été améliorée. Il fait partie des ressources de package NuGet du Kit de développement logiciel hello.

Lors de la mise à niveau toohello une nouvelle version du Kit de développement logiciel de hello, vous pouvez choisir que si vous souhaitez tookeep vos fichiers à partir de hello superposition dossier des ressources ou non :

* Si le segment de recouvrement hello précédent fonctionne pour vous, ou vous intégrez hello `WebView` éléments manuellement, vous pouvez choisir ensuite tookeep votre sortie de fichiers, il continuera de fonctionner.
* tooupdate toohello nouveau segment de recouvrement, hello remplacer toute `overlay` dossier à partir de vos ressources avec hello nouveau à partir du package SDK de hello (applications UWP : après la mise à niveau de hello, vous pouvez obtenir le nouveau dossier de superposition hello à partir de % USERPROFILE%\\.nuget\packages\ MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).

> [!WARNING]
> À l’aide de la superposition de nouveau hello remplace les personnalisations effectuées sur la version précédente de hello.
> 
> 

### <a name="upgrade-from-older-versions"></a>Mise à niveau à partir de versions antérieures
Consultez la rubrique [Procédures de mise à niveau](mobile-engagement-windows-store-upgrade-procedure.md)

