---
title: "aaaCommon provoque des rôles de Service Cloud recyclage | Documents Microsoft"
description: "Le recyclage soudain d’un rôle de service cloud peut entraîner d’importants temps d’arrêt. Voici quelques problèmes courants qui provoquent toobe rôles recyclé, ce qui peut aider à réduire le temps mort."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 533930d1-8035-4402-b16a-cf887b2c4f85
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 8fa152b33d2b22a8a02f834d4bc38519b4272f7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="common-issues-that-cause-roles-toorecycle"></a>Problèmes courants pouvant provoquer des rôles toorecycle
Cet article présente certaines des causes courantes de hello des problèmes de déploiement et fournit la résolution des problèmes de conseils toohelp vous résolvez ces problèmes. Indique qu’un problème existe avec une application est lorsque l’instance de rôle hello échoue toostart, ou lorsqu’elle bascule entre les États initialisation, occupé et arrêt hello.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-runtime-dependencies"></a>Dépendances d'exécution manquantes
Si un rôle dans votre application s’appuie sur un assembly qui ne fait pas partie de hello bibliothèque managée de .NET Framework ou hello Azure, vous devez inclure explicitement cet assembly dans le package d’application hello. N'oubliez pas que les autres infrastructures Microsoft ne sont pas disponibles par défaut dans Azure. Si votre rôle repose sur une telle infrastructure, vous devez ajouter le package d’application ces assemblys toohello.

Avant de générer et empaqueter votre application, vérifiez les suivant hello :

* Si vous utilisez Visual studio, assurez-vous que hello **copie locale** propriété a la valeur trop**True** pour chaque assembly dans votre projet qui ne fait pas partie de hello Azure SDK référencé ou hello .NET Framework.
* Assurez-vous que le fichier web.config de hello ne fait pas référence à tous les assemblys inutilisés dans l’élément de compilation hello.
* Hello **Action de génération** de chaque .cshtml fichier est défini trop**contenu**. Cela garantit que les fichiers hello s’affichent correctement dans le package de hello et permet des autres tooappear fichiers référencés dans le package de hello.

## <a name="assembly-targets-wrong-platform"></a>L’assembly cible la mauvaise plateforme
Azure est un environnement 64 bits. Par conséquent, les assemblys .NET compilés pour une cible 32 bits ne fonctionneront pas sur Azure.

## <a name="role-throws-unhandled-exceptions-while-initializing-or-stopping"></a>Le rôle génère des exceptions non gérées lors de l'initialisation ou de l'arrêt
Toutes les exceptions levées par des méthodes hello Hello [RoleEntryPoint] (classe), qui inclut hello [OnStart], [OnStop], et [exécuter]méthodes, sont des exceptions non gérées. Si une exception non gérée se produit dans un de ces méthodes, le rôle de hello sera recyclé. Si le rôle de hello est recyclé de façon répétée, il peut lever une exception non gérée chaque fois qu’il tentera de toostart.

## <a name="role-returns-from-run-method"></a>Le rôle est renvoyé à partir de la méthode Run
Hello [exécuter] méthode est prévue toorun indéfiniment. Si votre code remplace hello [exécuter] (méthode), il doit être en veille indéfiniment. Si hello [exécuter] méthode est retournée, hello rôle est recyclé.

## <a name="incorrect-diagnosticsconnectionstring-setting"></a>Chaîne DiagnosticsConnectionString incorrecte
Si l’application utilise des Diagnostics Windows Azure, votre fichier de configuration de service doit spécifier hello `DiagnosticsConnectionString` paramètre de configuration. Ce paramètre doit spécifier un compte de stockage tooyour connexion HTTPS dans Azure.

tooensure que votre `DiagnosticsConnectionString` paramètre est correct avant de déployer votre tooAzure de package d’application, vérifiez hello suivantes :  

* Hello `DiagnosticsConnectionString` définissant des points de compte de stockage valide tooa dans Azure.  
  Par défaut, ce paramètre pointe compte de stockage toohello émulée, donc vous devez modifier explicitement ce paramètre avant de déployer votre package d’application. Si vous ne modifiez pas ce paramètre, une exception est levée lorsque l’instance de rôle hello tente de moniteur de diagnostic toostart hello. Cela peut entraîner hello rôle instance toorecycle indéfiniment.
* chaîne de connexion Hello est spécifiée dans les suivant hello [format](../storage/common/storage-configure-connection-string.md). (le protocole de hello doit être spécifié en tant que HTTPS). Remplacez *MyAccountName* avec nom hello de votre compte de stockage et *MyAccountKey* avec votre clé d’accès :    

        DefaultEndpointsProtocol=https;AccountName=MyAccountName;AccountKey=MyAccountKey

  Si vous développez votre application à l’aide de Windows Azure Tools pour Microsoft Visual Studio, vous pouvez utiliser cette valeur tooset de pages de propriété hello.

## <a name="exported-certificate-does-not-include-private-key"></a>Le certificat exporté ne contient aucune clé privée
toorun un rôle web sous SSL, vous devez vous assurer que votre certificat de gestion exporté inclut la clé privée de hello. Si vous utilisez hello *Gestionnaire de certificats Windows* tooexport certificat de hello, être vraiment tooselect **Oui** pour hello **clé privée de hello exportation** option. certificat de Hello doit être exporté au format PFX hello, qui est hello seul format pris en charge actuellement.

## <a name="next-steps"></a>Étapes suivantes
Affichez plus d’ [articles de résolution des problèmes](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) liés aux services cloud.

Affichez d’autres scénarios de recyclage des rôles dans la [série du blog de Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).

[RoleEntryPoint]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx
[OnStart]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx
[OnStop]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx
[exécuter]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx
