---
title: "rôles aaaTroubleshoot qui échouent toostart | Documents Microsoft"
description: "Voici quelques-unes des raisons pour lesquelles un rôle de Service Cloud peut échouer toostart. Problèmes de toothese solutions sont également fournies."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 674b2faf-26d7-4f54-99ea-a9e02ef0eb2f
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: e2fbecb08a10984add79dfc74e73de6869bb314f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-service-roles-that-fail-toostart"></a>Résoudre les problèmes de rôle Service de cloud computing toostart
Voici certains problèmes courants et solutions connexes tooAzure Services de cloud computing rôles qui échouent toostart.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-dlls-or-dependencies"></a>DLL ou dépendances manquantes
Les rôles qui ne répondent pas ou qui basculent sans cesse entre les états **Initialisation**, **Occupé** et **Arrêt** peuvent être affectés par l’absence de bibliothèques DLL ou d’assemblys.

Symptômes liés à l’absence de bibliothèques DLL ou d’assemblys :

* Votre instance de rôle alterne entre les états **Initialisation**, **Occupé** et **Arrêt**.
* Votre instance de rôle a été déplacé trop**prêt** , mais si vous naviguez d’application web de tooyour, hello ne s’affiche pas.

Plusieurs méthodes sont recommandées pour rechercher une solution à ces problèmes.

## <a name="diagnose-missing-dll-issues-in-a-web-role"></a>Diagnostiquer les problèmes de DLL manquante dans un rôle web
Lorsque vous accédez tooa site Web déployé dans un rôle web et navigateur de hello affiche un serveur erreur similaires toohello suite, il peut indiquer qu’une DLL est manquante.

![Erreur de serveur dans l’application « / ».](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503388.png)

## <a name="diagnose-issues-by-turning-off-custom-errors"></a>Diagnostiquer les problèmes en désactivant les erreurs personnalisées
Informations plus complètes sur l’erreur sont consultables en configurant web.config hello pour tooOff mode erreurs personnalisées de la tooset rôle hello web hello et de redéployer hello service.

tooview plus complètes que les erreurs sans l’aide du Bureau à distance :

1. Ouvrez la solution de hello dans Microsoft Visual Studio.
2. Bonjour **l’Explorateur de solutions**, recherchez le fichier web.config de hello et ouvrez-le.
3. Dans le fichier web.config hello, localisez la section system.web de hello et ajouter hello ligne suivante :

    ```xml
    <customErrors mode="Off" />
    ```
4. Enregistrez le fichier de hello.
5. Réempaquetez et redéployez hello service.

Une fois que le service de hello est redéployé, vous verrez un message d’erreur de nom hello Hello manquant assembly ou une DLL.

## <a name="diagnose-issues-by-viewing-hello-error-remotely"></a>Diagnostiquer les problèmes en affichant les erreurs hello à distance
Vous pouvez utiliser le rôle de bureau à distance tooaccess hello et afficher des informations plus complètes sur l’erreur à distance. Utilisez hello suivant des erreurs de hello tooview étapes à l’aide du Bureau à distance :

1. Assurez-vous que le Kit de développement logiciel (SDK) Azure 1.3 ou ultérieur est installé.
2. Au cours du déploiement hello de solution hello à l’aide de Visual Studio, choisissez trop « Configurer les connexions Bureau à distance... ». Pour plus d’informations sur la configuration de connexion Bureau à distance de hello, consultez [à l’aide de bureau à distance avec des rôles Azure](../vs-azure-tools-remote-desktop-roles.md).
3. Dans hello classique du portail Microsoft Azure, une fois que l’instance de hello présente l’état de **prêt**, cliquez sur une des instances de rôle hello.
4. Cliquez sur hello **Connect** icône Bonjour **l’accès à distance** zone du ruban de hello.
5. Connectez-vous toohello virtuels à l’aide des informations d’identification hello qui ont été spécifiées lors de la configuration du Bureau à distance hello.
6. Ouvrez une fenêtre de commandes.
7. Saisissez `IPconfig`.
8. Notez la valeur d’adresse IPV4 hello.
9. Ouvrez Internet Explorer.
10. Tapez les adresses hello hello nom et application web de hello. Par exemple, `http://<IPV4 Address>/default.aspx`.

Navigation toohello site Web sera retournent désormais des messages d’erreur plus explicites :

