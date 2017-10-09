---
title: "aaaSet d’intégration continue d’Azure microservices | Documents Microsoft"
description: "Obtenir une vue d’ensemble de la façon tooset d’intégration continue et de déploiement pour une application de Service Fabric à l’aide de Visual Studio Team Services (VSTS)."
services: service-fabric
documentationcenter: na
author: mthalman-msft
manager: timlt
editor: 
ms.assetid: 3e8c2290-9e7a-456a-9b2c-db44d1b3988d
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 12/06/2016
ms.author: mthalman;mikhegn
ms.openlocfilehash: 041e081f4a42f379394f2d21f07db4f6de045b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-service-fabric-continuous-integration-and-deployment-with-visual-studio-team-services"></a>Configurer l’intégration et le déploiement continus de Service Fabric avec Visual Studio Team Services
Cet article décrit tooset d’étapes hello d’intégration continue et de déploiement pour une application Azure Service Fabric à l’aide de Visual Studio Team Services (VSTS).

Ce document reflète la procédure en cours hello et toochange attendue au fil du temps.

## <a name="prerequisites"></a>Composants requis
tooget démarré, procédez comme suit :

1. Assurez-vous d’avoir accès tooa Team Services compte ou [créer un](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services) vous-même.
2. Vérifiez que vous disposez de projet d’équipe Team Services accès tooa ou [créer un](https://www.visualstudio.com/docs/setup-admin/create-team-project) vous-même.
3. Assurez-vous d’avoir un toowhich de cluster Service Fabric, vous pouvez déployer votre application ou créez-en un à l’aide de hello [portail Azure](service-fabric-cluster-creation-via-portal.md), un [modèle Azure Resource Manager](service-fabric-cluster-creation-via-arm.md), ou [Visual Studio ](service-fabric-cluster-creation-via-visual-studio.md).
4. Vérifiez qu’un projet d’application Service Fabric (.sfproj) a été créé. Vous devez disposer d’un projet qui a été créé ou mis à niveau avec le Service Fabric SDK 2.1 ou version ultérieure (fichier de .sfproj hello doit contenir une valeur de propriété ProjectVersion 1.1 ou version ultérieure).

> [!NOTE]
> Les agents de build personnalisés ne sont plus nécessaires. Les agents hébergés par Team Services sont désormais installés au préalable avec le logiciel de gestion du cluster Service Fabric, ce qui permet le déploiement de vos applications depuis ces agents, directement.
> 
> 

## <a name="configure-and-share-your-source-files"></a>Configurer et partager vos fichiers source
Hello plus important est de toodo préparer un profil de publication pour une utilisation par les processus de déploiement hello qui s’exécute dans Team Services.  profil de publication Hello doit être cluster hello tootarget configurés que vous avez précédemment préparé :

1. Choisissez un profil de publication au sein de votre projet d’Application que vous souhaitez toouse pour votre flux de travail d’intégration continue. Suivez hello [publier les instructions](service-fabric-publish-app-remote-cluster.md) sur la façon de toopublish un cluster à distance tooa d’application. En fait inutile toopublish votre application via. Vous pouvez cliquer sur hello **enregistrer** lien hypertexte Bonjour la boîte de dialogue de publier une fois que vous avez configuré correctement les choses.
2. Si vous souhaitez que votre toobe application mis à niveau pour chaque déploiement qui se produit dans les Services d’équipe, vous souhaitez tooconfigure hello mise à niveau tooenable de profil de publication. Bonjour même publier la boîte de dialogue utilisée à l’étape 1, vérifiez que hello **mise à niveau hello Application** case à cocher est activée.  Plus d’informations sur la [configuration de paramètres de mise à niveau supplémentaires](service-fabric-visualstudio-configure-upgrade.md). Cliquez sur hello **enregistrer** toohello de paramètres de lien hypertexte toosave hello le profil de publication.
3. Assurez-vous que vous avez enregistré vos modifications toohello publier profil et annulez hello boîte de dialogue Publier.
4. Il est temps trop[partager des fichiers sources du projet de votre Application](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services#vs) avec Team Services. Une fois que vos fichiers sources sont accessibles dans les Services d’équipe, vous pouvez maintenant déplacer sur l’étape suivante de toohello de génération de builds. 

## <a name="create-a-build-definition"></a>Créer une définition de build
Une définition de build Team Services décrit un flux de travail qui se compose d’un ensemble d’étapes de génération exécutées séquentiellement. objectif de Hello de définition de build hello que vous créez est tooproduce un package d’application Service Fabric et autres artefacts, qui peuvent être utilisés toodeploy hello application. Plus d’informations sur les [définitions de build](https://www.visualstudio.com/docs/build/define/create)Team Services.

### <a name="create-a-definition-from-hello-build-template"></a>Créer une définition de modèle de build hello
1. Ouvrez votre projet d’équipe dans Visual Studio Team Services.
2. Sélectionnez hello **générer** onglet.
3. Vert de hello sélectionnez  **+**  signer toocreate une définition de build.
4. Dans la boîte de dialogue hello qui s’ouvre, sélectionnez **Application Azure Service Fabric** dans hello **générer** catégorie de modèle.
5. Sélectionnez **Suivant**.
6. Sélectionnez le référentiel de hello et une branche associé à votre application de Service Fabric.
7. Sélectionnez la file d’attente de l’agent hello toouse vous le souhaitez. Les agents hébergés sont pris en charge.
8. Sélectionnez **Créer**.
9. Enregistrer la définition de build hello et fournir un nom.
10. Bonjour paragraphe suivant est une description des étapes de génération hello généré par le modèle de hello :

| Étape de génération | Description |
| --- | --- |
| Restauration NuGet |Restaure les packages NuGet hello pour les solutions hello. |
| Génération de la solution \*.sln |Génère un ensemble de la solution hello. |
| Génération de la solution \*.sfproj |Génère un package d’application de Service Fabric hello est utilisé toodeploy hello application. emplacement de package d’application Hello est toobe spécifié dans le répertoire de l’artefact de la build hello. |
| Mise à jour des versions de l’application Service Fabric |Met à jour les valeurs de version hello contenues dans tooallow de fichiers manifeste du package d’application hello pour la prise en charge de mise à niveau. Consultez hello [page de documentation de tâche](https://go.microsoft.com/fwlink/?LinkId=820529) pour plus d’informations. |
| Copie des fichiers |Hello de copies publier toobe d’artefacts de build toohello application paramètres fichiers utilisé pour le déploiement et un profil. |
| Publication d’artefact |Publie les artefacts de build hello. Permet à une définition de mise en production les artefacts de build tooconsume hello. |

### <a name="verify-hello-default-set-of-tasks"></a>Vérifiez l’ensemble de tâches par défaut de hello
1. Vérifiez que hello **Solution** champ d’entrée de hello **restauration NuGet** et **générer la solution** étapes de génération.  Par défaut, les étapes de build exécuter en cas de tous les fichiers de solution qui sont contenus dans le référentiel de hello associé.  Si vous souhaitez uniquement toooperate de définition de build hello sur l’un de ces fichiers de solution, vous devez le fichier toothat chemin d’accès tooexplicitly mise à jour hello.
2. Vérifiez que hello **Solution** champ d’entrée de hello **Package application** étape de génération.  Par défaut, cette étape de génération ne suppose qu’un seul projet d’Application Service Fabric (.sfproj) existe dans le référentiel de hello.  Si vous avez plusieurs de ces fichiers dans votre référentiel et que vous souhaitez tootarget uniquement un d’eux pour cette définition de build, vous devez le fichier toothat chemin d’accès tooexplicitly mise à jour hello.  Si vous souhaitez toopackage Application plusieurs projets dans votre référentiel, vous devez toocreate supplémentaires **Visual Studio Build** les étapes dans la définition de build hello que chaque cible d’un projet d’Application.  Vous devez également tooupdate hello **Arguments MSBuild** champ pour chacune de ces étapes de build afin que l’emplacement du package hello est unique pour chacun d’eux.
3. Vérifier le comportement du contrôle de version hello défini dans hello **Versions de mise à jour de Service Fabric application** étape de génération.  Par défaut, cette étape de génération ajoute hello build tooall version valeurs numériques dans les fichiers manifeste du package d’application hello. Consultez hello [page de documentation de tâche](https://go.microsoft.com/fwlink/?LinkId=820529) pour plus d’informations. Cela est utile pour prendre en charge la mise à niveau de votre application, car chaque déploiement de mise à niveau requiert que les valeurs de version différente du déploiement précédent de hello. Si vous n’êtes pas intention mise à niveau des applications toouse dans votre flux de travail, vous pouvez envisager la désactivation de cette étape de génération. Il doit être désactivée si votre intention est tooproduce une build qui peut être utilisé toooverwrite une application de Service Fabric existante. déploiement de Hello échoue si la version hello d’application hello produite par hello build ne correspond pas à la version hello d’application hello dans un cluster de hello.
4. Si votre solution contient un projet .NET Core, vous devez vous assurer que votre définition de build contient une étape de génération qui restaure les dépendances hello :
   1. Sélectionnez **Ajouter une étape de build...**.
   2. Recherchez hello **de ligne de commande** de tâches dans l’onglet d’utilitaire hello et cliquez sur le bouton Ajouter.
   3. Pour les champs d’entrée de la tâche hello, utilisez hello valeurs suivantes :
   4. Outil : dotnet
   5. Arguments : restore
   6. Faites glisser les tâches hello afin qu’il soit immédiatement après hello **restauration NuGet** étape.
5. Enregistrer les modifications apportées à la définition de build toohello.

### <a name="try-it"></a>Essayer
Sélectionnez **file d’attente de** toomanually de démarrer une génération. Les builds sont également déclenchées sur notification Push ou archivage. Une fois que vous avez vérifié que build de hello s’exécute correctement, vous pouvez maintenant passer toodefining une définition de mise en production qui déploie votre cluster tooa d’application.

## <a name="create-a-release-definition"></a>Création d’une définition de version
Une définition de version Team Services décrit un flux de travail qui se compose d’un ensemble d’étapes de génération exécutées séquentiellement. objectif Hello de définition de la version hello que vous créez est tootake un package d’application et déployez-la tooa cluster. Utilisés conjointement, hello définition de build et définition de la version peut exécuter des flux de travail entier hello de démarrer avec tooending de fichiers de code source avec une application en cours d’exécution dans votre cluster. Plus d’informations sur les [définitions de version](https://www.visualstudio.com/docs/release/author-release-definition/more-release-definition)Team Services.

### <a name="create-a-definition-from-hello-release-template"></a>Créer une définition de modèle de version hello
1. Ouvrez votre projet dans Visual Studio Team Services.
2. Sélectionnez hello **version** onglet.
3. Sélectionnez hello vert  **+**  toocreate une nouvelle définition de mise en production puis sélectionnez **définition de la version créer** dans le menu de hello.
4. Dans la boîte de dialogue hello qui s’ouvre, sélectionnez **Azure Service Fabric déploiement** dans hello **déploiement** catégorie de modèle.
5. Sélectionnez **Suivant**.
6. Sélectionnez la définition de build de hello toouse souhaitée en tant que source de hello de cette définition de mise en production.  définition de build Hello version définition références hello artefacts qui ont été générés par hello sélectionné.
7. Vérifiez hello **déploiement continu** case à cocher si vous le souhaitez toohave Team Services automatiquement créer une nouvelle version et déployer l’application de Service Fabric hello chaque fois qu’une build est terminée.
8. Sélectionnez la file d’attente de l’agent hello toouse vous le souhaitez. Les agents hébergés sont pris en charge.
9. Sélectionnez **Créer**.
10. Modifier le nom de la définition hello en cliquant sur icône de crayon hello en hello haut hello.
11. Sélectionnez toowhich de cluster hello votre application doit être déployée à partir de hello **connexion Cluster** champ d’entrée de tâche hello. connexion du cluster Hello fournit les informations nécessaires hello permet hello déploiement tâche tooconnect toohello cluster. Si vous n’avez pas encore d’une connexion de cluster pour votre cluster, sélectionnez hello **gérer** lien hypertexte suivant toohello champ tooadd une. Dans la page hello qui s’ouvre, procédez hello comme suit :
    1. Sélectionnez **nouveau point de terminaison de Service** , puis sélectionnez **Azure Service Fabric** à partir du menu de hello.
    2. Sélectionnez le type hello d’authentification utilisé par le cluster hello ciblée par ce point de terminaison.
    3. Définir un nom pour votre connexion Bonjour **nom de la connexion** champ.  En règle générale, vous utiliseriez nom hello de votre cluster.
    4. Définir l’URL de point de terminaison de connexion de client hello Bonjour **point de terminaison de Cluster** champ.  Exemple : tcp://contoso.westus.cloudapp.azure.com:19000.
    5. Informations d’identification d’Azure Active Directory, définir les informations de hello souhaité toouse tooconnect toohello cluster Bonjour **nom d’utilisateur** et **mot de passe** champs.
    6. Pour l’authentification de base de certificat, définissez hello Base64 encodage du fichier de certificat client hello hello **certificat Client** champ.  Consultez la fenêtre contextuelle de hello aide sur ce champ pour plus d’informations sur la façon de tooget cette valeur.  Si votre certificat est protégé par mot de passe, définir le mot de passe hello Bonjour **mot de passe** champ.
    7. Confirmez vos modifications en cliquant sur **OK**. Après avoir navigué arrière tooyour définition de version, cliquez sur icône d’actualisation hello sur hello **connexion Cluster** point de terminaison hello de toosee champ vous venez d’ajouter.
12. Enregistrez la définition de la version hello.

> [!NOTE]
> Les comptes Microsoft (par exemple, @hotmail.com ou @outlook.com ne sont pas pris en charge pour l’authentification Azure Active Directory.
> 
> 

définition de Hello créé se compose d’une tâche de type **déploiement d’Application Service Fabric**. Consultez hello [page de documentation de tâche](https://go.microsoft.com/fwlink/?LinkId=820528) pour plus d’informations sur cette tâche.

### <a name="verify-hello-template-defaults"></a>Vérifiez les valeurs par défaut du modèle hello
1. Vérifiez que hello **profil de publication** champ d’entrée de hello **déployer une Application de Service Fabric** tâche. Par défaut, ce champ fait référence à un profil de publication nommé Cloud.xml contenus dans les artefacts de build hello. Si vous voulez tooreference un profil de publication différent ou si la build de hello contient plusieurs packages d’application dans ses artefacts, vous devez le chemin d’accès de tooupdate hello en conséquence.
2. Vérifiez que hello **Package d’Application** champ d’entrée de hello **déployer une Application de Service Fabric** tâche. Par défaut, ce champ fait référence à hello par défaut application package chemin d’accès utilisé dans le modèle de définition de build hello.  Si vous avez modifié le chemin d’accès du package application par défaut hello Bonjour la définition de build, vous devez le chemin d’accès de tooupdate hello correctement ici également.

### <a name="try-it"></a>Essayer
Sélectionnez **créer libérer** de hello **Release** toomanually de menu bouton Créer une mise en production. Dans la boîte de dialogue hello qui s’ouvre, sélectionnez build hello que vous souhaitez la version de hello toobase sur puis cliquez sur **créer**. Si vous avez activé le déploiement continu, les versions sont créées automatiquement lors de la définition de build hello associé termine une build.

## <a name="next-steps"></a>Étapes suivantes
toolearn plus d’informations sur l’intégration continue avec des applications de Service Fabric, lire hello suivant des articles :

* [Page d’accueil de la documentation relative à Team Services](https://www.visualstudio.com/docs/overview)
* [Page relative à la gestion des builds dans Team Services](https://www.visualstudio.com/docs/build/overview)
* [Page relative à la gestion des versions dans Team Services](https://www.visualstudio.com/docs/release/overview)

