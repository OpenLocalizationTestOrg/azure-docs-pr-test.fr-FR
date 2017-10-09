---
title: "aaaScale des rôles de travail dans les Services d’applications - Azure pile | Documents Microsoft"
description: "Instructions détaillées pour la mise à l’échelle d’App Services Azure Stack"
services: azure-stack
documentationcenter: 
author: kathm
manager: slinehan
editor: anwestg
ms.assetid: 3cbe87bd-8ae2-47dc-a367-51e67ed4b3c0
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/6/2017
ms.author: kathm
ms.openlocfilehash: 252b4a531655e38f3a3747f8a04b16fc6303f9e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-on-azure-stack-adding-more-worker-roles"></a>App Service sur Azure Stack : ajouter davantage de rôles de travail 

Ce document fournit des instructions sur la façon tooscale du Service d’applications sur les rôles de travail Azure pile. Il contient les étapes de création d’applications de toosupport de rôles de travail supplémentaires de n’importe quelle taille.

> [!NOTE]
> Si votre environnement POC Azure Stack n’a pas plus de 96 Go de RAM, l’ajout de capacité supplémentaire pourrait se révéler difficile.

App Service sur Azure Stack, par défaut, prend en charge les niveaux Worker gratuits et partagés. tooadd autres niveaux de travail, vous devez tooadd plusieurs rôles de travail.

Si vous n’êtes pas sûr de ce qui a été déployé avec la valeur par défaut de hello du Service d’applications sur l’installation de la pile d’Azure, vous pouvez consulter des informations supplémentaires dans hello [du Service d’applications sur une vue d’ensemble de la pile de Azure](azure-stack-app-service-overview.md).

