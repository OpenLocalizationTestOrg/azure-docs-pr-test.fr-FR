---
title: "aaaCreate et gérer la base de données Azure MySQL aux règles de pare-feu à l’aide de hello portail Azure | Documents Microsoft"
description: "Créer et gérer la base de données Azure MySQL aux règles de pare-feu à l’aide de hello portail Azure"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 30dbdde4299df564fbf6581419e908186fe3b823
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-hello-azure-portal"></a>Créer et gérer la base de données Azure MySQL aux règles de pare-feu à l’aide de hello portail Azure
Les règles de pare-feu de niveau serveur activer administrateurs tooaccess une base de données Azure pour MySQL Server à partir d’une adresse IP spécifiée ou la plage d’adresses IP. 

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>Créer une règle de pare-feu de niveau serveur dans hello portail Azure

1. Sur le panneau de serveur MySQL hello, sous paramètres de titre, cliquez sur **sécurité de connexion** Panneau de sécurité de connexion tooopen hello pour hello Azure de base de données de MySQL.

   ![Portail Azure - cliquez sur Sécurité des connexions](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. Cliquez sur **ajouter une adresse IP Mes** sur la barre d’outils de hello toocreate une règle avec l’adresse IP de hello de votre ordinateur, comme perçue par hello système Azure.

   ![Portail Azure - cliquez sur Ajouter mon adresse IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. Vérifiez votre adresse IP avant d’enregistrer la configuration de hello. Dans certaines situations, adresse IP de hello observée par le portail Azure diffère à partir de l’adresse IP de hello utilisée lorsque l’accès à hello internet et les serveurs Windows Azure. Par conséquent, vous devrez peut-être toochange hello IP de début et de fin IP toomake hello règle fonctionnent comme prévu.

   Utiliser un moteur de recherche ou d’autres toocheck de l’outil en ligne de votre adresse IP (par exemple, recherchez « quel est mon adresse IP »).

   ![Recherche Bing « quelle est mon adresse IP »](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. Ajoutez des plages d’adresses supplémentaires. Dans règles de hello pour hello Azure de base de données MySQL pare-feu, vous pouvez spécifier une adresse IP unique, ou une plage d’adresses. Si vous souhaitez toolimit hello règle tooone adresse IP unique, hello type identique à une adresse dans le champ de hello pour IP de début et IP de fin. Ouvrir le pare-feu hello permet tooaccess administrateurs et utilisateurs chaque base de données hello toowhich de serveur MySQL comportant des informations d’identification valides.

   ![Portail Azure - règles de pare-feu ](./media/howto-manage-firewall-using-portal/5-specify-addresses.png)


5. Cliquez sur **enregistrer** sur hello toosave de barre d’outils, cette règle de pare-feu de niveau serveur. Attendez la confirmation de hello que les règles de pare-feu toohello hello mise à jour a réussi.

   ![Portail Azure - cliquez sur Enregistrer](./media/howto-manage-firewall-using-portal/4-save-firewall-rule.png)

## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a>Gérer les règles de pare-feu de niveau serveur existante via hello portail Azure
Répétez les règles de pare-feu hello étapes toomanage hello.
* tooadd hello ordinateur en cours, cliquez sur **+ ajouter Mes IP**.
* les adresses IP supplémentaires tooadd, tapez Bonjour **nom de la règle**, **IP de début**, et **IP de fin**.
* toomodify une règle existante, cliquez sur un des champs hello dans la règle de hello et modifier.
* règle de toodelete existant sur hello de points de suspension [...] et cliquez sur **supprimer**.
* Cliquez sur **enregistrer** modifications de hello toosave.

## <a name="next-steps"></a>Étapes suivantes
- Pour vous aider à la connexion tooan base de données Azure pour le serveur MySQL, consultez [bibliothèques de connexions de base de données Azure pour MySQL](./concepts-connection-libraries.md)
