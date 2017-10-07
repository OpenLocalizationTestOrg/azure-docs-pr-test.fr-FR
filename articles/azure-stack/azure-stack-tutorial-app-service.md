---
title: "aaaMake web, mobiles et utilisateurs d’Azure pile API apps tooyour disponible | Documents Microsoft"
description: "Didacticiel tooinstall hello du fournisseur de ressources du Service d’applications et créer des offres donnent votre Azure pile utilisateurs hello capacité toocreate, mobile, applications web et API."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/03/2017
ms.author: erikje
ms.custom: mvc
ms.openlocfilehash: 62b86cf6288b8f629bc92dade003c712fe523187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="make-web-mobile-and-api-apps-available-tooyour-azure-stack-users"></a>Rendre web, mobiles et utilisateurs d’Azure pile API apps tooyour disponibles

En tant qu’un administrateur de cloud Azure Stack, vous pouvez créer des offres qui permettent à vos utilisateurs (locataires) de créer des applications Azure Functions, web, mobiles et API. En fournissant un accès aux utilisateurs de tooyour toothese applications cloud à la demande, vous pouvez enregistrer les temps et des ressources. tooset cet accès, vous allez :

> [!div class="checklist"]
> * Déployer hello fournisseur de ressources du Service d’applications
> * Créer une offre
> * Offre de hello de test

## <a name="deploy-hello-app-service-resource-provider"></a>Déployer hello fournisseur de ressources du Service d’applications

1. [Préparer l’hôte du Kit de développement de pile Azure hello](azure-stack-app-service-before-you-get-started.md). Cela inclut le déploiement de fournisseur de ressources SQL Server hello, qui est requis pour la création des applications.
2. [Télécharger les scripts d’installation et d’assistance hello](azure-stack-app-service-deploy.md#download-the-required-components).
3. [Exécuter script du programme d’assistance hello toocreate requis certificats](azure-stack-app-service-deploy.md#create-certificates-required-by-app-service-on-azure-stack).
4. [Installer hello fournisseur de ressources du Service d’applications](azure-stack-app-service-deploy.md#use-the-installer-to-download-and-install-app-service-on-azure-stack) (prendra quelques heures tooinstall et, pour tous les hello tooappear des rôles de travail).
5. [Valider l’installation de hello](azure-stack-app-service-deploy.md#validate-the-app-service-on-azure-stack-installation).

## <a name="create-an-offer"></a>Créer une offre

Vous pouvez créer une offre qui, par exemple, permet aux utilisateurs de créer des systèmes de gestion de contenu web DNN. Il requiert le service de SQL Server hello qui vous est déjà activé en installant le fournisseur de ressources SQL Server hello.

1.  [Définissez un quota](azure-stack-setting-quotas.md) et nommez-le *AppServiceQuota*. Sélectionnez **Microsoft.Web** pour hello **Namespace** champ.
2.  [Créer un plan](azure-stack-create-plan.md). Nommez-le *TestAppServicePlan*, sélectionnez Bonjour Bonjour **Microsoft.SQL** service, et **AppService Quota** quota.

    > [!NOTE]
    > toolet utilisateurs créer d’autres applications, d’autres services peuvent être nécessaires dans le plan de hello. Par exemple, les fonctions Azure requiert ce plan hello inclure hello **Microsoft.Storage** de service, tandis que Wordpress requiert **Microsoft.MySQL**.
    > 
    >

3.  [Créer une offre](azure-stack-create-offer.md), nommez-le **TestAppServiceOffer** et sélectionnez hello **TestAppServicePlan** plan.

## <a name="test-hello-offer"></a>Offre de hello de test

Maintenant que vous avez déployé hello fournisseur de ressources du Service d’applications et créé une offre, vous pouvez vous connecter en tant qu’utilisateur, s’abonner toohello offre et créer une application. Pour cet exemple, nous allons créer un système de gestion de contenu de plateforme DNN. Vous devez d’abord créer une base de données SQL, puis l’application hello profonds DNN web.

### <a name="subscribe-toohello-offer"></a>S’abonner toohello offre
1. Se connecter toohello le portail Azure pile (https://portal.local.azurestack.external) en tant que client.
2. Cliquez sur **Prendre un abonnement** > tapez **TestAppServiceSubscription** sous **’** > **Sélectionner une offre** > **TestAppServiceOffer** > **Créer**.

### <a name="create-a-sql-database"></a>Créer une base de données SQL

1. Cliquez sur **+** > **Données et stockage** > **Base de données SQL**.
2. Conservez les valeurs par défaut de la hello pour les champs de hello, sauf comme suit :
    - **Nom de la base de données** : DNNdb
    - **Taille maximale (en Mo)** : 100
    - **Abonnement**: TestAppServiceOffer
    - **Groupe de ressources** : DNN-RG
3. Cliquez sur **les paramètres de connexion**, entrez les informations d’identification pour la base de données hello, puis cliquez sur **OK**. Vous allez utiliser ces informations d’identification plus tard dans cette procédure.
4. Cliquez sur **référence (SKU)** > sélectionnez hello SKU SQL que vous avez créé pour le serveur d’hébergement SQL de hello > **OK**.
5. Cliquez sur **Créer**.

### <a name="create-a-dnn-app"></a>Créer une application DNN    

1. Cliquez sur **+** > **Afficher tout** > **Aperçu de la plateforme DNN** > **Créer**.
2. Tapez *DNNapp* sous **Nom de l’application**, puis sélectionnez **TestAppServiceOffer** sous **Abonnement**.
3. Cliquez sur **Configurer les paramètres obligatoires** > **Créer** > tapez un nom de**Plan App Service**.
4. Cliquez sur **Niveau tarifaire** > **F1 Gratuit** > **Sélectionner** > **OK**.
5. Cliquez sur **base de données** et entrez les informations de hello pour la base de données SQL hello que vous avez créé précédemment.
6. Cliquez sur **Créer**.

Dans ce didacticiel, vous avez appris à :

> [!div class="checklist"]
> * Déployer hello fournisseur de ressources du Service d’applications
> * Créer une offre
> * Offre de hello de test

Comment toolearn de didacticiel suivant toohello d’avance pour :

> [!div class="nextstepaction"]
> [Déployer des applications tooAzure et la pile de Azure](azure-stack-solution-pipeline.md)
