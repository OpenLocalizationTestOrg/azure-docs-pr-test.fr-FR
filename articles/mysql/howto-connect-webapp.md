---
title: "aaaConnect existant du Service d’applications Azure tooAzure base de données MySQL | Documents Microsoft"
description: "Instructions de la tooproperly connexion d’un tooAzure Azure App Service existant de base de données pour MySQL"
services: mysql
author: v-chenyh
ms.author: v-chenyh
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 6d5b16f316e186d665370adcd8b7c7bb38c8d51a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-an-existing-azure-app-service-tooazure-database-for-mysql-server"></a>Se connecter à un tooAzure Azure App Service existant de base de données du serveur MySQL
Ce document explique comment tooconnect un tooyour Azure App Service existant Azure de base de données du serveur MySQL.

## <a name="before-you-begin"></a>Avant de commencer
Connectez-vous à toohello [portail Azure](https://portal.azure.com). Créez un serveur de base de données Azure pour MySQL. Pour plus d’informations, consultez trop[comment toocreate Azure de base de données MySQL server à partir du portail](quickstart-create-mysql-server-database-using-azure-portal.md) ou [comment toocreate Azure de base de données MySQL server à l’aide de CLI](quickstart-create-mysql-server-database-using-azure-cli.md).

Il existe actuellement deux solutions tooenable d’accès à partir d’un base de données Azure du tooan Azure App Service pour MySQL. Ces deux solutions impliquent de configurer des règles de pare-feu au niveau du serveur.

## <a name="solution-1---create-a-firewall-rule-tooallow-all-ips"></a>Solution 1 : créer un tooallow de règle de pare-feu toutes les adresses IP
Base de données Azure pour MySQL fournit la sécurité d’accès à l’aide d’un pare-feu tooprotect vos données. Lors de la connexion à partir d’un tooAzure Azure App Service de base de données du serveur MySQL, gardez à l’esprit que hello sortant des adresses IP du Service d’applications sont dynamiques par nature. 

disponibilité de hello tooensure de votre Service d’applications Azure, nous recommandons d’utiliser cette tooallow solution toutes les adresses IP.

> [!NOTE]
> Microsoft s’emploie pour un tooavoid solution à long terme consistant à autoriser toutes les adresses IP pour les services Azure tooconnect tooAzure base de données MySQL.

1. Sur le panneau de serveur MySQL hello, sous paramètres de titre, cliquez sur **sécurité de connexion** Panneau de sécurité de connexion tooopen hello pour hello Azure de base de données de MySQL.

   ![Portail Azure - cliquez sur Sécurité des connexions](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. Entrez **NOM DE LA RÈGLE**, **ADRESSE IP DE DÉBUT** et **ADRESSE IP DE FIN**. Cliquez ensuite sur **Enregistrer**.
   - Nom de la règle : Allow-All-IPs
   - Adresse IP de début : 0.0.0.0
   - Adresse IP de fin : 255.255.255.255

   ![Portail Azure - Ajouter toutes les adresses IP](./media/howto-connect-webapp/1_2-add-all-ips.png)

## <a name="solution-2---create-a-firewall-rule-tooexplicitly-allow-outbound-ips"></a>Solution 2 : création d’un pare-feu tooexplicitly de règle Autoriser les adresses IP sortante
Vous pouvez ajouter explicitement que tous les hello sortant adresses IP de votre Service d’applications Azure.

1. Sur le panneau des propriétés de Service d’application hello, affichez votre **adresse IP sortante**.

   ![Portail Azure - Afficher des adresses IP sortantes](./media/howto-connect-webapp/2_1-outbound-ip-address.png)

2. Dans Panneau de sécurité de connexion MySQL hello, ajouter des adresses IP sortant un par un.

   ![Portail Azure - Ajouter des adresses IP explicites](./media/howto-connect-webapp/2_2-add-explicit-ips.png)

3. N’oubliez pas trop**enregistrer** vos règles de pare-feu.

Si hello Azure App service tente de tookeep IP adresses constante au fil du temps, il existe des cas où les adresses IP de hello peuvent changer. Par exemple, hello lorsque les recyclages de l’application ou une opération de mise à l’échelle se produit lorsque les nouveaux ordinateurs sont ajoutés dans les données régionales Azure centres de capacité de hello tooincrease. Lors de la modification des adresses IP de hello, application hello peut rencontrer des temps d’arrêt dans l’événement hello il peut ne plus se connecter toohello MySQL server. Envisagez cette possibilité lorsque vous choisissez une des hello précédant les solutions.

## <a name="ssl-configuration"></a>Configuration SSL
SSL est activé par défaut sur la base de données Azure pour MySQL. Si votre application n’utilise pas de base de données SSL tooconnect toohello, vous devez toodisable SSL sur le serveur MySQL. Pour plus d’informations sur la façon de tooconfigure SSL, voir [à l’aide de SSL avec la base de données Azure pour MySQL](howto-configure-ssl.md).

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur les chaînes de connexion, consultez trop[les chaînes de connexion](howto-connection-string.md).
