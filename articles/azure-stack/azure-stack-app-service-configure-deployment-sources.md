---
title: "aaaConfigure des Sources de déploiement pour les Services d’application sur Azure pile | Documents Microsoft"
description: "Comment un administrateur de service peut configurer des sources de déploiement (Git, GitHub, BitBucket, Dropbox et OneDrive) pour App Service sur Azure Stack"
services: azure-stack
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/6/2017
ms.author: anwestg
ms.openlocfilehash: 2eaf0a7f4b6e52d64a302000c1dd3c3eb5d6a6ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-deployment-sources"></a>Configurer des sources de déploiement

App Service sur Azure Stack prend en charge le déploiement à la demande à partir de plusieurs fournisseurs de contrôle de code source.  Cette fonctionnalité permet d’application aux développeurs toobe en mesure de toodeploy directe à partir de leurs référentiels de contrôle de code source.  Dans commande pour tooconfigure en mesure de locataires toobe du Service d’applications tooconnect tootheir référentiels, les administrateurs doivent tout d’abord configurer l’intégration entre le Service d’application sur Azure pile hello et hello du fournisseur de contrôle de code Source.  Fournisseurs de contrôle de code Source Hello pris en charge, en outre toolocal Git, sont :

* GitHub
* BitBucket
* OneDrive
* DropBox

## <a name="view-deployment-sources-in-app-service-administration"></a>Afficher les sources de déploiement dans l’administration App Service

