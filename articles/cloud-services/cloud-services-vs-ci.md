---
title: remise aaaContinuous pour cloud services avec Visual Studio Online | Documents Microsoft
description: "Découvrez comment tooset de livraison continue pour Azure cloud applications sans enregistrer les fichiers de configuration de service de clés toohello stockage de diagnostics"
services: cloud-services
documentationcenter: 
author: cawa
manager: paulyuk
editor: 
ms.assetid: 148b2959-c5db-4e4a-a7e9-fccb252e7e8a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/02/2016
ms.author: cawa
ms.openlocfilehash: dc87d049e46daf8b8a26ee4450ebd9b7910f287b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="securely-save-cloud-services-diagnostics-storage-key-and-setup-continuous-integration-and-deployment-tooazure-using-visual-studio-online"></a>Securely enregistrer Services Diagnostics clé de stockage Cloud et tooAzure d’intégration continue du programme d’installation et de déploiement à l’aide de Visual Studio Online
 Il est aujourd'hui un communes des projets sources pratique tooopen. L’enregistrement des secrets de l’application dans les fichiers de configuration n’est plus sûr, dans la mesure où des failles de sécurité peuvent provoquer la révélation des secrets à partir des contrôles de code source publics. Le stockage de clé secrète comme texte en clair dans un fichier dans un pipeline de l’intégration continue n’est pas sécurisé soit depuis les serveurs de build peut être ressources partagées sur un environnement de Cloud hello. Cet article explique comment Visual Studio et Visual Studio Online permet d’atténuer les problèmes de sécurité hello pendant le développement et le processus d’intégration continue.

## <a name="remove-diagnostics-storage-key-secret-in-project-configuration-file"></a>Supprimer le secret de clé de stockage de diagnostic dans le fichier de configuration de projet
L’extension des diagnostics des services cloud nécessite un stockage Azure pour l’enregistrement des résultats des diagnostics. Auparavant, chaîne de connexion de stockage hello est spécifié dans les fichiers de configuration (.cscfg) de Services de cloud computing hello et peut être activé dans le contrôle de toosource. Dans la dernière version de Windows Azure SDK hello, nous avons modifié du store tooonly hello comportement un partielle chaîne de connexion avec la clé hello remplacé par un jeton. Hello comme suit décrire le fonctionnement des outils de Services de cloud computing hello nouvelle :

### <a name="1-open-hello-role-designer"></a>1. Ouvrez le Concepteur de rôle hello
* Double-cliquez sur ou cliquez avec le bouton droit sur un concepteur de rôle Services de cloud computing rôle tooopen

![Ouvrez le Concepteur de rôle][0]

### <a name="2-under-diagnostics-section-a-new-check-box-dont-remove-storage-key-secret-from-project-is-added"></a>2. Dans la section Diagnostics, une nouvelle case à cocher « Ne pas supprimer le secret de clé de stockage du projet » a été ajoutée.
* Si vous utilisez l’émulateur de stockage local hello, cette case à cocher est désactivée, car il n’existe aucun secret toomanage pour la chaîne de connexion locale hello, qui est UseDevelopmentStorage = true.

![La chaîne de connexion de l’émulateur de stockage local n’est pas secrète][1]

* Si vous créez un nouveau projet, cette case est désactivée par défaut. Ainsi, dans la section de clé de stockage hello de chaîne de connexion de stockage hello sélectionné qui est remplacé par un jeton. Hello valeur du jeton de hello trouverez sous le dossier AppData itinérant de l’utilisateur actuel hello, par exemple : C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService

> Notez le dossier user\AppData hello est l’accès contrôlé par la connexion d’utilisateur et est considéré comme un emplacement sécurisé toostore les secrets de développement.
> 
> 

![La clé de stockage est enregistrée dans le dossier du profil utilisateur][2]

### <a name="3-select-a-diagnostics-storage-account"></a>3. Sélectionnez un compte de stockage de diagnostics
* Sélectionnez un compte de stockage à partir de la boîte de dialogue hello lancé en cliquant sur hello «... » . Notez la chaîne de connexion de stockage hello généré ne disposera de clé de compte de stockage hello.
* Par exemple : DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)

### <a name="4----debugging-hello-project"></a>4.    Débogage du projet de hello
* F5 toostart de débogage dans Visual Studio. Tout doit fonctionner dans hello même façon qu’avant.
  ![Démarrer le débogage local][3]

### <a name="5-publish-project-from-visual-studio"></a>5. Publier un projet à partir de Visual Studio
* Lancement hello boîte de dialogue Publier et poursuivre les instructions de connexion toopublish hello applicaion tooAzure.

### <a name="6-additional-information"></a>6. Informations supplémentaires
> Remarque : panneau des paramètres dans le Concepteur de rôle hello hello resteront car il n’est pour l’instant. Si vous souhaitez la fonctionnalité de gestion des secrets toouse hello pour les diagnostics, accédez à onglet Configurations de toohello.
> 
> 

![Ajouter des paramètres][4]

> Remarque : Si activé, clé d’Application Insights hello sera stocké en tant que texte brut. Hello clé est uniquement utilisée pour télécharger contenu est donc aucune donnée sensible au risque de compromission.
> 
> 

## <a name="build-and-publish-a-cloud-services-project-using-visual-studio-online-task-templates"></a>Créer et publier un projet de service cloud à l’aide des modèles de tâches en ligne Visual Studio
* Hello qui suit illustre comment toosetup intégration continue pour les Services de cloud computing de projet à l’aide de tâches en ligne de Visual Studio :
  ### <a name="1----obtain-a-vso-account"></a>1.    Obtenir un compte VSO
