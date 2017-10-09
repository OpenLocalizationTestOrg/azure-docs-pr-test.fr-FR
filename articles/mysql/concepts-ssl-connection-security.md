---
title: "connectivité aaaSSL pour la base de données Azure pour MySQL | Documents Microsoft"
description: "Informations de configuration de base de données Azure pour MySQL et les applications associées tooproperly utiliser des connexions SSL"
services: mysql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 6fca7c88fc0f1fd6058d68fcff90fd409abd97a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="ssl-connectivity-in-azure-database-for-mysql"></a><span data-ttu-id="d7fb0-103">Connectivité SSL dans la base de données Azure pour MySQL</span><span class="sxs-lookup"><span data-stu-id="d7fb0-103">SSL connectivity in Azure Database for MySQL</span></span>
<span data-ttu-id="d7fb0-104">Base de données Azure pour MySQL prend en charge la connexion de vos applications tooclient de serveur de base de données à l’aide de Secure Sockets Layer (SSL).</span><span class="sxs-lookup"><span data-stu-id="d7fb0-104">Azure Database for MySQL supports connecting your database server tooclient applications using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="d7fb0-105">Application des connexions SSL entre le serveur de base de données et de vos applications clientes vous aide à protéger contre les attaques de « l’homme au milieu de hello » en chiffrant les flux de données hello entre le serveur de hello et votre application.</span><span class="sxs-lookup"><span data-stu-id="d7fb0-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in hello middle" attacks by encrypting hello data stream between hello server and your application.</span></span>

## <a name="default-settings"></a><span data-ttu-id="d7fb0-106">Paramètres par défaut</span><span class="sxs-lookup"><span data-stu-id="d7fb0-106">Default settings</span></span>
<span data-ttu-id="d7fb0-107">Par défaut, service de base de données hello doit être configuré toorequire des connexions SSL lors de la connexion tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="d7fb0-107">By default, hello database service should be configured toorequire SSL connections when connecting tooMySQL.</span></span>  <span data-ttu-id="d7fb0-108">Il est recommandé d’éviter de désactiver l’option de SSL hello autant que possible.</span><span class="sxs-lookup"><span data-stu-id="d7fb0-108">It is recommended avoid disabling hello SSL option whenever possible.</span></span> 

<span data-ttu-id="d7fb0-109">Lors de la configuration d’une nouvelle base de données Azure pour le serveur MySQL via hello portail Azure et l’interface CLI, mise en œuvre de connexions SSL est activé par défaut.</span><span class="sxs-lookup"><span data-stu-id="d7fb0-109">When provisioning a new Azure Database for MySQL server through hello Azure portal and CLI, enforcement of SSL connections is enabled by default.</span></span> 

<span data-ttu-id="d7fb0-110">De même, les chaînes de connexion qui sont prédéfinis dans les paramètres de « Chaînes de connexion » hello sous votre serveur Bonjour Azure portal incluent des paramètres de hello requis courantes langues tooconnect tooyour serveur de base de l’utilisation de SSL.</span><span class="sxs-lookup"><span data-stu-id="d7fb0-110">Likewise, connection strings that are pre-defined in hello "Connection Strings" settings under your server in hello Azure portal include hello required parameters for common languages tooconnect tooyour database server using SSL.</span></span> <span data-ttu-id="d7fb0-111">Hello paramètre SSL varie en fonction de connecteur de hello, par exemple « ssl = true » ou « sslmode = nécessitent » ou « sslmode = requis » et d’autres variations.</span><span class="sxs-lookup"><span data-stu-id="d7fb0-111">hello SSL parameter varies based on hello connector, for example "ssl=true" or "sslmode=require" or "sslmode=required" and other variations.</span></span>

<span data-ttu-id="d7fb0-112">toolearn comment tooenable ou désactiver connexion SSL lors du développement d’application, consultez trop[comment tooconfigure SSL](howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="d7fb0-112">toolearn how tooenable or disable SSL connection when developing application, please refer too[How tooconfigure SSL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7fb0-113">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d7fb0-113">Next steps</span></span>
[<span data-ttu-id="d7fb0-114">Bibliothèques de connexions de la base de données Azure pour MySQL</span><span class="sxs-lookup"><span data-stu-id="d7fb0-114">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)
