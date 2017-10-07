---
title: "aaaMake SQL des bases de données utilisateurs d’Azure pile disponible tooyour | Documents Microsoft"
description: "Didacticiel tooinstall hello du fournisseur de ressources SQL Server et créer des offres qui permettent de créer des bases de données SQL Azure pile utilisateurs."
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
ms.openlocfilehash: 778513ba982981895afe2d57b3b5dda71ead8886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="make-sql-databases-available-tooyour-azure-stack-users"></a>Rendre les bases de données SQL utilisateurs d’Azure pile tooyour disponibles

En tant qu’administrateur de cloud Azure Stack, vous pouvez créer des offres qui permettent aux utilisateurs de créer des bases de données SQL qu’ils peuvent utiliser avec leurs applications cloud natives, sites web et charges de travail. En fournissant ces personnalisé, à la demande, les utilisateurs de bases de données en nuage tooyour, vous pouvez enregistrer les temps et des ressources. tooset cet accès, vous allez :

> [!div class="checklist"]
> * Déployer le fournisseur de ressources SQL Server hello
> * Créer une offre
> * Offre de hello de test

## <a name="deploy-hello-sql-server-resource-provider"></a>Déployer le fournisseur de ressources SQL Server hello

processus de déploiement Hello est décrit en détail dans hello [bases de données SQL d’utilisation sur un article de la pile de Azure](azure-stack-sql-resource-provider-deploy.md)et est composé de hello principal comme suit :

1.  [Déployer le fournisseur de ressources SQL hello]( azure-stack-sql-resource-provider-deploy.md#deploy-the-resource-provider).
2.  [Vérifier le déploiement de hello]( azure-stack-sql-resource-provider-deploy.md#verify-the-deployment-using-the-azure-stack-portal).
3.  [Fournir une capacité en vous connectant tooa hébergeant SQL server]( azure-stack-sql-resource-provider-deploy.md#provide-capacity-by-connecting-to-a-hosting-sql-server).

## <a name="create-an-offer"></a>Créer une offre

1.  [Définissez un quota](azure-stack-setting-quotas.md) et nommez-le *SQLServerQuota*. Sélectionnez **Microsoft.SQLAdapter** pour hello **Namespace** champ.
2.  [Créer un plan](azure-stack-create-plan.md). Nommez-le *TestSQLServerPlan*, sélectionnez hello **Microsoft.SQLAdapter** service, et **SQLServerQuota** quota.

    > [!NOTE]
    > toolet utilisateurs créer d’autres applications, d’autres services peuvent être nécessaires dans le plan de hello. Par exemple, les fonctions Azure requiert ce plan hello inclure hello **Microsoft.Storage** de service, tandis que Wordpress requiert **Microsoft.MySQLAdapter**.
    > 
    >

3.  [Créer une offre](azure-stack-create-offer.md), nommez-le **TestSQLServerOffer** et sélectionnez hello **TestSQLServerPlan** plan.

## <a name="test-hello-offer"></a>Offre de hello de test

Maintenant que vous avez déployé le fournisseur de ressources SQL Server hello et créé une offre, vous pouvez vous connecter en tant qu’utilisateur, s’abonner toohello offre et créer une base de données.

### <a name="subscribe-toohello-offer"></a>S’abonner toohello offre
1. Se connecter toohello le portail Azure pile (https://portal.local.azurestack.external) en tant que client.
2. Cliquez sur **Prendre un abonnement**, puis tapez **TestSQLServerSubscription** sous **Nom d’affichage**.
3. Cliquez sur **Sélectionner une offre** > **TestSQLServerOffer** > **Créer**.
4. Cliquez sur **Plus de services** > **Abonnements** > **TestSQLServerSubscription** > **Fournisseurs de ressources**.
5. Cliquez sur **inscrire** toohello suivant **Microsoft.SQLAdapter** fournisseur.

### <a name="create-a-sql-database"></a>Créer une base de données SQL

1. Cliquez sur **+** > **Données et stockage** > **Base de données SQL**.
2. Valeurs par défaut de congé hello pour les champs hello, ou vous peuvent utiliser ces exemples :
    - **Nom de la base de données** : SQLdb
    - **Taille maximale (en Mo)** : 100
    - **Abonnement** : TestSQLOffer
    - **Groupe de ressources** : SQL-RG
3. Cliquez sur **les paramètres de connexion**, entrez les informations d’identification pour la base de données hello, puis cliquez sur **OK**.
4. Cliquez sur **référence (SKU)** > sélectionnez hello SKU SQL que vous avez créé pour le serveur d’hébergement SQL de hello > **OK**.
5. Cliquez sur **Créer**.

Dans ce didacticiel, vous avez appris à :

> [!div class="checklist"]
> * Déployer le fournisseur de ressources SQL Server hello
> * Créer une offre
> * Offre de hello de test

Comment toolearn de didacticiel suivant toohello d’avance pour :

> [!div class="nextstepaction"]
> [Que web, mobiles et les utilisateurs de API apps tooyour disponibles]( azure-stack-tutorial-app-service.md)

