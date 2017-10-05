---
title: "Connectivité SSL de la base de données Azure pour MySQL | Microsoft Docs"
description: "Informations de configuration de la base de données Azure pour MySQL et des applications associées afin d’utiliser correctement les connexions SSL."
services: mysql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 4b03b3a2dbfad92cc0cfa84777b38ddff90452cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="ssl-connectivity-in-azure-database-for-mysql"></a><span data-ttu-id="55d6d-103">Connectivité SSL dans la base de données Azure pour MySQL</span><span class="sxs-lookup"><span data-stu-id="55d6d-103">SSL connectivity in Azure Database for MySQL</span></span>
<span data-ttu-id="55d6d-104">La base de données Azure pour MySQL prend en charge la connexion de votre serveur de base de données aux applications clientes via SSL (Secure Sockets Layer).</span><span class="sxs-lookup"><span data-stu-id="55d6d-104">Azure Database for MySQL supports connecting your database server to client applications using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="55d6d-105">L’application de connexions SSL entre votre serveur de base de données et vos applications clientes vous protège contre les « attaques de l’intercepteur » en chiffrant le flux de données entre le serveur et votre application.</span><span class="sxs-lookup"><span data-stu-id="55d6d-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in the middle" attacks by encrypting the data stream between the server and your application.</span></span>

## <a name="default-settings"></a><span data-ttu-id="55d6d-106">Paramètres par défaut</span><span class="sxs-lookup"><span data-stu-id="55d6d-106">Default settings</span></span>
<span data-ttu-id="55d6d-107">Par défaut, le service de base de données doit être configuré pour exiger des connexions SSL lors de la connexion à MySQL.</span><span class="sxs-lookup"><span data-stu-id="55d6d-107">By default, the database service should be configured to require SSL connections when connecting to MySQL.</span></span>  <span data-ttu-id="55d6d-108">Il est recommandé d’éviter de désactiver l’option SSL dans la mesure du possible.</span><span class="sxs-lookup"><span data-stu-id="55d6d-108">It is recommended avoid disabling the SSL option whenever possible.</span></span> 

<span data-ttu-id="55d6d-109">Lorsque vous approvisionnez un nouveau serveur de base de données Azure pour MySQL par le biais du Portail Azure et d’Azure CLI, l’application de connexions SSL est activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="55d6d-109">When provisioning a new Azure Database for MySQL server through the Azure portal and CLI, enforcement of SSL connections is enabled by default.</span></span> 

<span data-ttu-id="55d6d-110">De même, les chaînes de connexion prédéfinies dans les paramètres « Chaînes de connexion » du serveur sur le Portail Azure incluent les paramètres requis par les langages courants pour se connecter au serveur de base de données via SSL.</span><span class="sxs-lookup"><span data-stu-id="55d6d-110">Likewise, connection strings that are pre-defined in the "Connection Strings" settings under your server in the Azure portal include the required parameters for common languages to connect to your database server using SSL.</span></span> <span data-ttu-id="55d6d-111">Le paramètre SSL varie en fonction du connecteur, par exemple « ssl=true », « sslmode=require » ou « sslmode=require » et d’autres variations.</span><span class="sxs-lookup"><span data-stu-id="55d6d-111">The SSL parameter varies based on the connector, for example "ssl=true" or "sslmode=require" or "sslmode=required" and other variations.</span></span>

<span data-ttu-id="55d6d-112">Pour savoir comment activer ou désactiver la connexion SSL pour le développement d’applications, consultez la page [Guide pratique : configurer SSL](howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="55d6d-112">To learn how to enable or disable SSL connection when developing application, please refer to [How to configure SSL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="55d6d-113">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="55d6d-113">Next steps</span></span>
[<span data-ttu-id="55d6d-114">Bibliothèques de connexions de la base de données Azure pour MySQL</span><span class="sxs-lookup"><span data-stu-id="55d6d-114">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)
