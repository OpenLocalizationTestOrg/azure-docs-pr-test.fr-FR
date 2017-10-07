---
title: "aaaPublishing un Service Cloud à l’aide des outils d’Azure hello | Documents Microsoft"
description: "En savoir plus sur les projets de service de cloud toopublish Azure à l’aide de Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1a07b6e4-3678-4cbf-b37e-4520b402a3d9
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/14/2017
ms.author: kraigb
ms.openlocfilehash: 31ede8308146de2bb128b768f23f64eb85bc7548
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="publishing-a-cloud-service-using-hello-azure-tools"></a>Publication d’un Service Cloud à l’aide des outils d’Azure hello
À l’aide de hello Windows Azure Tools pour Microsoft Visual Studio, vous pouvez publier votre application Windows Azure directement à partir de Visual Studio. Visual Studio prend en charge intégrée de publication tooeither hello intermédiaire ou hello l’environnement de Production d’un service cloud.

Avant de pouvoir publier une application Azure, vous devez disposer d’un abonnement Azure. Vous devez également configurer un cloud service et le stockage compte toobe utilisé par votre application. Vous pouvez les définir à hello [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885).

> [!IMPORTANT]
> Lorsque vous publiez, vous pouvez sélectionner un environnement de déploiement hello pour votre service cloud. Vous devez également sélectionner un compte de stockage qui est le package d’application hello toostore utilisé pour le déploiement. Après le déploiement, package d’application hello est supprimé à partir du compte de stockage hello.
> 
> 

Lorsque vous développez et testez une application Windows Azure, vous pouvez utiliser Web Deploy des modifications toopublish incrémentielle pour vos rôles web. Après avoir publié votre environnement de déploiement d’application tooa, Web Deploy vous permet de déployer les modifications directement de l’ordinateur virtuel de toohello qui est en cours d’exécution rôle web de hello. Vous n’avez toopackage et publier votre application Azure complète chaque fois que vous tooupdate votre tootest de rôle web les changements de hello. Avec cette approche, vous pouvez avoir vos modifications de rôle web disponibles dans le cloud hello pour le test sans attente toohave votre environnement de déploiement d’application tooa publiée.

Utiliser hello suivant les procédures toopublish votre application Windows Azure et tooupdate un rôle web avec Web Deploy :

* Publier ou créer un package d'une application Azure à partir de Visual Studio
* Mettre à jour un rôle web dans le cadre du cycle de test et développement de hello

## <a name="publish-or-package-an-azure-application-from-visual-studio"></a>Publier ou créer un package d'une application Azure à partir de Visual Studio
Lorsque vous publiez votre application Windows Azure, vous pouvez effectuer une des hello tâches suivantes :