* Erreur de serveur dans l’application « / ».
* Description : Une exception non gérée s’est produite lors de l’exécution de hello de requête web actuelle de hello. Vérifiez la trace de la pile pour plus d’informations sur l’erreur de hello hello et son origine dans le code hello.
* Détails de l’exception : System.IO.FIleNotFoundException : impossible de charger le fichier ou l’assembly « Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35 » ou l’une de ses dépendances. Hello introuvable fichier hello spécifié.

Par exemple :

![Erreur de serveur explicite dans l’application « / »](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503389.png)

## <a name="diagnose-issues-by-using-hello-compute-emulator"></a>Diagnostiquer les problèmes à l’aide d’émulateur de calcul hello
Vous pouvez utiliser hello Microsoft Azure compute emulator toodiagnose et résoudre les problèmes de dépendances manquantes et les erreurs de web.config.

Pour obtenir de meilleurs résultats à l’aide de cette méthode de diagnostic, vous devez utiliser un ordinateur ou une machine virtuelle disposant d’une nouvelle installation de Windows. toobest simuler hello environnement Azure, utilisez Windows Server 2008 R2 x64.

1. Installer la version autonome de hello Hello [Azure SDK](https://azure.microsoft.com/downloads/).
2. Sur l’ordinateur de développement hello, générez le projet de service cloud hello.
3. Dans l’Explorateur Windows, accédez à toohello le dossier bin\debug du projet de service cloud hello.
4. Copier le dossier .csx hello et .cscfg ordinateur toohello que vous utilisez des problèmes de hello toodebug de fichiers.
5. Sur hello propre ordinateur, ouvrez une fenêtre d’invite de commandes du Kit de développement logiciel Azure et tapez `csrun.exe /devstore:start`.
6. À l’invite de commandes hello, tapez `run csrun <path too.csx folder> <path too.cscfg file> /launchBrowser`.
7. Démarrage de rôle de hello, vous verrez des informations d’erreur détaillées dans Internet Explorer. Vous pouvez également utiliser les outils de dépannage standard de Windows toofurther diagnostiquer le problème de hello.

## <a name="diagnose-issues-by-using-intellitrace"></a>Diagnostiquer les problèmes à l’aide d’IntelliTrace
Pour les rôles de travail et les rôles web qui utilisent .NET Framework 4, vous pouvez utiliser l’utilitaire [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), qui est disponible dans Microsoft Visual Studio Enterprise.

Avec IntelliTrace est activé, suivez ces services de hello toodeploy comme suit :

1. Vérifiez que le Kit de développement logiciel (SDK) Azure 1.3 ou ultérieur est installé.
2. Déployer la solution de hello à l’aide de Visual Studio. Pendant le déploiement, vérifiez hello **activer IntelliTrace pour les rôles .NET 4** case à cocher.
3. Une fois que le démarrage de l’instance de hello, ouvrez hello **l’Explorateur de serveurs**.
4. Développez hello **Azure\\Services de cloud computing** nœud et recherchez hello déploiement.
5. Étendre les déploiements de hello jusqu'à ce que les instances de rôle hello. Avec le bouton droit sur une des instances de hello.
6. Sélectionnez **Afficher les fichiers journaux IntelliTrace**. Hello **résumé IntelliTrace** s’ouvre.
7. Localiser la section exceptions hello hello résumé. S’il existe des exceptions, la section de hello est étiquetée **données d’Exception**.
8. Développez hello **données d’Exception** et recherchez **System.IO.FileNotFoundException** suivant de toohello erreurs similaires :

![Données d’exception, fichier ou assembly manquant](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503390.png)

## <a name="address-missing-dlls-and-assemblies"></a>Résoudre les problèmes de DLL et d’assemblys manquants
tooaddress manquant des erreurs de DLL et d’assembly, procédez comme suit :

1. Ouvrez la solution de hello dans Visual Studio.
2. Dans **l’Explorateur de solutions**, ouvrez hello **références** dossier.
3. Cliquez sur assembly hello identifié dans l’erreur de hello.
4. Bonjour **propriétés** volet, recherchez **propriété copie locale** et la valeur hello trop**True**.
5. Redéployez le service de cloud computing hello.

Une fois que vous avez vérifié que toutes les erreurs ont été corrigées, vous pouvez déployer le service de hello sans vérification hello **activer IntelliTrace pour les rôles .NET 4** case à cocher.

## <a name="next-steps"></a>Étapes suivantes
Affichez plus d’ [articles de résolution des problèmes](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) liés aux services cloud.

toolearn comment le rôle du service cloud tootroubleshoot problèmes à l’aide de données de diagnostic d’ordinateur PaaS Azure, consultez [série du blog de Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).
