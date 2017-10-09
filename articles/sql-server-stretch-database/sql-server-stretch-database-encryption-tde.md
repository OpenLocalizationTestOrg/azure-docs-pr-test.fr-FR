---
title: "aaaEnable chiffrement Transparent des données pour Stretch Database - Azure | Documents Microsoft"
description: "Activer le chiffrement transparent des données (TDE) pour SQL Server Stretch Database sur Azure"
services: sql-server-stretch-database
documentationcenter: 
author: douglaslMS
manager: barbkess
editor: 
ms.assetid: a44ed8f5-b416-4c41-9b1e-b7271f10bdc3
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2016
ms.author: douglasl
ms.openlocfilehash: 1d6bff455030ac8851b2184c1e8097afd61361d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure"></a><span data-ttu-id="22fe4-103">Activer le chiffrement transparent des données (TDE) pour Stretch Database sur Azure</span><span class="sxs-lookup"><span data-stu-id="22fe4-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="22fe4-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="22fe4-104">Azure portal</span></span>](sql-server-stretch-database-encryption-tde.md)
> * [<span data-ttu-id="22fe4-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="22fe4-105">TSQL</span></span>](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="22fe4-106">Chiffrement transparent des données (TDE) vous aide à protéger contre les menaces hello d’activités malveillantes en effectuant le chiffrement en temps réel et le déchiffrement de la base de données de hello, les sauvegardes associées et les fichiers journaux des transactions au repos sans nécessiter de modifications toohello application.</span><span class="sxs-lookup"><span data-stu-id="22fe4-106">Transparent Data Encryption (TDE) helps protect against hello threat of malicious activity by performing real-time encryption and decryption of hello database, associated backups, and transaction log files at rest without requiring changes toohello application.</span></span>

<span data-ttu-id="22fe4-107">Stockage hello d’une base de données entière est chiffré à l’aide d’une clé de chiffrement de base de données hello appelée de clé symétrique.</span><span class="sxs-lookup"><span data-stu-id="22fe4-107">TDE encrypts hello storage of an entire database by using a symmetric key called hello database encryption key.</span></span> <span data-ttu-id="22fe4-108">clé de chiffrement de base de données Hello est protégé par un certificat de serveur intégré.</span><span class="sxs-lookup"><span data-stu-id="22fe4-108">hello database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="22fe4-109">certificat de serveur intégré Hello est unique pour chaque serveur Azure.</span><span class="sxs-lookup"><span data-stu-id="22fe4-109">hello built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="22fe4-110">Microsoft alterne automatiquement ces certificats au moins tous les 90 jours.</span><span class="sxs-lookup"><span data-stu-id="22fe4-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="22fe4-111">Pour obtenir une description générale du chiffrement transparent des données, consultez [Chiffrement transparent des données (TDE)].</span><span class="sxs-lookup"><span data-stu-id="22fe4-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="22fe4-112">Activation du chiffrement</span><span class="sxs-lookup"><span data-stu-id="22fe4-112">Enabling Encryption</span></span>
<span data-ttu-id="22fe4-113">tooenable chiffrement transparent des données pour une base de données Azure stocke hello les données migrées à partir d’une base de données SQL Server compatible Stretch, hello suivant choses :</span><span class="sxs-lookup"><span data-stu-id="22fe4-113">tooenable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="22fe4-114">Base de données ouverte hello Bonjour [portail Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="22fe4-114">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="22fe4-115">Dans le panneau de la base de données hello, cliquez sur hello **paramètres** bouton</span><span class="sxs-lookup"><span data-stu-id="22fe4-115">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="22fe4-116">Sélectionnez hello **chiffrement Transparent des données** option![][1]</span><span class="sxs-lookup"><span data-stu-id="22fe4-116">Select hello **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="22fe4-117">Sélectionnez hello **sur** définition, puis sélectionnez **enregistrer**
   ![][2]</span><span class="sxs-lookup"><span data-stu-id="22fe4-117">Select hello **On** setting, and then select **Save**
![][2]</span></span>

## <a name="disabling-encryption"></a><span data-ttu-id="22fe4-118">Désactivation du chiffrement</span><span class="sxs-lookup"><span data-stu-id="22fe4-118">Disabling Encryption</span></span>
<span data-ttu-id="22fe4-119">toodisable chiffrement transparent des données pour une base de données Azure stocke hello les données migrées à partir d’une base de données SQL Server compatible Stretch, hello suivant choses :</span><span class="sxs-lookup"><span data-stu-id="22fe4-119">toodisable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="22fe4-120">Base de données ouverte hello Bonjour [portail Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="22fe4-120">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="22fe4-121">Dans le panneau de la base de données hello, cliquez sur hello **paramètres** bouton</span><span class="sxs-lookup"><span data-stu-id="22fe4-121">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="22fe4-122">Sélectionnez hello **chiffrement Transparent des données** option</span><span class="sxs-lookup"><span data-stu-id="22fe4-122">Select hello **Transparent data encryption** option</span></span>
4. <span data-ttu-id="22fe4-123">Sélectionnez hello **hors** définition, puis sélectionnez **enregistrer**</span><span class="sxs-lookup"><span data-stu-id="22fe4-123">Select hello **Off** setting, and then select **Save**</span></span>

<!--Anchors-->
[Chiffrement transparent des données (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->
[1]: ./media/sql-server-stretch-database-encryption-tde/stretchtde1.png
[2]: ./media/sql-server-stretch-database-encryption-tde/stretchtde2.png


<!--Link references-->
