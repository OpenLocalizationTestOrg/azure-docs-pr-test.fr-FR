---
title: aaaManage vos applications dans Visual Studio | Documents Microsoft
description: "Utiliser Visual Studio toocreate, package, développer, déployer et déboguer vos applications de Service Fabric et services."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: c317cb7e-7eae-466e-ba41-6aa2518be5cf
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: b2d5803d85e4f9645dcbece33a2208bc0955498d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-visual-studio-toosimplify-writing-and-managing-your-service-fabric-applications"></a>Utiliser l’écriture de toosimplify Visual Studio et la gestion de vos applications de Service Fabric
Vous pouvez gérer vos applications et services Azure Service Fabric via Visual Studio. Une fois que vous avez [configurer votre environnement de développement](service-fabric-get-started.md), vous pouvez utiliser les applications de Service Fabric toocreate Visual Studio, ajouter le Registre des services ou un package et déployer des applications dans votre cluster de développement local.

## <a name="deploy-your-service-fabric-application"></a>Déploiement de votre application Service Fabric
Par défaut, le déploiement d’une application combine hello dans une simple opération comme suit :

1. Création de package d’application hello
2. Magasin d’images toohello hello application package de téléchargement
3. L’enregistrement du type d’application hello
4. Suppression des instances d'application en cours d'exécution
5. Création d’une instance d’application

Dans Visual Studio, en appuyant sur **F5** déploie votre application et de joindre des instances de l’application hello débogueur tooall. Vous pouvez utiliser **Ctrl + F5** toodeploy une application sans débogage, ou vous pouvez publier tooa local ou un cluster distant à l’aide de hello le profil de publication. Pour plus d’informations, consultez [publier un cluster à distance tooa d’application à l’aide de Visual Studio](service-fabric-publish-app-remote-cluster.md).

### <a name="application-debug-mode"></a>Mode de débogage d’application
Visual Studio fournit une propriété appelée **Mode de débogage d’Application**, qui contrôle comment vous souhaitez que le déploiement d’applications Visual Studio toohandle dans le cadre du débogage.

#### <a name="tooset-hello-application-debug-mode-property"></a>tooset hello propriété Mode de débogage d’Application
1. Sur hello Service Fabric du projet d’application (*.sfproj) menu contextuel, choisissez **propriétés** (ou appuyez sur hello **F4** clé).
2. Bonjour **propriétés** fenêtre, jeu hello **Mode de débogage d’Application** propriété.

![Définir la propriété Mode de débogage d’application][debugmodeproperty]

#### <a name="application-debug-modes"></a>Modes de débogage de l’application

1. **Actualiser l’Application** ce mode vous permet de tooquickly modifier et déboguer votre code et les prend en charge la modification des fichiers web statiques pendant le débogage. Ce mode fonctionne uniquement si votre cluster de développement local est en [mode 1 nœud](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).
2. **Supprimer Application** causes hello toobe application supprimée lors de la session de débogage hello se termine.
3. **Mis à niveau automatiquement** application hello continue toorun lors de la session de débogage hello se termine. Hello session de débogage suivante traite le déploiement de hello comme une mise à niveau. processus de mise à niveau de Hello conserve toutes les données que vous avez entré dans une session de débogage précédente.
4. **Conserver l’Application** hello maintient les applications en cours d’exécution dans le cluster hello lorsque hello fin de la session de débogage. Hello début Hello prochaine session de débogage, application hello sera supprimée.

Pour **mise à niveau automatique** données sont conservées par l’application hello mise à niveau des fonctionnalités des applications de Service Fabric. Pour plus d’informations sur la mise à niveau des applications et sur la façon d’effectuer une mise à niveau dans un environnement réel, consultez [Mise à niveau d’application Service Fabric](service-fabric-application-upgrade.md).

## <a name="add-a-service-tooyour-service-fabric-application"></a>Ajouter un tooyour service application Service Fabric
Vous pouvez ajouter les nouveaux services tooyour application tooextend ses fonctionnalités.  tooensure que le service de hello est inclus dans votre package d’application, ajoutez service hello via hello **nouveau Service Fabric...**  élément de menu.

![Ajouter un service Service Fabric][newservice]

Sélectionnez une application de Service Fabric projet type tooadd tooyour et spécifiez un nom pour le service de hello.  Consultez [choix d’une infrastructure pour votre service](service-fabric-choose-framework.md) toohelp vous décidez quel service de type toouse.

![Sélectionnez une application de Service Fabric service projet type tooadd tooyour][addserviceproject]

Hello nouveau service est ajouté tooyour solution et le package d’application existant. références de service Hello et une instance de service par défaut sera ajouté toohello manifeste d’application, toobe de service à l’origine hello créé et démarré hello prochaine fois que vous déployez l’application hello.

![nouveau service de Hello est ajouté le manifeste d’application tooyour][newserviceapplicationmanifest]

## <a name="package-your-service-fabric-application"></a>Empaquetage de votre application Service Fabric
application de hello toodeploy et son cluster tooa de services, vous devez toocreate un package d’application.  package de Hello organise le manifeste de l’application hello, les manifestes de service et les autres fichiers nécessaires dans une disposition spécifique.  Visual Studio configure et gère le package hello dans le dossier du projet d’application hello, dans le répertoire de « pkg » hello.  En cliquant sur **Package** de hello **Application** crée du menu contextuel ou les mises à jour hello package d’application.

## <a name="remove-applications-and-application-types-using-cloud-explorer"></a>Supprimer des applications et des types d’applications à l’aide de Cloud Explorer
Vous pouvez effectuer les opérations de gestion de cluster de base à partir de Visual Studio à l’aide de Cloud Explorer, que vous pouvez lancer à partir de hello **vue** menu. Par exemple, vous pouvez supprimer des applications et annuler la mise en service de types d’applications sur des clusters locaux ou distants.

![Supprimer une application][removeapplication]

> [!TIP]
> Pour obtenir des fonctionnalités de gestion de clusters enrichies, consultez [Visualisation de votre cluster à l’aide de l’outil Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).
>
>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Étapes suivantes
* [Modèle d'application Service Fabric](service-fabric-application-model.md)
* [Déploiement d'applications Service Fabric](service-fabric-deploy-remove-applications.md)
* [Gestion des paramètres d’application pour plusieurs environnements](service-fabric-manage-multiple-environment-app-configuration.md)
* [Débogage de votre application Service Fabric](service-fabric-debugging-your-application.md)
* [Visualisation de votre cluster à l’aide de l’explorateur Service Fabric](service-fabric-visualizing-your-cluster.md)

<!--Image references-->
[addserviceproject]:./media/service-fabric-manage-application-in-visual-studio/addserviceproject.png
[manageservicefabric]: ./media/service-fabric-manage-application-in-visual-studio/manageservicefabric.png
[newservice]:./media/service-fabric-manage-application-in-visual-studio/newservice.png
[newserviceapplicationmanifest]:./media/service-fabric-manage-application-in-visual-studio/newserviceapplicationmanifest.png
[debugmodeproperty]:./media/service-fabric-manage-application-in-visual-studio/debugmodeproperty.png
[removeapplication]:./media/service-fabric-manage-application-in-visual-studio/removeapplication.png