1. Ouvrez une session dans toohello portail d’administration Azure pile (https://adminportal.local.azurestack.external) en tant qu’administrateur de service hello.
2. Parcourir trop**fournisseurs de ressources** et sélectionnez hello **App Service ressource fournisseur Admin**.  ![Administrateur du fournisseur de ressources App Service][1]
3. Cliquez sur **Source control configuration** (Configuration du contrôle de code source).  Vous trouverez liste hello de toutes les Sources de déploiement configuré.
    ![Configuration du contrôle de code source de l’administrateur du fournisseur de ressources App Service][2]

## <a name="configure-github"></a>Configurer GitHub

> [!NOTE]
> Vous avez besoin une toocomplete de compte GitHub cette tâche.  Vous pouvez toouse un compte pour votre organisation plutôt qu’un compte personnel.

1. Connectez-vous à tooGitHub, parcourir toohttps://www.github.com/settings/developers et cliquez sur **inscrire une nouvelle application** ![GitHub - inscrire une nouvelle application][3]
2. Entrez un **nom d’application**, par exemple, App Service sur Azure Stack.
3. Entrez hello **URL de la page d’accueil**.  **URL de la page d’accueil de Hello doit être l’adresse du portail de pile Azure hello** https://portal.local.azurestack.external, par exemple :
4. Entrez une **description de l’application**
5. Entrez hello **URL de rappel d’autorisation**.  Dans un déploiement d’Azure pile par défaut, les Url hello est hello formulaire https://portal.local.azurestack.external/tokenauthorize, si vous s’exécutent sous un substitut de domaine différent de votre domaine pour azurestack.local ![GitHub - enregistrer un nouveau application avec des valeurs remplies][4]
6. Cliquez sur **Inscrire l’application**.  Vous aurez maintenant avec un Bonjour de liste de page **ID Client** et **clé secrète Client** pour l’application hello.
    ![GitHub - Inscription de l’application terminée][5]
7.  Dans une nouvelle fenêtre de navigateur onglet ou une fenêtre connectez-vous toohello portail d’administration Azure pile (https://adminportal.local.azurestack.external) en tant qu’administrateur de service hello. 
8.  Parcourir trop**fournisseurs de ressources** et sélectionnez hello **App Service ressource fournisseur Admin**. 
9. Cliquez sur **Source control configuration** (Configuration du contrôle de code source).
10. Copiez et collez hello **Id Client** et **clé secrète Client** dans des zones d’entrée correspondante de hello pour GitHub.
11. Cliquez sur **Enregistrer**.
12. Si vous ne souhaitez pas tooconfigure d’autres Sources de déploiement, passez trop[réparation planification de rôles de gestion](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles).


## <a name="configure-bitbucket"></a>Configurer BitBucket

> [!NOTE]
> Vous avez besoin une toocomplete de compte BitBucket cette tâche.  Vous pouvez toouse un compte pour votre organisation plutôt qu’un compte personnel.

1. Connectez-vous à tooBitBucket et parcourir trop**intégrations** sous votre compte ![tableau de bord BitBucket - intégrations][7]
2. Cliquez sur **OAuth** sous Gestion de l’accès et sur **Add consumer** (Ajouter un consommateur) ![BitBucket Ajouter un consommateur OAuth][8]
3. Entrez un **nom** pour le consommateur hello, par exemple du Service d’applications sur la pile de Azure
4. Entrez un **Description** pour l’application hello
5. Entrez hello **URL de rappel**.  Dans un déploiement d’Azure pile par défaut, hello Url de rappel est hello formulaire https://portal.local.azurestack.external/TokenAuthorize, si vous exécutez sous un domaine différent, remplacez votre domaine pour azurestack.local.  Url de Hello doit suivre la mise en majuscules de hello comme indiqué ici pour toosucceed d’intégration BitBucket.
6. Entrez hello **URL** -l’Url doit être hello URL du portail Azure pile, par exemple https://portal.local.azurestack.external
7. Sélectionnez hello **autorisations** requis **référentiels**: **en lecture** **Webhooks**: **en lecture et écriture**
8. Cliquez sur **Enregistrer**.  Vous voyez maintenant cette nouvelle application, ainsi que de hello **clé** et **Secret** sous **OAuth consommateurs**.
    ![Liste des applications BitBucket][9]
9.  Dans une nouvelle fenêtre de navigateur onglet ou une fenêtre connectez-vous toohello portail d’administration Azure pile (https://adminportal.local.azurestack.external) en tant qu’administrateur de service hello. 
10.  Parcourir trop**fournisseurs de ressources** et sélectionnez hello **App Service ressource fournisseur Admin**. 
11. Cliquez sur **Source control configuration** (Configuration du contrôle de code source).
12. Copiez et collez hello **clé** dans hello **Id Client** zone d’entrée et **Secret** dans hello **clé secrète Client** zone d’entrée pour BitBucket.
13. Cliquez sur **Enregistrer**.
14. Si vous ne souhaitez pas tooconfigure d’autres Sources de déploiement, passez trop[réparation planification de rôles de gestion](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles).

## <a name="configure-onedrive"></a>Configurer OneDrive

> [!NOTE]
> Les comptes OneDrive Entreprise ne sont actuellement pas pris en charge.  Vous devez toohave une tooa Account Microsoft lié OneDrive compte toocomplete cette tâche.  Vous pouvez toouse un compte pour votre organisation plutôt qu’un compte personnel.

1. Parcourir toohttps://apps.dev.microsoft.com/?referrer=https%3A%2F%2Fdev.onedrive.com%2Fapp-registration.htm et connectez-vous à l’aide de votre Account Microsoft.
2. Cliquez sur **Ajouter une application** sous **Mes applications**.
![Applications OneDrive][10]
3. Entrez un **nom** pour hello nouvelle inscription de l’Application, entrez **du Service d’applications sur Azure pile**, puis cliquez sur **créer une Application**
4. écran de Hello suivant répertorie les propriétés de hello de votre nouvelle application. Hello d’enregistrement **Id d’Application**
![propriétés de l’Application OneDrive][11]
5. Sous **Secrets d’Application** cliquez sur **générer un nouveau mot de passe** et enregistrement Bonjour **nouveau mot de passe généré** -il s’agit votre secret d’application.
> [!NOTE]
> Notez que toomake un nouveau mot de passe hello car il n’est pas obligatoirement une fois que vous cliquez sur OK à ce stade.
6. Sous **Plateformes**, cliquez sur **Ajouter une plateforme** et sélectionnez **Web**
7. Entrez hello **URI de redirection**.  Dans un déploiement par défaut de la pile de Azure hello URI de redirection est dans hello formulaire https://portal.local.azurestack.external/tokenauthorize, si vous s’exécutent sous un substitut de domaine différent de votre domaine pour azurestack.local ![OneDrive Application - Ajouter la plateforme Web][12]
8. Ensemble hello **Microsoft Graph autorisations** - **autorisations déléguées**
    - **Files.ReadWrite.AppFolder**
    - **User.Read**  
      ![Application OneDrive - Autorisations pour Microsoft Graph][13]
10. Cliquez sur **Enregistrer**.
11.  Dans une nouvelle fenêtre de navigateur onglet ou une fenêtre connectez-vous toohello portail d’administration Azure pile (https://adminportal.local.azurestack.external) en tant qu’administrateur de service hello. 
12.  Parcourir trop**fournisseurs de ressources** et sélectionnez hello **App Service ressource fournisseur Admin**. 
13. Cliquez sur **Source control configuration** (Configuration du contrôle de code source).
14. Copiez et collez hello **Id d’Application** dans hello **Id Client** zone d’entrée et **mot de passe** dans hello **clé secrète Client** zone d’entrée pour OneDrive.
15. Cliquez sur **Enregistrer**.
16. Si vous ne souhaitez pas tooconfigure d’autres Sources de déploiement, passez trop[réparation planification de rôles de gestion](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles).

## <a name="configure-dropbox"></a>Configurer Dropbox

> [!NOTE]
> Vous devez toohave un toocomplete de compte DropBox de cette tâche.  Vous pouvez toouse un compte pour votre organisation plutôt qu’un compte personnel.

1. Parcourir toohttps://www.dropbox.com/developers/apps et connectez-vous à l’aide de votre compte DropBox
2. Cliquez sur **Créer une application**. 
![Applications Dropbox][14]
3. Sélectionnez **Dropbox API** (API Dropbox).
4. Définir le niveau d’accès hello trop**dossier de l’application**
5. Entrez un **nom** pour votre application.
![Inscription d’une application Dropbox][15]
6. Cliquez sur **Créer une application**.  Vous aurez maintenant avec une page de liste de paramètres hello pour inclure des application hello **clé application** et **secret d’application**.
7. Vérifiez hello **nom du dossier application** est défini trop**du Service d’applications sur la pile de Azure**
8. Ensemble hello **URI de redirection OAuth 2** et cliquez sur **ajouter**.  Dans un déploiement par défaut de la pile de Azure hello URI de redirection est dans hello formulaire https://portal.local.azurestack.external/tokenauthorize, si vous s’exécutent sous un substitut de domaine différent de votre domaine pour azurestack.local ![application Dropbox configuration][16]
9.  Dans une nouvelle fenêtre de navigateur onglet ou une fenêtre connectez-vous toohello portail d’administration Azure pile (https://adminportal.local.azurestack.external) en tant qu’administrateur de service hello. 
10.  Parcourir trop**fournisseurs de ressources** et sélectionnez hello **App Service ressource fournisseur Admin**. 
11. Cliquez sur **Source control configuration** (Configuration du contrôle de code source).
12. Copiez et collez hello **clé d’Application** dans hello **Id Client** zone d’entrée et **secret d’application** dans hello **clé secrète Client** zone d’entrée pour Échange.
13. Cliquez sur **Enregistrer**.
14. Si vous ne souhaitez pas tooconfigure d’autres Sources de déploiement, passez trop[réparation planification de rôles de gestion](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles).

## <a name="schedule-repair-of-management-roles"></a>Planifier la réparation des rôles de gestion
Pour les paramètres de hello mis à jour dans la configuration de hello Hello toobe de sources diverses déploiement appliqué, hello les rôles de gestion doivent toobe réparé.  Ce processus garantit que les valeurs de configuration hello sont appliquées correctement et hello configuré déploiement Sources sont apportées tootenants disponibles.

1. Dans une nouvelle fenêtre de navigateur onglet ou une fenêtre connectez-vous toohello portail d’administration Azure pile (https://adminportal.local.azurestack.external) en tant qu’administrateur de service hello.
2. Parcourir trop**fournisseurs de ressources** et sélectionnez hello **App Service ressource fournisseur Admin**.
3. Cliquez sur **Source control configuration** (Configuration du contrôle de code source).
4. Copiez et collez hello **Id Client** et **clé secrète Client** dans des zones d’entrée correspondante de hello pour GitHub.
5. Cliquez sur **Enregistrer**.
6. Cliquez sur **Rôles**.
7. Cliquez sur **Serveur d’administration**.
8. Cliquez sur **Repair All** (Tout réparer) et sélectionnez **Oui**.  Cette opération permet de planifier une réparation sur l’intégration hello de toocomplete tous les serveurs d’administration.  les opérations de réparation Hello sont gérés toominimize temps d’arrêt.
    ![Administrateur du fournisseur de ressources App Service - Rôles - Serveur d’administration - Tout réparer][6]

<!--Image references-->
[1]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin.png
[2]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-source-control-configuration.png
[3]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-github-developer-applications.png
[4]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-github-register-a-new-oauth-application-populated.png
[5]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-github-register-a-new-oauth-application-complete.png
[6]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-roles-management-server-repair-all.png
[7]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-bitbucket-dashboard.png
[8]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-bitbucket-access-management-add-oauth-consumer.png
[9]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-bitbucket-access-management-add-oauth-consumer-complete.png
[10]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Onedrive-applications.png
[11]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Onedrive-application-registration.png
[12]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Onedrive-application-platform.png
[13]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Onedrive-application-graph-permissions.png
[14]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Dropbox-applications.png
[15]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Dropbox-application-registration.png
[16]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Dropbox-application-configuration.png
