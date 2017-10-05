---
title: "Connecter un service Azure App Service existant à une base de données Azure pour MySQL | Microsoft Docs"
description: "Instructions pour connecter correctement un service Azure App Service existant à une base de données Azure pour MySQL"
services: mysql
author: v-chenyh
ms.author: v-chenyh
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 735e21e8135d67405ec6b88d75be1711a2f071f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-an-existing-azure-app-service-to-azure-database-for-mysql-server"></a>Connecter un service Azure App Service existant à un serveur de base de données Azure pour MySQL
Ce document explique comment connecter un service Azure App Service existant à votre serveur de base de données Azure pour MySQL.

## <a name="before-you-begin"></a>Avant de commencer
Connectez-vous au [portail Azure](https://portal.azure.com). Créez un serveur de base de données Azure pour MySQL. Pour plus d’informations, reportez-vous à [Guide pratique pour créer un serveur de base de données Azure pour MySQL à partir du portail](quickstart-create-mysql-server-database-using-azure-portal.md) ou à [Guide pratique pour créer un serveur de base de données Azure pour MySQL à l’aide de l’interface CLI](quickstart-create-mysql-server-database-using-azure-cli.md).

Il existe actuellement deux solutions pour activer l’accès à partir d’un service Azure App Service vers une base de données Azure pour MySQL. Ces deux solutions impliquent de configurer des règles de pare-feu au niveau du serveur.

## <a name="solution-1---create-a-firewall-rule-to-allow-all-ips"></a>Solution 1 - Créer une règle de pare-feu pour autoriser toutes les adresses IP
La base de données Azure pour MySQL fournit une sécurité d’accès à l’aide d’un pare-feu afin de protéger vos données. Lors de la connexion d’un service Azure App Service à une base de données Azure pour MySQL, gardez à l’esprit que les adresses IP sortantes d’App Service sont dynamiques par nature. 

Pour garantir la disponibilité de votre service Azure App Service, nous recommandons d’utiliser cette solution pour autoriser TOUTES les adresses IP.

> [!NOTE]
> Microsoft travaille à une solution à long terme pour éviter d’autoriser toutes les adresses IP des services Azure à se connecter à la base de données Azure pour MySQL.

1. Dans le panneau du serveur MySQL, sous le titre Paramètres, cliquez sur **Sécurité des connexions** afin d’ouvrir le panneau Sécurité des connexions pour la base de données Azure pour MySQL.

   ![Portail Azure - cliquez sur Sécurité des connexions](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. Entrez **NOM DE LA RÈGLE**, **ADRESSE IP DE DÉBUT** et **ADRESSE IP DE FIN**. Cliquez ensuite sur **Enregistrer**.
   - Nom de la règle : Allow-All-IPs
   - Adresse IP de début : 0.0.0.0
   - Adresse IP de fin : 255.255.255.255

   ![Portail Azure - Ajouter toutes les adresses IP](./media/howto-connect-webapp/1_2-add-all-ips.png)

## <a name="solution-2---create-a-firewall-rule-to-explicitly-allow-outbound-ips"></a>Solution 2 - Créer une règle de pare-feu pour autoriser explicitement des adresses IP sortantes
Vous pouvez ajouter explicitement toutes les adresses IP sortantes de votre service Azure App Service.

1. Dans le panneau Propriétés d’App Service, affichez votre **ADRESSE IP SORTANTE**.

   ![Portail Azure - Afficher des adresses IP sortantes](./media/howto-connect-webapp/2_1-outbound-ip-address.png)

2. Dans le panneau Sécurité de la connexion de MySQL, ajoutez une par une des adresses IP sortantes.

   ![Portail Azure - Ajouter des adresses IP explicites](./media/howto-connect-webapp/2_2-add-explicit-ips.png)

3. N’oubliez pas d’**Enregistrer** vos règles de pare-feu.

Bien que le service Azure App Service tente de maintenir les adresses IP constantes au fil du temps, il existe des cas où les adresses IP peuvent changer. Par exemple, quand l’application est recyclée, qu’une opération de mise à l’échelle se produit ou que de nouvelles machines sont ajoutées dans des centres de données régionaux Azure pour augmenter la capacité. Quand les adresses IP changent, l’application peut subir des temps d’arrêt s’il ne peut plus se connecter au serveur MySQL. Envisagez cette éventualité lors du choix de l’une des solutions précédentes.

## <a name="ssl-configuration"></a>Configuration SSL
SSL est activé par défaut sur la base de données Azure pour MySQL. Si votre application n’utilise pas le protocole SSL pour se connecter à la base de données, vous devez le désactiver sur le serveur MySQL. Pour plus d’informations sur la configuration de SSL, consultez [Utilisation de SSL avec une base de données Azure pour MySQL](howto-configure-ssl.md).

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur les chaînes de connexion, reportez-vous à [Chaînes de connexions](howto-connection-string.md).
