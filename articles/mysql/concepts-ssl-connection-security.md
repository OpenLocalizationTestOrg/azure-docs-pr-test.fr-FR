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
# <a name="ssl-connectivity-in-azure-database-for-mysql"></a>Connectivité SSL dans la base de données Azure pour MySQL
Base de données Azure pour MySQL prend en charge la connexion de vos applications tooclient de serveur de base de données à l’aide de Secure Sockets Layer (SSL). Application des connexions SSL entre le serveur de base de données et de vos applications clientes vous aide à protéger contre les attaques de « l’homme au milieu de hello » en chiffrant les flux de données hello entre le serveur de hello et votre application.

## <a name="default-settings"></a>Paramètres par défaut
Par défaut, service de base de données hello doit être configuré toorequire des connexions SSL lors de la connexion tooMySQL.  Il est recommandé d’éviter de désactiver l’option de SSL hello autant que possible. 

Lors de la configuration d’une nouvelle base de données Azure pour le serveur MySQL via hello portail Azure et l’interface CLI, mise en œuvre de connexions SSL est activé par défaut. 

De même, les chaînes de connexion qui sont prédéfinis dans les paramètres de « Chaînes de connexion » hello sous votre serveur Bonjour Azure portal incluent des paramètres de hello requis courantes langues tooconnect tooyour serveur de base de l’utilisation de SSL. Hello paramètre SSL varie en fonction de connecteur de hello, par exemple « ssl = true » ou « sslmode = nécessitent » ou « sslmode = requis » et d’autres variations.

toolearn comment tooenable ou désactiver connexion SSL lors du développement d’application, consultez trop[comment tooconfigure SSL](howto-configure-ssl.md).

## <a name="next-steps"></a>Étapes suivantes
[Bibliothèques de connexions de la base de données Azure pour MySQL](concepts-connection-libraries.md)
