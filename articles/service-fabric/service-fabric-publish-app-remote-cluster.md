---
title: "aaaPublish un cluster à distance de tooa d’application avec Visual Studio | Documents Microsoft"
description: "Découvrez comment toopublish une infrastructure de service distant tooa application cluster à l’aide de Visual Studio."
services: service-fabric
documentationcenter: na
author: cawams
manager: timlt
editor: 
ms.assetid: faecd892-eb54-4d9c-8023-c67442afb8e8
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 07/29/2016
ms.author: cawa
ms.openlocfilehash: d0f06f120cc7e22f3f8e73ce0970e1da5823e647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-visual-studio"></a>Déployer et supprimer des applications avec Visual Studio
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-deploy-remove-applications.md)
> * [Visual Studio](service-fabric-publish-app-remote-cluster.md)
> * [API FabricClient](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

Hello extension Azure Service Fabric pour Visual Studio fournit un moyen facile, reproductibles et scriptable de toopublish un cluster de Service Fabric application tooa.

## <a name="hello-artifacts-required-for-publishing"></a>artefacts Hello requis pour la publication
### <a name="deploy-fabricapplicationps1"></a>Deploy-FabricApplication.ps1
Il s’agit d’un script PowerShell qui utilise un chemin d’accès au profil de publication comme paramètre pour publier des applications Service Fabric. Étant donné que ce script fait partie de votre application, vous êtes toomodify Bienvenue en tant que nécessaire pour votre application.

### <a name="publish-profiles"></a>Profils de publication
Un dossier de projet d’application Service Fabric hello appelé **PublishProfiles** contient des fichiers XML qui stockent des informations essentielles pour la publication d’une application, telles que :

* les paramètres de connexion au cluster Service Fabric ;
* Fichier de paramètres de chemin d’accès tooan application
* les paramètres de mise à niveau.

Par défaut, votre application inclut trois profils de publication : Local.1Node.xml, Local.5Node.xml, et Cloud.xml. Vous pouvez ajouter d’autres profils en copiant et collant un des fichiers par défaut de hello.

### <a name="application-parameter-files"></a>Fichiers de paramètre d’application
Un dossier de projet d’application Service Fabric hello appelé **ApplicationParameters** contient des fichiers XML pour les valeurs de paramètre de manifeste spécifié par l’utilisateur une application. Les fichiers manifeste de l’application peuvent être paramétrés de sorte que vous pouvez utiliser des valeurs différentes pour les paramètres de déploiement. toolearn en savoir plus sur le paramétrage de votre application, consultez [gérer plusieurs environnements dans le Service Fabric](service-fabric-manage-multiple-environment-app-configuration.md).

> [!NOTE]
> Pour les services d’acteur, vous devez créer le projet de hello tout d’abord avant de tenter de fichier de hello tooedit dans un éditeur ou via hello boîte de dialogue Publier. Il s’agit, car la partie des fichiers de manifeste hello sera générée lors de la génération de hello.

## <a name="toopublish-an-application-using-hello-publish-service-fabric-application-dialog-box"></a>toopublish une application à l’aide de la boîte de dialogue Publier une Application de Service Fabric hello
Hello étapes suivantes montrent comment une application à l’aide de toopublish hello **publier une Application de Service Fabric** boîte de dialogue fournie par hello outils de Visual Studio Service Fabric.

1. Dans le menu contextuel de hello du projet d’Application Service Fabric hello, choisissez **publier...** tooview hello **publier une Application de Service Fabric** boîte de dialogue.
   
    ![Hello ** boîte de dialogue Publier Service Fabric Application **][0]
   
    fichier Hello sélectionné Bonjour **cibler profile** zone de liste déroulante est où tous les paramètres de hello, à l’exception **manifeste versions**, sont enregistrés. Vous pouvez réutiliser un profil existant ou créez-en un en choisissant **< gérer les profils... >** Bonjour **cibler profile** zone de liste déroulante. Lorsque vous choisissez un profil de publication, son contenu s’affichent dans les champs de correspondance hello de boîte de dialogue hello. toosave vos modifications à tout moment, choisissez hello **enregistrer le profil** lien.    
2. Bonjour **point de terminaison de connexion** section, spécifiez le point de terminaison de publication local ou distant Service Fabric d’un cluster. modification ou tooadd hello du point de terminaison de connexion, cliquez sur hello **connexion de point de terminaison** liste déroulante. liste de Hello affiche hello disponible l’infrastructure du Service cluster connexion points de terminaison toowhich que vous pouvez publier en fonction de vos abonnements Azure. Notez que si vous n’êtes pas déjà connecté dans tooVisual Studio, vous serez invité à toodo ainsi.
   
    Utilisez hello cluster sélection boîte de dialogue zone toochoose jeu hello des clusters et des abonnements disponibles.
   
    ![Hello ** boîte de dialogue Sélectionnez Service Fabric Cluster **][1]
   
   > [!NOTE]
   > Si vous souhaitez que le point de terminaison toopublish tooan arbitraire (par exemple, un cluster tiers), consultez hello **publication point de terminaison de cluster arbitraire tooan** section ci-dessous.
   > 
   > 
   
    Une fois que vous choisissez un point de terminaison, Visual Studio valide cluster Service Fabric de hello connexion toohello sélectionné. Si le cluster de hello n’est pas sécurisé, Visual Studio peut se connecter tooit immédiatement. Toutefois, si le cluster de hello est sécurisé, vous devez tooinstall un certificat sur votre ordinateur local avant de continuer. Consultez [tooconfigure comment sécuriser les connexions](service-fabric-visualstudio-configure-secure-connections.md) pour plus d’informations. Lorsque vous avez terminé, choisissez hello **OK** bouton. cluster sélectionné de Hello s’affiche dans hello **publier une Application de Service Fabric** boîte de dialogue.
3. Bonjour **fichier de paramètres d’Application** liste déroulante, accédez le fichier de paramètres d’application tooan. Un fichier de paramètres d’application conserve les valeurs des paramètres spécifiés par l’utilisateur dans le fichier manifeste d’application hello. tooadd ou modifier un paramètre, choisissez hello **modifier** bouton. Entrez ou modifiez la valeur du paramètre hello Bonjour **paramètres** grille. Lorsque vous avez terminé, choisissez hello **enregistrer** bouton.
   
    ![Hello ** boîte de dialogue Modifier les paramètres **][2]
4. Hello d’utilisation **mise à niveau hello Application** toospecify de case à cocher si cette action de publication est une mise à niveau. Les actions de mise à niveau sont différentes des actions de publication normales. Consultez la page [Mise à niveau des applications Service Fabric](service-fabric-application-upgrade.md) pour obtenir la liste des différences. paramètres de mise à niveau tooconfigure, choisissez hello **configurer les paramètres de mise à niveau** lien. éditeur de mise à niveau paramètre Hello s’affiche. Consultez [configurer la mise à niveau hello d’une application de Service Fabric](service-fabric-visualstudio-configure-upgrade.md) toolearn plus d’informations sur les paramètres de mise à niveau.
5. Choisissez hello **Versions de manifeste...** hello tooview de bouton **modifier les Versions** boîte de dialogue. Vous devez tooupdate application et les versions de service pour un emplacement tootake mise à niveau. Consultez [didacticiel de mise à niveau l’application Service Fabric](service-fabric-application-upgrade-tutorial.md) toolearn comment les application et les versions de manifeste de service avoir un impact sur une mise à niveau.
   
    ![Hello ** boîte de dialogue Modifier les Versions **][3]
   
    Si l’application hello et les versions de service utilisent le contrôle de version sémantique comme 1.0.0 ou des valeurs numériques au format hello 1.0.0.0, sélectionnez hello **mettre à jour automatiquement les applications et les versions de service** option. Lorsque vous choisissez cette option, le service de hello et numéros de version d’application sont automatiquement mis à jour chaque fois qu’un code, la configuration, ou version du package est mis à jour. Si vous préférez les versions hello tooedit manuellement, désactivez hello case à cocher toodisable cette fonctionnalité.
   
   > [!NOTE]
   > Pour toutes les tooappear entrées de package pour un projet d’acteur, tout d’abord créer la hello projet toogenerate entrées hello dans les fichiers de manifeste de Service hello.
   > 
   > 
6. Lorsque vous avez terminé en spécifiant les paramètres nécessaires hello, choisissez hello **publier** bouton toopublish votre toohello d’application sélectionné cluster Service Fabric. Hello les paramètres que vous avez spécifiés sont appliqués toohello les processus de publication.

## <a name="publish-tooan-arbitrary-cluster-endpoint-including-party-clusters"></a>Publier le point de terminaison de cluster arbitraire tooan (y compris les clusters de tiers)
Hello expérience de publication de Visual Studio est optimisée pour la publication des clusters tooremote associés à un de vos abonnements Azure. Toutefois, il est possible toopublish tooarbitrary points de terminaison (tels que les clusters de partie de l’infrastructure de Service) par directement modification hello XML du profil de publication. Comme décrit ci-dessus, trois profils de publication sont fournies par défaut--**Local.1Node.xml**, **Local.5Node.xml**, et **Cloud.xml**--mais vous êtes toocreate Bienvenue profils supplémentaires pour différents environnements. Par exemple, vous pourriez toocreate un profil de publication des clusters tooparty, peut-être nommés **Party.xml**.

Si vous vous connectez tooan sécurisée de cluster, tout ce qui a requis est hello cluster connexion point de terminaison comme `partycluster1.eastus.cloudapp.azure.com:19000`. Dans ce cas, publier de point de terminaison de connexion hello Bonjour profil ressemble quelque chose comme ceci :

```XML
<ClusterConnectionParameters ConnectionEndpoint="partycluster1.eastus.cloudapp.azure.com:19000" />
```

  Si vous vous connectez le cluster sécurisée de tooa, vous devez également tooprovide les détails de hello du certificat de client hello de hello toobe de magasin local utilisé pour l’authentification. Pour plus d’informations, consultez [cluster Service Fabric de configuration des connexions sécurisées tooa](service-fabric-visualstudio-configure-secure-connections.md).

  Une fois votre profil de publication est configurée, vous pouvez le référencer dans hello boîte de dialogue Publier, comme illustré ci-dessous.

  ![Nouveau profil de publication dans la boîte de dialogue Publier][4]

  Notez que dans ce cas, hello nouveau profil de publication pointe tooone hello par défaut paramètre de fichiers d’application. Cela est approprié si vous souhaitez toopublish hello même application configuration tooa plusieurs environnements. En revanche, dans le cas où vous souhaitez toohave différentes configurations pour chaque environnement que vous souhaitez toopublish à, il serait logique toocreate un fichier de paramètres d’application correspondant.

## <a name="next-steps"></a>Étapes suivantes
toolearn comment le processus de publication hello tooautomate dans un environnement d’intégration continue, consultez [configurer l’intégration continue de l’infrastructure de Service](service-fabric-set-up-continuous-integration.md).

[0]: ./media/service-fabric-publish-app-remote-cluster/PublishDialog.png
[1]: ./media/service-fabric-publish-app-remote-cluster/SelectCluster.png
[2]: ./media/service-fabric-publish-app-remote-cluster/EditParams.png
[3]: ./media/service-fabric-publish-app-remote-cluster/EditVersions.png
[4]: ./media/service-fabric-publish-app-remote-cluster/publish-to-party-cluster.png
