---
title: "aaaCreate et gérer la base de données Azure pour MySQL server à l’aide du portail Azure | Documents Microsoft"
description: "Cet article décrit comment vous pouvez rapidement créer une nouvelle base de données Azure pour le serveur MySQL et gérer le serveur hello à l’aide de hello portail Azure."
services: mysql
author: v-chenyh
ms.author: nolanwu
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: c532df43b3d2124d7bd34875b32d52357f162af8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-server-using-azure-portal"></a>Création et gestion d’un serveur Azure Database pour MySQL à l’aide du portail Azure
Cet article décrit comment vous pouvez rapidement créer une nouvelle base de données Azure pour le serveur MySQL et gérer le serveur hello à l’aide de hello portail Azure. Gestion des serveurs inclut l’affichage des détails du serveur et les bases de données, de la réinitialisation de mot de passe et de suppression du serveur de hello.

## <a name="log-in-toohello-azure-portal"></a>Ouvrez une session dans toohello portail Azure
Connectez-vous à toohello [portail Azure](https://portal.azure.com).

## <a name="create-an-azure-database-for-mysql-server"></a>Créer un serveur de base de données Azure pour MySQL
Suivez ces étapes de toocreate serveur MySQL nommé « mysqlserver4demo » dans une base de données Azure

1-click **nouveau** bouton se trouve sur le coin supérieur gauche hello Hello portail Azure.

2-Sélectionnez **bases de données** à partir de la nouvelle page de hello, puis sélectionnez **base de données Azure pour MySQL** à partir de la page de bases de données hello.

> Un serveur Azure Database pour MySQL est créé avec un ensemble défini de [ressources de calcul et de stockage](./concepts-compute-unit-and-storage.md). base de données Hello est créé dans un groupe de ressources Azure et dans une base de données Azure pour le serveur MySQL.

![create-new-server](./media/howto-create-manage-server-portal/create-new-server.png)

3 - remplir hello Azure de base de données MySQL formulaire avec hello informations suivantes :

| **Champ de formulaire** | **Description du champ** |
|----------------|-----------------------|
| *Nom du serveur* | azure-mysql (le nom du serveur est globalement unique) |
| *Abonnement* | MySQLaaS (sélectionnez une option dans le menu déroulant) |
| *Groupe de ressources* | myresource (créez un nouveau groupe de ressources ou utilisez un groupe existant) |
| *Connexion d’administrateur serveur* | myadmin (nom du compte administrateur de l’installation) |
| *Mot de passe* | mot de passe du compte administrateur de l’installation |
| *Confirmer le mot de passe* | confirmez le mot de passe du compte administrateur |
| *Emplacement* | Europe du Nord (sélection Europe du Nord ou États-Unis de l'Ouest) |
| *Version* | 5.6 (choisissez la version du serveur Azure Database pour MySQL) |

4-Cliquez **niveau tarifaire** toospecify hello performances et la couche de niveau de service pour votre nouveau serveur. L’unité de calcul peut être configurée entre 50 et 100 dans le niveau de base, entre 100 et 200 dans le niveau standard, et vous pouvez augmenter le stockage en fonction du montant inclus. Pour ce guide pratique, choisissons 50 unités de calcul et 50 Go. Cliquez sur **OK** toosave votre sélection.
![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)

Cliquez sur 5 **créer** serveur hello de tooprovision. L’approvisionnement prend quelques minutes.

> Vérifiez hello **toodashboard du code confidentiel** option tooallow simplifier le suivi de vos déploiements.
> [!NOTE]
> Bien que les too1000GB dans le niveau de base et 10000 Go dans la norme couche est prises en charge pour le stockage, version préliminaire publique, maximale de stockage hello est toujours limitée too1000GB temporairement. 
</Include>

## <a name="update-an-azure-database-for-mysql-server"></a>Mise à jour d’un serveur Azure Database pour MySQL
Une fois le nouveau serveur est configuré, utilisateur dispose d’un serveur existant 2 options tooedit : réinitialiser le mot de passe administrateur ou d’échelle haut/bas server de hello en modifiant les unités de calcul hello.

### <a name="change-hello-administrator-user-password"></a>Mot de passe de l’utilisateur d’administrateur modification hello
1 - sur le serveur de hello **vue d’ensemble** panneau, cliquez sur **réinitialisation de mot de passe** toopopulate une fenêtre d’entrée et la confirmation de mot de passe.

2 - Entrez le nouveau mot de passe et confirmer le mot de passe hello dans la fenêtre hello comme indiqué ci-dessous : ![réinitialisation de mot de passe](./media/howto-create-manage-server-portal/reset-password.png)

3-Cliquez **OK** toosave hello nouveau mot de passe.

### <a name="scale-updown-by-changing-compute-units"></a>Montée/descente en puissance en modifiant les unités de calcul

1 - sur le panneau de serveur hello, sous **paramètres**, cliquez sur **niveau tarifaire** Panneau de niveau de tarification de hello tooopen pour hello Azure de base de données du serveur MySQL.

Étape 2-Suivez 4 dans **créer une base de données Azure pour le serveur MySQL** toochange les unités de calcul en hello même niveau de tarification.

## <a name="delete-an-azure-database-for-mysql-server"></a>Suppression d’un serveur Azure Database pour MySQL

1 - sur le serveur de hello **vue d’ensemble** panneau, cliquez sur **supprimer** Panneau de confirmation de commande bouton tooopen hello suppression.

Nom de serveur correct 2-type hello dans la zone d’entrée du panneau hello confirmation double.

3-Cliquez **supprimer** bouton Nouveau tooconfirm suppression d’action et attendez que « Suppression de réussite » le menu contextuel sur la barre de notification hello.

## <a name="list-hello-azure-database-for-mysql-databases"></a>Liste hello Azure de base de données pour les bases de données MySQL
Sur le serveur de hello **vue d’ensemble** panneau, faites défiler vers le bas jusqu'à ce que vous voyiez de la base de données hello vignette sous hello. Toutes les bases de données hello seront afficheront dans la table de hello. Cliquez sur **supprimer** Panneau de confirmation de commande bouton tooopen hello suppression.

![show-databases](./media/howto-create-manage-server-portal/show-databases.png)

## <a name="show-details-of-an-azure-database-for-mysql-server"></a>Affichage des détails d’un serveur Azure Database pour MySQL
Cliquez sur **propriétés** sous **paramètres** sur le serveur de hello panneau hello **propriétés** panneau. Vous pouvez afficher toutes les informations détaillées sur les serveur hello.

## <a name="next-steps"></a>Étapes suivantes

[Démarrage rapide : création d’un serveur Azure Database pour MySQL à l’aide du portail Azure](./quickstart-create-mysql-server-database-using-azure-portal.md)