* Créer un package de service : vous pouvez utiliser cette toopublish de fichier de configuration service hello et de package de votre environnement de déploiement application tooa hello [portail classique Azure](http://go.microsoft.com/fwlink/?LinkID=213885).
* Publier votre projet Azure à partir de Visual Studio : toopublish votre application directement tooAzure, que vous utilisez hello Assistant Publication. Pour plus d’informations, consultez [Assistant Publication d’application Azure](vs-azure-tools-publish-azure-application-wizard.md).

### <a name="toocreate-a-service-package-from-visual-studio"></a>toocreate un package de service à partir de Visual Studio
1. Lorsque vous êtes prêt toopublish votre application, ouvrez l’Explorateur de solutions, menu contextuel Ouvrir hello hello projet Windows Azure qui contient vos rôles, et choisissez Publier.
2. toocreate un package de services uniquement, procédez comme suit :  
   
   1. Dans le menu contextuel hello hello Azure de projet, choisissez **Package**.
   2. Bonjour **Package d’Application Azure** boîte de dialogue, choisissez configuration du service pour lequel vous souhaitez toocreate hello un package, puis choisissez la configuration de build hello.
   3. tooturn (facultatif) sur le Bureau à distance pour le service cloud hello après sa publication, sélectionnez hello **activer le Bureau à distance pour tous les rôles** case à cocher, puis sélectionnez **paramètres** tooconfigure Bureau à distance. Si vous souhaitez toodebug votre service cloud après sa publication, activer le débogage à distance en sélectionnant **activer le débogueur distant pour tous les rôles**.
      
      Pour plus d’informations, consultez [Utilisation du Bureau à distance avec des rôles Azure](vs-azure-tools-remote-desktop-roles.md).
   4. toocreate hello du package, choisissez hello **Package** lien.
      
      L’Explorateur de fichiers affiche l’emplacement du fichier hello Hello nouvellement créé package. Vous pouvez copier cet emplacement afin que vous puissiez l’utiliser à partir de hello [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885).
   5. toopublish cet environnement de déploiement tooa du package, vous devez utiliser cet emplacement comme hello emplacement du Package lorsque vous créez un service cloud et déployez cet environnement tooan de package avec hello [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885).
3. Processus de déploiement hello toocancel (facultatif), sur le menu contextuel hello hello élément de ligne dans le journal d’activité hello, choisissez **Annuler et supprimer**. Cela arrête le processus de déploiement hello et supprime l’environnement de déploiement hello de Azure.
   
   > [!NOTE]
   > tooremove cet environnement de déploiement après qu’il a été déployé, vous devez utiliser hello [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885).
   > 
   > 
4. (Facultatif) Après avoir démarré vos instances de rôle, Visual Studio affiche automatiquement un environnement de déploiement hello Bonjour **Services de cloud computing** nœud dans l’Explorateur de serveurs. À ce stade, vous pouvez voir l’état hello hello individuelles d’instances de rôle. Consultez [des ressources de la gestion de Azure avec Cloud Explorer](vs-azure-tools-resources-managing-with-cloud-explorer.md).hello après l’illustration montre les instances de rôle de hello pendant qu’elles sont toujours en hello initialisation de l’état :
   
    ![VST_DeployComputeNode](./media/vs-azure-tools-publishing-a-cloud-service/IC744134.png)

## <a name="update-a-web-role-as-part-of-hello-development-and-testing-cycle"></a>Un rôle Web dans le cadre de hello développement et de test du Cycle de mise à jour
Si l’infrastructure de serveur principal de votre application est stable, mais les rôles web hello doivent souvent plus de mises à jour, vous pouvez utiliser Web Deploy tooupdate qu’un rôle web dans votre projet. Cela est pratique lorsque vous ne souhaitez toorebuild et redéployer les rôles de travail principaux hello, ou si vous avez plusieurs rôles web et que vous souhaitez tooupdate uniquement un des rôles de web hello.

### <a name="requirements"></a>Configuration requise
Voici votre rôle web hello exigences toouse Web Deploy tooupdate :

* **Pour le développement et de test uniquement à :** hello modifications sont apportées directement toohello virtual machine où le rôle web de hello est en cours d’exécution. Si cet ordinateur virtuel a toobe recyclé, hello modifications sont perdues, ordinateur de virtuel hello toorecreate utilisés pour le rôle de hello car hello du package d’origine que vous avez publiée. Vous devez republier votre application tooget hello dernières modifications de rôle web de hello.
* **Seuls les rôles web peuvent être mis à jour :** les rôles de travail ne peuvent pas être mis à jour. En outre, vous ne pouvez pas mettre à jour hello RoleEntryPoint dans WebRole.cs.
* **Peut prendre en charge une seule instance d'un rôle web :** vous ne pouvez pas avoir plusieurs instances d'un rôle web dans votre environnement de déploiement. Toutefois, plusieurs rôles web, chacun avec une seule instance, sont pris en charge.
* **Vous devez activer les connexions Bureau à distance :** cela est nécessaire afin que le déploiement Web puisse utiliser hello utilisateur et mot de passe tooconnect toohello machine virtuelle toodeploy hello modifications toohello serveur qui exécute Internet Information Services (IIS). En outre, vous devrez peut-être tooconnect toohello machine virtuelle tooadd un tooIIS de certificat approuvé sur cet ordinateur virtuel. (Cela assure que hello de connexion à distance pour IIS qui est utilisé par Web Deploy est sécurisée.)

Hello procédure suivante suppose que vous utilisez hello **publier l’Application Azure** Assistant.

### <a name="tooenable-web-deploy-when-you-publish-your-application"></a>tooEnable Web Deploy lorsque vous publiez votre Application
1. tooenable hello **activer Web Deploy** pour toutes les web case à cocher de rôles, vous devez d’abord configurer les connexions Bureau à distance. Sélectionnez **activer le Bureau à distance** pour tous les rôles, puis entrez ces informations hello qui seront utilisé tooconnect à distance dans hello **Configuration Bureau à distance** zone qui s’affiche. Consultez [Utilisation du Bureau à distance avec des rôles Azure](vs-azure-tools-remote-desktop-roles.md) pour plus d’informations.
2. tooenable Web Deploy pour tous les hello rôles web dans votre application, sélectionnez **activer Web Deploy pour tous les rôles web**.
   
    Un triangle d'avertissement jaune s'affiche. Web Deploy utilise par défaut un certificat non fiable et auto-signé, ce qui n'est pas recommandé pour télécharger des données sensibles. Si vous avez besoin à toosecure ce processus pour les données sensibles, vous pouvez ajouter un toobe de certificat SSL utilisé pour les connexions Web Deploy. Ce certificat doit toobe un certificat approuvé. Pour plus d’informations sur la façon toodo, consultez la section de hello **tooMake Web déployer Secure** plus loin dans cette rubrique.
3. Choisissez **suivant** tooshow hello **Résumé** écran, puis choisissez **publier** service de cloud toodeploy hello.
   
    service de cloud Hello est publié. machine virtuelle Hello qui est créé a des connexions distantes activées pour l’IIS afin que Web Deploy puisse être utilisé tooupdate vos rôles web sans les republier.
   
   > [!NOTE]
   > Si vous avez plusieurs instances configurées pour un rôle web, un message d’avertissement s’affiche, indiquant que chaque rôle web sera limité tooone seule instance dans hello package qui a créé toopublish votre application. Sélectionnez **OK** toocontinue. Comme indiqué dans la section Configuration requise de hello, vous pouvez avoir plus d’un rôle web, mais qu’une seule instance de chaque rôle.
   > 
   > 

### <a name="tooupdate-your-web-role-by-using-web-deploy"></a>tooUpdate votre rôle Web à l’aide de Web Deploy
1. toouse Web Deploy, assurez-vous de projet de toohello de modifications de code pour un de vos rôles web dans Visual Studio que vous toopublish, puis cliquez sur ce nœud de projet dans votre solution et pointez trop**publier**. Hello **publier le site Web** boîte de dialogue s’affiche.
2. (Facultatif) Si vous avez ajouté un toouse de certificat SSL approuvé pour les connexions distantes pour IIS, vous pouvez effacer hello **autoriser les certificats non approuvés** case à cocher. Pour plus d’informations sur la façon dont tooadd sécuriser un toomake certificat Web Deploy, consultez la section de hello **tooMake Web déploiement sécurisé** plus loin dans cette rubrique.
3. toouse Web Deploy, mécanisme de publication hello a besoin de nom d’utilisateur hello et un mot de passe que vous avez configurée pour votre connexion Bureau à distance lorsque vous commencez la publication du package de hello.
   
   1. Dans **nom d’utilisateur**, entrez le nom d’utilisateur hello.
   2. Dans **mot de passe**, entrez le mot de passe hello.
   3. (Facultatif) Si vous souhaitez toosave ce mot de passe de ce profil, choisissez **enregistrer le mot de passe**.
4. rôle de web tooyour toopublish hello modifications, choisissez **publier**.
   
    ligne Hello affiche **publier démarré**. Lors de la publication de hello est terminée, **publication a réussi** s’affiche. modifications de Hello ont désormais été rôle web de toohello déployée sur votre machine virtuelle. Maintenant vous pouvez démarrer votre application Windows Azure dans tootest d’environnement Windows Azure hello vos modifications.

### <a name="toomake-web-deploy-secure"></a>tooMake Web déploiement sécurisé
1. Web Deploy utilise par défaut un certificat non fiable et auto-signé, ce qui n'est pas recommandé pour télécharger des données sensibles. Si vous avez besoin à toosecure ce processus pour les données sensibles, vous pouvez ajouter un toobe de certificat SSL utilisé pour les connexions Web Deploy. Ce certificat doit toobe un certificat de confiance, vous obtenez à partir d’une autorité de certification (CA).
   
    toomake Web Deploy sécurisé pour chaque machine virtuelle pour chacun de vos rôles web, vous devez télécharger un certificat de confiance hello que vous souhaitez toouse pour le déploiement de web toohello [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885). Cela permet de s’assurer que le certificat hello est ajouté machine virtuelle toohello qui est créé pour le rôle de hello web lorsque vous publiez votre application.
2. tooadd un toouse de tooIIS de certificat SSL approuvé pour les connexions à distance, procédez comme suit :
   
   1. machine virtuelle de toohello tooconnect qui exécute le rôle web de hello, instance hello sélection du rôle web de hello dans **Cloud Explorer** ou **l’Explorateur de serveurs**, puis choisissez hello **se connecter à l’aide de Bureau à distance** commande. Pour des instructions détaillées sur l’ordinateur virtuel de toohello tooconnect, consultez [à l’aide de bureau à distance avec des rôles Azure](vs-azure-tools-remote-desktop-roles.md).
      
      Votre navigateur vous invitera à toodownload un. Fichier RDP.
   2. tooadd un certificat SSL, le service de gestion hello ouvert dans le Gestionnaire des services Internet. Dans le Gestionnaire des services Internet, activer SSL en ouvrant le hello **liaisons** lien Bonjour **Action** volet. Hello **ajouter la liaison de Site** boîte de dialogue s’affiche. Choisissez **ajouter**, puis choisissez HTTPS Bonjour **Type** liste déroulante. Bonjour **certificat SSL** , sélectionnez le certificat SSL hello que vous aviez signé par une autorité de certification et que vous avez téléchargé toohello [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885). Pour plus d’informations, consultez [configurer les paramètres de connexion pour hello Service de gestion](http://go.microsoft.com/fwlink/?LinkId=215824).
      
      > [!NOTE]
      > Si vous ajoutez un certificat SSL approuvé, triangle d’avertissement jaune de hello n’apparaît plus dans hello **Assistant Publication**.
      > 
      > 

## <a name="include-files-in-hello-service-package"></a>Fichiers Include Bonjour Package de Service
Vous devrez peut-être tooinclude des fichiers spécifiques dans votre package de service afin qu’ils soient disponibles sur l’ordinateur virtuel hello qui est créé pour un rôle. Par exemple, vous pourriez tooadd un fichier .exe ou un fichier .msi qui est utilisé par un package de service de démarrage du script tooyour. Ou bien, vous devrez peut-être tooadd un assembly qui nécessite d’un projet de rôle web ou de travail. fichiers de tooinclude qu'ils doivent être ajoutés solution toohello pour votre application Windows Azure.

### <a name="tooinclude-files-in-hello-service-package"></a>fichiers tooinclude dans le package de service hello
1. tooadd un package de service tooa assembly, utilisez hello comme suit :
   
   1. Dans **l’Explorateur de solutions** le nœud de projet hello ouvert pour projet hello est manquant pour l’assembly hello référencé.
   2. projet de toohello assembly tooadd hello, menu contextuel Ouvrir hello hello **références** dossier, puis choisissez **ajouter une référence**. boîte de dialogue Ajouter une référence de Hello.
   3. Choisissez une référence hello que vous souhaitez tooadd et choisissez hello **OK** bouton.
      
      référence de Hello est ajouté liste toohello sous hello **références** dossier.
   4. Ouvrez le menu contextuel hello assembly hello que vous avez ajouté, sélectionnez **propriétés**. Hello **propriétés** fenêtre s’affiche.
      
      package de cet assembly dans le service hello tooinclude, Bonjour **liste copie locale** choisissez **True**.
2. Dans **l’Explorateur de solutions** le nœud de projet hello ouvert pour projet hello est manquant pour l’assembly hello référencé.
3. projet de toohello assembly tooadd hello, menu contextuel Ouvrir hello hello **références** dossier, puis choisissez **ajouter une référence**. Hello **ajouter une référence** boîte de dialogue s’affiche.
4. Choisissez une référence hello que vous souhaitez tooadd et choisissez hello **OK** bouton.
   
    référence de Hello est ajouté liste toohello sous hello **références** dossier.
5. Ouvrez le menu contextuel hello assembly hello que vous avez ajouté, sélectionnez **propriétés**. fenêtre de propriétés Hello s’affiche.
6. package de cet assembly dans le service hello tooinclude, Bonjour **copie locale** , choisissez **True**.
7. fichiers tooinclude dans le package de service hello qui ont été ajoutés tooyour projet de rôle web, ouvrez le menu de raccourci hello du fichier de hello, puis choisissez **propriétés**. À partir de hello **propriétés** fenêtre, choisissez **contenu** de hello **Action de génération** zone de liste.
8. fichiers tooinclude dans le package de service hello qui ont été ajoutés tooyour projet de rôle de travail, ouvrez le menu de raccourci hello du fichier de hello, puis choisissez **propriétés**. À partir de hello **propriétés** fenêtre, choisissez **Copier si plus récent** de hello **toooutput répertoire** zone de liste.

## <a name="next-steps"></a>Étapes suivantes
toolearn en savoir plus sur la publication tooAzure à partir de Visual Studio, consultez [Assistant Publication d’Application Azure](vs-azure-tools-publish-azure-application-wizard.md).

