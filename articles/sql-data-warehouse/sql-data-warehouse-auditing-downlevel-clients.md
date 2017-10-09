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
# <a name="sql-data-warehouse----downlevel-clients-support-for-auditing-and-dynamic-data-masking"></a><span data-ttu-id="53766-103">SQL Data Warehouse : prise en charge des clients de niveau inférieur pour l’audit et le masquage dynamique des données (Dynamic Data Masking)</span><span class="sxs-lookup"><span data-stu-id="53766-103">SQL Data Warehouse -  Downlevel clients support for auditing and Dynamic Data Masking</span></span>
<span data-ttu-id="53766-104">[L’audit](sql-data-warehouse-auditing-overview.md) fonctionne avec les clients SQL qui prennent en charge la redirection TDS.</span><span class="sxs-lookup"><span data-stu-id="53766-104">[Auditing](sql-data-warehouse-auditing-overview.md) works with SQL clients that support TDS redirection.</span></span>

<span data-ttu-id="53766-105">Tout client qui implémente TDS 7.4 doit également prendre en charge la redirection.</span><span class="sxs-lookup"><span data-stu-id="53766-105">Any client which implements TDS 7.4 should also support redirection.</span></span> <span data-ttu-id="53766-106">Exceptions toothis incluent JDBC 4.0 quelle fonctionnalité de redirection hello n’est pas entièrement pris en charge et fastidieuses pour Node.JS dans lequel la redirection n’était pas implémentée.</span><span class="sxs-lookup"><span data-stu-id="53766-106">Exceptions toothis include JDBC 4.0 in which hello redirection feature is not fully supported and Tedious for Node.JS in which redirection was not implemented.</span></span>

<span data-ttu-id="53766-107">Pour les « Clients de bas niveau », autrement dit, qui prend en charge de TDS version 7.3 et ci-dessous - hello FQDN du serveur dans la chaîne de connexion hello doit être modifié :</span><span class="sxs-lookup"><span data-stu-id="53766-107">For "Downlevel clients", i.e. which support TDS version 7.3 and below - hello server FQDN in hello connection string should be modified:</span></span>

<span data-ttu-id="53766-108">FQDN du serveur d’origine dans la chaîne de connexion hello : <*nom du serveur*>. database.windows.net</span><span class="sxs-lookup"><span data-stu-id="53766-108">Original server FQDN in hello connection string: <*server name*>.database.windows.net</span></span>

<span data-ttu-id="53766-109">FQDN du serveur modifié dans la chaîne de connexion hello : <*nom du serveur*> .database. **sécurisé**. windows.net</span><span class="sxs-lookup"><span data-stu-id="53766-109">Modified server FQDN in hello connection string: <*server name*>.database.**secure**.windows.net</span></span>

<span data-ttu-id="53766-110">Voici une liste non exhaustive de « clients de niveau inférieur » :</span><span class="sxs-lookup"><span data-stu-id="53766-110">A partial list of "Downlevel clients" includes:</span></span>

* <span data-ttu-id="53766-111">.NET 4.0 et versions antérieures</span><span class="sxs-lookup"><span data-stu-id="53766-111">.NET 4.0 and below,</span></span>
* <span data-ttu-id="53766-112">ODBC 10.0 et versions antérieures</span><span class="sxs-lookup"><span data-stu-id="53766-112">ODBC 10.0 and below.</span></span>
* <span data-ttu-id="53766-113">JDBC (pendant JDBC prend en charge de TDS 7.4, hello fonctionnalité de redirection de TDS n’est pas entièrement pris en charge)</span><span class="sxs-lookup"><span data-stu-id="53766-113">JDBC (while JDBC does support TDS 7.4, hello TDS redirection feature is not fully supported)</span></span>
* <span data-ttu-id="53766-114">Tedious (pour Node.JS)</span><span class="sxs-lookup"><span data-stu-id="53766-114">Tedious (for Node.JS)</span></span>

<span data-ttu-id="53766-115">**Remarque :** hello au-dessus de modification de nom de domaine complet de serveur peut être utile également pour appliquer une stratégie d’audit au niveau de SQL Server sans nécessité d’une configuration de l’étape dans chaque base de données (atténuation temporaire).</span><span class="sxs-lookup"><span data-stu-id="53766-115">**Remark:** hello above server FDQN modification may be useful also for applying a SQL Server Level Auditing policy without a need for a configuration step in each database (Temporary mitigation).</span></span>     

