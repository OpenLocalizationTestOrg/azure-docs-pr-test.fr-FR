---
title: "Configurer des sources de déploiement pour App Services sur Azure Stack | Microsoft Docs"
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
ms.date: 10/10/2017
ms.author: anwestg
ms.openlocfilehash: dc341d872a3b8943a934217ace21537f45bafd10
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/08/2017
---
# <a name="configure-deployment-sources"></a>Configurer des sources de déploiement

App Service sur Azure Stack prend en charge le déploiement à la demande à partir de plusieurs fournisseurs de contrôle de code source. Cette fonctionnalité permet aux développeurs d’applications d’effectuer un déploiement directement à partir de leurs référentiels de contrôle de code source. Si les utilisateurs veulent configurer App Service pour se connecter à leurs référentiels, les opérateurs doivent d’abord configurer l’intégration entre App Service sur Azure Stack et le fournisseur de contrôle de code source.  

Les fournisseurs de contrôle de code source pris en charge, en plus du Git local, sont les suivants :

* GitHub
* BitBucket
* OneDrive
* DropBox

## <a name="view-deployment-sources-in-app-service-administration"></a>Afficher les sources de déploiement dans l’administration App Service

1. Connectez-vous au portail d’administration Azure Stack (https://adminportal.local.azurestack.external) en tant qu’administrateur du service.
2. Accédez à **Fournisseurs de ressources** et sélectionnez **App Service Resource Provider Admin** (Administrateur du fournisseur de ressources App Service).  ![Administrateur du fournisseur de ressources App Service][1]
3. Cliquez sur **Source control configuration** (Configuration du contrôle de code source).  La liste de toutes les sources de déploiement configurées s’affiche.
    ![Configuration du contrôle de code source de l’administrateur du fournisseur de ressources App Service][2]

## <a name="configure-github"></a>Configurer GitHub

Vous avez besoin d’un compte GitHub pour effectuer cette tâche. Vous voudrez peut-être utiliser un compte d’entreprise, plutôt qu’un compte personnel.

1. Connectez-vous à GitHub, recherchez https://www.github.com/settings/developers, puis cliquez sur **Register a new application** (Inscrire une nouvelle application).
    ![GitHub - Inscrire une nouvelle application][3]
2. Entrez un **nom d’application**, par exemple, App Service sur Azure Stack.
3. Entrez **l’URL de la page d’accueil**. L’URL de la page d’accueil doit être l’adresse du portail Azure Stack. Par exemple, https://portal.local.azurestack.external.
4. Entrez une **description de l’application**.
5. Entrez **l’URL de rappel d’autorisation**.  Dans un déploiement Azure Stack par défaut, l’URL est au format https://portal.local.azurestack.external/TokenAuthorize, si l’exécution a lieu dans un autre domaine, remplacez votre domaine pour azurestack.local.
    ![GitHub - inscrire une nouvelle application avec des valeurs remplies][4]
6. Cliquez sur **Inscrire l’application**.  Vous avez à présent accès à une page répertoriant **l’ID client** et la **clé secrète client** de l’application.
    ![GitHub - Inscription de l’application terminée][5]
7.  Dans un nouvel onglet ou une nouvelle fenêtre du navigateur, connectez-vous au portail d’administration Azure Stack (https://adminportal.local.azurestack.external) en tant qu’administrateur du service.
8.  Accédez à **Fournisseurs de ressources** et sélectionnez **App Service Resource Provider Admin** (Administrateur du fournisseur de ressources App Service).
9. Cliquez sur **Source control configuration** (Configuration du contrôle de code source).
10. Copiez et collez **l’ID client** et la **clé secrète client** dans les zones de saisie correspondantes pour GitHub.
11. Cliquez sur **Enregistrer**.

## <a name="configure-bitbucket"></a>Configurer BitBucket

Vous avez besoin d’un compte BitBucket pour effectuer cette tâche. Vous voudrez peut-être utiliser un compte d’entreprise, plutôt qu’un compte personnel.

1. Connectez-vous à BitBucket et accédez à **Intégrations** dans votre compte.
    ![Tableau de bord BitBucket - Intégrations][7]
2. Cliquez sur **OAuth** sous Gestion de l’accès et sur **Add consumer** (Ajouter un consommateur).
    ![BitBucket - Ajouter un consommateur OAuth][8]
3. Entrez un **Nom** pour le consommateur, par exemple, App Service sur Azure Stack.
4. Entrez une **Description** pour l’application.
5. Entrez **l’URL de rappel**.  Dans un déploiement Azure Stack par défaut, l’URL de rappel est au format https://portal.local.azurestack.external/TokenAuthorize, si l’exécution a lieu dans un autre domaine, remplacez votre domaine pour azurestack.local.  L’URL doit respecter la mise en majuscules comme indiqué ici pour une intégration BitBucket réussie.
6. Entrez **l’URL** : cette URL doit être celle du portail Azure Stack, par exemple https://portal.local.azurestack.external.
7. Sélectionnez les **autorisations** requises :
    - **Référentiels** : *Lire*
    - **Webhooks** : *Lire et écrire*
8. Cliquez sur **Enregistrer**.  Cette nouvelle application s’affiche maintenant avec la **clé** et la **clé secrète** sous **OAuth consumers** (Consommateurs OAuth).
    ![Liste des applications BitBucket][9]
9.  Dans un nouvel onglet ou une nouvelle fenêtre du navigateur, connectez-vous au portail d’administration Azure Stack (https://adminportal.local.azurestack.external) en tant qu’administrateur du service.
10.  Accédez à **Fournisseurs de ressources** et sélectionnez **App Service Resource Provider Admin** (Administrateur du fournisseur de ressources App Service).
11. Cliquez sur **Source control configuration** (Configuration du contrôle de code source).
12. Copiez et collez la **clé** dans la zone de saisie **ID client** et la **clé secrète** dans la zone de saisie **Clé secrète client** pour BitBucket.
13. Cliquez sur **Enregistrer**.


## <a name="configure-onedrive"></a>Configurer OneDrive

Vous devez disposer d’un compte Microsoft associé à un compte OneDrive pour effectuer cette tâche.  Vous voudrez peut-être utiliser un compte d’entreprise, plutôt qu’un compte personnel.

> [!NOTE]
> Les comptes OneDrive Entreprise ne sont actuellement pas pris en charge.

1. Accédez à https://apps.dev.microsoft.com/?referrer=https%3A%2F%2Fdev.onedrive.com%2Fapp-registration.htm et connectez-vous à l’aide de votre compte Microsoft.
2. Sous **Mes applications**, cliquez sur **Ajouter une application**.
![Applications OneDrive][10]
3. Entrez un **nom** pour la nouvelle inscription d’application, entrez **App Service sur Azure Stack**, puis cliquez sur **Créer une application**.
4. L’écran suivant répertorie les propriétés de votre nouvelle application. Récupérez l’**ID de l’application**. ![Propriétés de l’application OneDrive][11]
5. Sous **Secrets de l’application**, cliquez sur **Générer un nouveau mot de passe**. Prenez note du **Nouveau mot de passe généré**. Il s’agit de votre secret d’application qui n’est pas récupérable après avoir cliqué sur **OK** à ce stade.
6. Sous **Plateformes**, cliquez sur **Ajouter une plateforme** et sélectionnez **Web**.
7. Entrez **l’URI de redirection**.  Dans un déploiement Azure Stack par défaut, l’URI de redirection est au format https://portal.local.azurestack.external/tokenauthorize, si l’exécution a lieu dans un autre domaine, remplacez votre domaine pour azurestack.local. ![Application OneDrive - Ajouter une plateforme Web][12]
8. Ajouter des **Autorisations pour Microsoft Graph** - **Autorisations déléguées**
    - **Files.ReadWrite.AppFolder**
    - **User.Read**  
      ![Application OneDrive - Autorisations pour Microsoft Graph][13]
9. Cliquez sur **Enregistrer**.
10.  Dans un nouvel onglet ou une nouvelle fenêtre du navigateur, connectez-vous au portail d’administration Azure Stack (https://adminportal.local.azurestack.external) en tant qu’administrateur du service.
11.  Accédez à **Fournisseurs de ressources** et sélectionnez **App Service Resource Provider Admin** (Administrateur du fournisseur de ressources App Service).
12. Cliquez sur **Source control configuration** (Configuration du contrôle de code source).
13. Copiez et collez **l’ID d’application** dans la zone de saisie **ID client** et le **mot de passe** dans la zone de saisie **Clé secrète client** pour OneDrive.
14. Cliquez sur **Enregistrer**.

## <a name="configure-dropbox"></a>Configurer Dropbox

> [!NOTE]
> Vous devez avoir un compte Dropbox pour effectuer cette tâche.  Vous pouvez utiliser un compte d’entreprise, plutôt qu’un compte personnel.

1. Accédez à https://www.dropbox.com/developers/apps et connectez-vous à l’aide de votre compte Dropbox.
2. Cliquez sur **Create app**.

    ![Applications Dropbox][14]

3. Sélectionnez **Dropbox API** (API Dropbox).
4. Définissez le niveau d’accès sur **App Folder** (Dossier d’application).
5. Entrez un **nom** pour votre application.
![Inscription d’une application Dropbox][15]
6. Cliquez sur **Créer une application**.  Une page répertoriant les paramètres de l’application, notamment **Clé d’application** et **Clé secrète d’application** s’affiche.
7. Vérifiez que le **nom du dossier d’application** est défini sur **App Service sur Azure Stack**.
8. Définissez **l’URI de redirection OAuth 2** et cliquez sur **Ajouter**.  Dans un déploiement Azure Stack par défaut, l’URL est au format https://portal.local.azurestack.external/TokenAuthorize, si l’exécution a lieu dans un autre domaine, remplacez votre domaine pour azurestack.local.
![Configuration de l’application Dropbox][16]
9.  Dans un nouvel onglet ou une nouvelle fenêtre du navigateur, connectez-vous au portail d’administration Azure Stack (https://adminportal.local.azurestack.external) en tant qu’administrateur du service.
10.  Accédez à **Fournisseurs de ressources** et sélectionnez **App Service Resource Provider Admin** (Administrateur du fournisseur de ressources App Service).
11. Cliquez sur **Source control configuration** (Configuration du contrôle de code source).
12. Copiez et collez la **clé d’application** dans la zone de saisie **ID client** et la **clé secrète d’application** dans la zone de saisie **Clé secrète client** pour Dropbox.
13. Cliquez sur **Enregistrer**.


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

## <a name="next-steps"></a>Étapes suivantes

Les utilisateurs peuvent désormais utiliser les sources de déploiement pour le [déploiement continu](https://docs.microsoft.com/azure/app-service-web/app-service-continuous-deployment), le [déploiement Git local](https://docs.microsoft.com/azure/app-service-web/app-service-deploy-local-git), et la [synchronisation de dossiers de cloud](https://docs.microsoft.com/azure/app-service-web/app-service-deploy-content-sync).
