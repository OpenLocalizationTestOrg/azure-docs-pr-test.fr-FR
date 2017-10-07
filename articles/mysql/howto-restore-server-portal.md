---
title: "aaaHow tooRestore un serveur de base de données Azure pour MySQL | Documents Microsoft"
description: "Cet article décrit comment un serveur de base de données Azure pour MySQL à l’aide de toorestore hello portail Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 4b990d5b37c5d4924de9571192b923e3c81094ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-mysql-using-hello-azure-portal"></a>Comment tooBackup et restauration d’un serveur de base de données Azure pour l’utilisation de MySQL hello portail Azure

## <a name="backup-happens-automatically"></a>La sauvegarde s’effectue automatiquement
Lors de l’utilisation de base de données Azure pour MySQL, service de base de données hello effectue automatiquement une sauvegarde du service de hello toutes les 5 minutes. 

sauvegardes de Hello sont disponibles pour les 7 jours lors de l’utilisation de niveau de base et de 35 jours lors de l’utilisation de niveau Standard. Pour plus d’informations, consultez [Niveaux de service d’Azure Database pour MySQL](concepts-service-tiers.md)

À l’aide de cette fonctionnalité de sauvegarde automatique vous pouvez restaurer le serveur de hello et toutes ses bases de données dans un nouveau serveur tooan précédemment point-à-temps.

## <a name="restore-in-hello-azure-portal"></a>Restaurer Bonjour portail Azure
Base de données Azure pour MySQL vous permet de toorestore hello server tooa précédent point dans le temps et en tooa une nouvelle copie du serveur de hello. Vous pouvez utiliser cette nouvelle toorecover de serveur à vos données. 

Par exemple, si une table a été accidentellement supprimé à midi aujourd'hui, vous pourriez restaurer temps toohello juste avant midi et les récupérer hello manquant de table et les données à partir de la copie du serveur de hello.

Hello suit restaurer hello exemple server tooa point dans le temps :

1. L’authentification à hello [portail Azure](https://portal.azure.com/)

2. Recherchez votre serveur Azure Database pour MySQL. Dans le volet gauche de hello, sélectionnez **toutes les ressources**, puis sélectionnez votre serveur à partir de la liste de hello.

3.  Dans le haut de hello du Panneau de vue d’ensemble du serveur hello, cliquez sur **restaurer** sur la barre d’outils hello. Panneau de restauration Hello s’ouvre.
![Cliquez sur le bouton Restaurer](./media/howto-restore-server-portal/click-restore-button.png)

4. Remplissez le formulaire de restauration de hello avec les informations de hello requis :

- **(UTC) de point de restauration**: à l’aide du sélecteur de dates hello time picker, sélectionnez un toorestore point-à-temps pour. heure de Hello spécifiée est au format UTC, donc vous devez probablement tooconvert hello local heure en UTC.
- **Restaurer le serveur de toonew**: fournir un nouveau serveur serveur existant de nom toorestore hello dans.
- **Emplacement**: choix de la région de hello remplit avec la région du serveur source hello automatiquement et ne peut pas être modifié.
- **Niveau de tarification**: hello choix du niveau de tarification automatiquement remplit avec hello tarification même niveau en tant que serveur de source de hello et ne peut pas être modifiées ici. 
![Restauration PITR](./media/howto-restore-server-portal/pitr-restore.png)

5. Cliquez sur **OK** toorestore hello server toorestore tooa point dans le temps. 

6. Après la restauration de hello, recherchez hello nouveau serveur qui a été créé hello tooverify bases de données ont été restaurés comme prévu.

## <a name="next-steps"></a>Étapes suivantes
- [Bibliothèques de connexions de la base de données Azure pour MySQL](concepts-connection-libraries.md)