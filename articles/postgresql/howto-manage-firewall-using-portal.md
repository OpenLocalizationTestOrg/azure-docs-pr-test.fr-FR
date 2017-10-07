---
title: "aaaCreate et gérer la base de données Azure PostgreSQL aux règles de pare-feu à l’aide de hello portail Azure | Documents Microsoft"
description: "Créer et gérer la base de données Azure PostgreSQL aux règles de pare-feu à l’aide de hello portail Azure"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 6a41a077168657769e442401e9df9931aa809240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-hello-azure-portal"></a>Créer et gérer la base de données Azure PostgreSQL aux règles de pare-feu à l’aide de hello portail Azure
Les règles de pare-feu de niveau serveur activer administrateurs tooaccess une base de données Azure pour PostgreSQL serveur à partir d’une adresse IP spécifiée ou la plage d’adresses IP. 

## <a name="prerequisites"></a>Composants requis
toostep via ce tooguide de procédure, vous devez :
- Un serveur [Création d’une base de données Azure pour PostgreSQL](quickstart-create-server-database-portal.md)

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>Créer une règle de pare-feu de niveau serveur dans hello portail Azure
1. Sur le panneau serveur PostgreSQL hello, sous paramètres de titre, cliquez sur **sécurité de connexion** Panneau de sécurité de connexion tooopen hello pour hello Azure base de données PostgreSQL.

  ![Portail Azure - cliquez sur Sécurité des connexions](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. Cliquez sur **ajouter une adresse IP Mes** sur la barre d’outils hello. Cela crée une règle automatiquement avec l’adresse IP de hello de votre ordinateur, comme perçue par hello système Azure.

  ![Portail Azure - cliquez sur Ajouter mon adresse IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. Vérifiez votre adresse IP avant d’enregistrer la configuration de hello. Dans certaines situations, adresse IP de hello observée par le portail Azure diffère à partir de l’adresse IP de hello utilisée lorsque l’accès à hello internet et les serveurs Windows Azure. Par conséquent, vous devrez peut-être toochange hello IP de début et de fin IP toomake hello règle fonctionnent comme prévu.
Utiliser un moteur de recherche ou d’autres toocheck de l’outil en ligne de votre adresse IP (par exemple, la recherche Bing « quel est mon IP »).

  ![Recherche Bing « quelle est mon adresse IP »](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. Ajoutez des plages d’adresses supplémentaires. Dans règles de hello pour hello Azure de base de données PostgreSQL pare-feu, vous pouvez spécifier une adresse IP unique, ou une plage d’adresses. Si vous souhaitez toolimit hello règle tooone adresse IP unique, hello type identique à une adresse dans le champ de hello pour IP de début et IP de fin. Ouvrir le pare-feu hello permet aux administrateurs et utilisateurs toologin tooany base de données sur hello PostgreSQL toowhich de serveur disposent des informations d’identification valides.

  ![Portail Azure - règles de pare-feu ](./media/howto-manage-firewall-using-portal/4-specify-addresses.png)

5. Cliquez sur **enregistrer** sur hello toosave de barre d’outils, cette règle de pare-feu de niveau serveur. Attendez la confirmation de hello que les règles de pare-feu toohello hello mise à jour a réussi.

  ![Portail Azure - cliquez sur Enregistrer](./media/howto-manage-firewall-using-portal/5-save-firewall-rule.png)


## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a>Gérer les règles de pare-feu de niveau serveur existante via hello portail Azure
Répétez les règles de pare-feu hello étapes toomanage hello.
* tooadd hello ordinateur en cours, cliquez sur le bouton de hello + **ajouter une adresse IP Mes**. Cliquez sur **enregistrer** modifications de hello toosave.
* tooadd des adresses IP supplémentaires, tapez Bonjour, nom de la règle, adresse IP de début et adresse IP de fin. Cliquez sur **enregistrer** modifications de hello toosave.
* toomodify une règle existante, cliquez sur un des champs hello dans la règle de hello et modifier. Cliquez sur **enregistrer** modifications de hello toosave.
* toodelete une règle existante, sur hello de points de suspension [...], puis cliquez sur Supprimer la règle hello remove. Cliquez sur **enregistrer** modifications de hello toosave.

## <a name="next-steps"></a>Étapes suivantes
- De même, vous pouvez écrire un script trop[créer et gérer la base de données Azure PostgreSQL aux règles de pare-feu à l’aide de CLI d’Azure](howto-manage-firewall-using-cli.md)
- Pour la connexion tooan Azure de base de données PostgreSQL serveur, consultez [bibliothèques de connexions de base de données Azure pour PostgreSQL](concepts-connection-libraries.md)
