---
title: "prend en charge les clients de bas niveau de l’entrepôt de données aaaSQL pour l’audit de données | Documents Microsoft"
description: "En savoir plus sur la prise en charge des clients de niveau inférieur de SQL Data Warehouse pour l’audit des données"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: dfe29ff3-dfeb-4309-83c0-c1a300f4f44e
ms.service: sql-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 377488680eb297c3e9b1dc754c003c5b19b47996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse----downlevel-clients-support-for-auditing-and-dynamic-data-masking"></a>SQL Data Warehouse : prise en charge des clients de niveau inférieur pour l’audit et le masquage dynamique des données (Dynamic Data Masking)
[L’audit](sql-data-warehouse-auditing-overview.md) fonctionne avec les clients SQL qui prennent en charge la redirection TDS.

Tout client qui implémente TDS 7.4 doit également prendre en charge la redirection. Exceptions toothis incluent JDBC 4.0 quelle fonctionnalité de redirection hello n’est pas entièrement pris en charge et fastidieuses pour Node.JS dans lequel la redirection n’était pas implémentée.

Pour les « Clients de bas niveau », autrement dit, qui prend en charge de TDS version 7.3 et ci-dessous - hello FQDN du serveur dans la chaîne de connexion hello doit être modifié :

FQDN du serveur d’origine dans la chaîne de connexion hello : <*nom du serveur*>. database.windows.net

FQDN du serveur modifié dans la chaîne de connexion hello : <*nom du serveur*> .database. **sécurisé**. windows.net

Voici une liste non exhaustive de « clients de niveau inférieur » :

* .NET 4.0 et versions antérieures
* ODBC 10.0 et versions antérieures
* JDBC (pendant JDBC prend en charge de TDS 7.4, hello fonctionnalité de redirection de TDS n’est pas entièrement pris en charge)
* Tedious (pour Node.JS)

**Remarque :** hello au-dessus de modification de nom de domaine complet de serveur peut être utile également pour appliquer une stratégie d’audit au niveau de SQL Server sans nécessité d’une configuration de l’étape dans chaque base de données (atténuation temporaire).     