Il existe deux façons tooadd une capacité supplémentaire tooApp Service sur la pile de Azure :
1.  [Ajouter des traitements supplémentaires directement à partir d’avec dans hello App Service ressource fournisseur Admin](#Add-additional-workers-directly-from-within-the-App-Service-Resource-Provider-Admin).
2.  [Créer des machines virtuelles supplémentaires manuellement et les ajouter toohello fournisseur de ressources du Service application](#Create-additional-VMs-manually-and-add-them-to-the-App-Service-Resource-Provider).

## <a name="add-additional-workers-directly-within-hello-app-service-resource-provider-admin"></a>Ajouter des traitements supplémentaires directement dans hello application administrateur fournisseur des ressources de Service.

1.  Se connecter toohello portail de la pile de Azure en tant qu’administrateur de service hello ;
2.  Parcourir trop**fournisseurs de ressources** et sélectionnez hello **App Service ressource fournisseur Admin**. ![Fournisseurs de ressources Azure Stack][1]
3.  Cliquez sur **Rôles**.  Vous trouverez répartition hello de tous les rôles du Service d’applications déployées.
4.  Cliquez sur hello option **nouvelle Instance de rôle** ![ajouter une nouvelle instance de rôle][2]
5.  Bonjour **nouvelle Instance de rôle** panneau :
    1. Choisissez le nombre supplémentaire **instances de rôle** tooadd voulue.  Dans l’aperçu de hello, il existe un maximum de 10.
    2. Sélectionnez hello **type de rôle**.  Dans cette version préliminaire, cette option est limitée tooWeb de travail.
    3. Sélectionnez hello **niveau de worker** vous aimeriez toodeploy ce processus de travail, le choix par défaut sont faible, moyenne, grande ou partagé.  Si vous avez créé vos propres niveaux Worker, ceux-ci sont également disponibles pour la sélection.
    4. Cliquez sur **OK** toodeploy hello traitements supplémentaires
6.  Service d’applications va de la pile de Azure ajouter maintenant hello des machines virtuelles supplémentaires, configurez-les, installer tous les logiciels requis de hello et les marquer comme prêt lorsque ce processus est terminé.  Ce processus peut prendre environ 80 minutes.
7.  Vous pouvez surveiller la progression hello de préparation hello de nouveaux threads de travail hello en affichant les workers hello Bonjour **rôles** panneau.

>[!NOTE]
>  Dans cette version préliminaire, hello flux intégré de nouvelle Instance de rôle est limitée tooWorker rôles et déployer des machines virtuelles de taille A1.  Nous développerons cette fonctionnalité dans une version ultérieure.

## <a name="manually-adding-additional-capacity-tooapp-service-on-azure-stack"></a>Ajout d’une capacité supplémentaire tooApp Service manuellement sur la pile de Azure.

Hello étapes suivantes sont requises tooadd des rôles supplémentaires :

1. [Créer une machine virtuelle](#step-1-create-a-new-vm-to-support-the-new-instance-size)
2. [Configuration de la machine virtuelle de hello](#step-2-configure-the-virtual-machine)
3. [Configurer le rôle de travail hello web dans le portail d’Azure pile hello](#step-3-configure-the-web-worker-role-in-the-azure-stack-portal)
4. [Configurer des plans App Service](#step-4-configure-app-service-plans)

## <a name="step-1-create-a-new-vm-toosupport-hello-new-instance-size"></a>Étape 1 : Créer une nouvelle machine virtuelle toosupport hello nouvelle taille d’instance
Créez un ordinateur virtuel, comme décrit dans [cet article](azure-stack-provision-vm.md), vous être assuré que le respect de hello sont effectuées les sélections :

* Nom d’utilisateur et mot de passe : fournir hello du même nom d’utilisateur et mot de passe fourni lors de l’installation du Service d’applications sur la pile de Azure.
* Abonnement : Utiliser un abonnement de fournisseur par défaut hello.
* Groupe de ressources : choisissez **AppService-LOCAL**.

> [!NOTE]
> Stocker des rôles de travail des machines virtuelles hello Bonjour même groupe de ressources en tant que Service d’applications sur la pile de Azure est déployé sur. (Cela est recommandé pour cette version.)
> 
> 

## <a name="step-2-configure-hello-virtual-machine"></a>Étape 2 : Configurer hello Machine virtuelle
Une fois terminé, déploiement de hello hello configuration suivante est rôle de traitement web requis toosupport hello :

1. Parcourir toohello **AppService LOCAL** groupe de ressources dans le portail de hello et sélectionnez hello nouvel ordinateur vous avez créé à l’étape 1.
2. Cliquez sur connecter Bonjour panneau toodownload hello distant bureau profil d’ordinateur virtuel.  Ouvrez hello profil tooopen un tooyour de session Bureau à distance machine virtuelle.
3. Connectez-vous à toohello machine virtuelle à l’aide du nom d’utilisateur hello et le mot de passe spécifié à l’étape 1.
4. Ouvrez PowerShell en cliquant sur hello **Démarrer** bouton et tapez PowerShell. Avec le bouton droit **PowerShell.exe**, puis sélectionnez **exécuter en tant qu’administrateur** tooopen PowerShell en mode administrateur.
5. Copie et collage de hello suivant les commandes (un à la fois) dans la fenêtre de PowerShell hello et appuyez sur entrez :
   
   ```netsh advfirewall firewall set rule group="File and Printer Sharing" new enable=Yes```
   ```netsh advfirewall firewall set rule group="Windows Management Instrumentation (WMI)" new enable=yes```
   ```reg add HKLM\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\Policies\\system /v LocalAccountTokenFilterPolicy /t REG\_DWORD /d 1 /f```
   
6. Fermez votre session Bureau à distance.
7. Redémarrez hello machine virtuelle à partir du portail de hello.

> [!NOTE]
> Il s’agit de la configuration minimale requise pour App Service sur Azure Stack. Ils sont des paramètres par défaut de hello d’image de Windows 2012 R2 hello inclus avec la pile de Azure. les instructions de Hello ont été fournies pour référence ultérieure et pour ceux qui utilisent une autre image.
> 
> 

## <a name="step-3-configure-hello-worker-role-in-hello-azure-stack-portal"></a>Étape 3 : Configurer le rôle de travail hello dans le portail d’Azure pile hello
1. Portail hello ouvrir en tant qu’administrateur de service hello sur **ClientVM**.
2. Accédez trop**fournisseurs de ressources** &gt; **App Service ressource fournisseur Admin**.![ Administrateur de fournisseur de ressources du Service d’applications][3]
3. Dans le panneau des paramètres de hello, cliquez sur **rôles**.![ Rôles de fournisseur de ressources du Service d’applications][4]
4. Cliquez sur **Ajouter une instance de rôle**.
5. Dans la zone de texte hello **nom du serveur** entrez hello **adresse IP** du serveur hello créé précédemment (dans la Section 1).
6. Sélectionnez hello **Type de rôle** vous aimeriez tooadd - contrôleur, serveur d’administration, frontal, traitement Web, serveur de publication ou serveur de fichiers.  Dans cette instance, sélectionnez Web Worker.
7. Cliquez sur hello **niveau** vous serez comme hello toodeploy nouvelle instance trop (petite, moyenne, grande ou partagé).  Si vous avez créé vos propres niveaux Worker, ceux-ci sont également disponibles pour la sélection.
8. Cliquez sur **OK**.
9. Revenir en arrière toohello **rôles** vue
10. Cliquez sur hello ligne toohello correspondante combinaison Type de rôle et le niveau de traitement attribué de votre machine virtuelle.
11. Recherchez pourquoi le nom de serveur que vous venez d’ajouter. Passez en revue la colonne d’état hello et attendre la prochaine étape de toomove toohello état de hello « Prêt ». Ceci peut prendre environ 80 minutes. ![Rôle Fournisseur de ressources App Service prêt][5]

## <a name="step-4-configure-app-service-plans"></a>Étape 4 : Configurer des plans App Service

1. Portail toohello sur hello ClientVM vous connecter.
2. Accédez trop**nouveau** &gt; **Web et Mobile**.
3. Sélectionnez le type de hello d’application, vous aimeriez toodeploy.
4. Fournir des informations de hello pour application hello et sélectionnez **un Plan / emplacement**.
    1. Cliquez sur **Create New**.
    2. Créer votre plan, en sélectionnant hello correspondant niveau tarifaire pour hello plan.

> [!NOTE]
> Dans ce panneau, vous pouvez créer plusieurs plans. Avant de déployer, toutefois, assurez-vous que vous avez sélectionné le plan approprié de hello.
> 
> 

Hello Voici un exemple de hello plusieurs niveaux de tarification disponibles par défaut.  Vous remarquerez que s’il n’y a aucune disposition des employés pour un niveau de travail spécifique, hello de toochoose option hello correspondant du niveau tarifaire est indisponible.![Niveaux tarifaires par défaut App Service sur Azure Stack][6]

<!--Image references-->
[1]: ./media/azure-stack-app-service-add-worker-roles/azure-stack-resource-providers.png
[2]: ./media/azure-stack-app-service-add-worker-roles/app-service-new-role-instance.png
[3]: ./media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-admin.png
[4]: ./media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-roles.png
[5]: ./media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-role-ready.png
[6]: ./media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-pricing-tier.png