* [Créer le compte Visual Studio Online] [ Create Visual Studio Online account] si vous n’avez pas déjà
* [Créer le projet d’équipe] [ Create team project] dans votre compte en ligne de Visual Studio

### <a name="2----setup-source-control-in-visual-studio"></a>2.    Configurer le contrôle de code source dans Visual Studio
* Connecter le projet d’équipe tooa

![Connecter tooteam projet][5]

![Sélectionnez tooconnect de projet d’équipe à][6]

* Ajouter votre contrôle toosource de projet

![Ajouter le contrôle toosource du projet][7]

![Mapper le dossier de contrôle de projet tooa source][8]

* Archivez votre projet à partir de Team Explorer

![Vérifiez dans le projet de contrôle de toosource][9]

### <a name="3----configure-build-process"></a>3.    Configurer le processus de génération
* Parcourir le projet d’équipe tooyour et ajouter un processus de génération de nouveaux modèles

![Ajoutez une nouvelle génération][10]

* Sélectionnez une tâche de génération

![Ajoutez une tâche de génération][11]

![Sélectionnez le modèle de tâche de génération Visual Studio][12]

* Modifiez l’entrée de tâche de génération. Veuillez personnaliser build hello paramètres selon tooyour doivent

![Configurez la tâche de génération][13]

`/t:Publish /p:TargetProfile=$(targetProfile) /p:DebugType=None /p:SkipInvalidConfigurations=true /p:OutputPath=bin\ /p:PublishDir="$(build.artifactstagingdirectory)\\"`

* Configurez les variables de génération

![Configurez les variables de génération][14]

* Ajouter une cible de build tooupload tâche

![Choisissez de publier la tâche de cible de génération][15]

![Configurez la publication de la tâche de cible de génération][16]

* Exécutez hello build

![Mettez la nouvelle génération en file d’attente][17]

![Affichez le résumé de génération][18]

* Si la génération de hello est réussie, vous verrez un toobelow similaire de résultat

![Résultat de la génération][19]

### <a name="4----configure-release-process"></a>4.    Configurez un processus de publication
* Créez une nouvelle version

![Créez une nouvelle version][20]

* Sélectionnez la tâche de déploiement des Services Cloud Azure hello

![Sélectionnez la tâche de déploiement des services cloud Azure][21]

* Comme la clé de compte de stockage hello n’est pas activée dans le contrôle toosource, nous devons toospecify une clé secrète hello pour la définition d’extensions de diagnostic. Développez hello **des Options avancées pour la création d’un Service** section et modifier hello **clés de compte de stockage de Diagnostics** entrée de paramètre. Cette entrée utilise plusieurs lignes de la paire clé / valeur au format hello de **[RoleName]:$(StorageAccountKey)**

> Remarque : Si votre compte de stockage est sous de diagnostics hello même abonnement qu’où vous allez publier l’application de Services de cloud computing hello, vous ne disposez tooenter hello clé dans l’entrée de tâche de déploiement hello ; déploiement de Hello récupèrera par programmation les informations de stockage hello à partir de votre abonnement
> 
> 

![Configurez la tâche de déploiement des services cloud][22]

* Secret de l’utilisation de variables toosave build clés de stockage. entrée de Variables toomask une variable en tant que secret sur l’icône de verrou hello sur le côté droit de hello Hello

![Enregistrez les clés de stockage dans les variables de génération secrètes][23]

* Créez une version et de déployer votre tooAzure de projet

![Créez une nouvelle version][24]

## <a name="next-steps"></a>Étapes suivantes
toolearn en savoir plus sur la définition d’extensions de diagnostic pour les Services de Cloud Azure, consultez [activer les diagnostics dans Azure Cloud Services à l’aide de PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]

[Create Visual Studio Online account]:https://www.visualstudio.com/team-services/
[Create team project]: https://www.visualstudio.com/it-it/docs/setup-admin/team-services/connect-to-visual-studio-team-services
[Enable diagnostics in Azure Cloud Services using PowerShell]:https://azure.microsoft.com/en-us/documentation/articles/cloud-services-diagnostics-powershell/

[0]: ./media/cloud-services-vs-ci/vs-01.png
[1]: ./media/cloud-services-vs-ci/vs-02.png
[2]: ./media/cloud-services-vs-ci/file-01.png
[3]: ./media/cloud-services-vs-ci/vs-03.png
[4]: ./media/cloud-services-vs-ci/vs-04.png
[5]: ./media/cloud-services-vs-ci/vs-05.png
[6]: ./media/cloud-services-vs-ci/vs-06.png
[7]: ./media/cloud-services-vs-ci/vs-07.png
[8]: ./media/cloud-services-vs-ci/vs-08.png
[9]: ./media/cloud-services-vs-ci/vs-09.png
[10]: ./media/cloud-services-vs-ci/vso-01.png
[11]: ./media/cloud-services-vs-ci/vso-02.png
[12]: ./media/cloud-services-vs-ci/vso-03.png
[13]: ./media/cloud-services-vs-ci/vso-04.png
[14]: ./media/cloud-services-vs-ci/vso-05.png
[15]: ./media/cloud-services-vs-ci/vso-06.png
[16]: ./media/cloud-services-vs-ci/vso-07.png
[17]: ./media/cloud-services-vs-ci/vso-08.png
[18]: ./media/cloud-services-vs-ci/vso-09.png
[19]: ./media/cloud-services-vs-ci/vso-10.png
[20]: ./media/cloud-services-vs-ci/vso-11.png
[21]: ./media/cloud-services-vs-ci/vso-12.png
[22]: ./media/cloud-services-vs-ci/vso-13.png
[23]: ./media/cloud-services-vs-ci/vso-14.png
[24]: ./media/cloud-services-vs-ci/vso-15.png
