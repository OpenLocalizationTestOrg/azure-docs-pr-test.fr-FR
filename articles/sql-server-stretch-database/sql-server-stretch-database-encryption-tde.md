---
title: Activer Transparent Data Encryption pour Stretch Database - Azure | Microsoft Docs
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
ms.openlocfilehash: ceb355d2ba872ed5d3886c6dc82ca75b1854db0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure"></a><span data-ttu-id="f803b-103">Activer le chiffrement transparent des données (TDE) pour Stretch Database sur Azure</span><span class="sxs-lookup"><span data-stu-id="f803b-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f803b-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="f803b-104">Azure portal</span></span>](sql-server-stretch-database-encryption-tde.md)
> * [<span data-ttu-id="f803b-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="f803b-105">TSQL</span></span>](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="f803b-106">Le chiffrement transparent des données (Transparent Data Encryption, TDE) protège le système contre toute menace d’activité malveillante, en effectuant un chiffrement et un déchiffrement en temps réel de la base de données, des sauvegardes associées et des fichiers journaux de transactions au repos, sans qu’il soit nécessaire de modifier l’application.</span><span class="sxs-lookup"><span data-stu-id="f803b-106">Transparent Data Encryption (TDE) helps protect against the threat of malicious activity by performing real-time encryption and decryption of the database, associated backups, and transaction log files at rest without requiring changes to the application.</span></span>

<span data-ttu-id="f803b-107">Le chiffrement transparent des données chiffre le stockage d’une base de données entière à l’aide d’une clé symétrique appelée clé de chiffrement de base de données.</span><span class="sxs-lookup"><span data-stu-id="f803b-107">TDE encrypts the storage of an entire database by using a symmetric key called the database encryption key.</span></span> <span data-ttu-id="f803b-108">La clé de chiffrement de base de données est protégée par un certificat de serveur intégré.</span><span class="sxs-lookup"><span data-stu-id="f803b-108">The database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="f803b-109">Le certificat de serveur intégré est unique pour chaque serveur Azure.</span><span class="sxs-lookup"><span data-stu-id="f803b-109">The built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="f803b-110">Microsoft alterne automatiquement ces certificats au moins tous les 90 jours.</span><span class="sxs-lookup"><span data-stu-id="f803b-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="f803b-111">Pour obtenir une description générale du chiffrement transparent des données, consultez [Chiffrement transparent des données (TDE)].</span><span class="sxs-lookup"><span data-stu-id="f803b-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="f803b-112">Activation du chiffrement</span><span class="sxs-lookup"><span data-stu-id="f803b-112">Enabling Encryption</span></span>
<span data-ttu-id="f803b-113">Pour activer le chiffrement transparent des données pour une base de données Azure qui stocke les données migrées à partir d’une base de données SQL Server compatible avec Stretch, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f803b-113">To enable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="f803b-114">Ouvrez la base de données dans le [portail Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="f803b-114">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="f803b-115">Dans le panneau de la base de données, cliquez sur le bouton **Paramètres**</span><span class="sxs-lookup"><span data-stu-id="f803b-115">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="f803b-116">Sélectionnez l’option **Chiffrement transparent des données**![][1]</span><span class="sxs-lookup"><span data-stu-id="f803b-116">Select the **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="f803b-117">Sélectionnez le paramètre **Activé**, puis **Enregistrer**
   ![][2]</span><span class="sxs-lookup"><span data-stu-id="f803b-117">Select the **On** setting, and then select **Save**
![][2]</span></span>

## <a name="disabling-encryption"></a><span data-ttu-id="f803b-118">Désactivation du chiffrement</span><span class="sxs-lookup"><span data-stu-id="f803b-118">Disabling Encryption</span></span>
<span data-ttu-id="f803b-119">Pour désactiver le chiffrement transparent des données pour une base de données Azure qui stocke les données migrées à partir d’une base de données SQL Server compatible avec Stretch, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f803b-119">To disable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="f803b-120">Ouvrez la base de données dans le [portail Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="f803b-120">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="f803b-121">Dans le panneau de la base de données, cliquez sur le bouton **Paramètres**</span><span class="sxs-lookup"><span data-stu-id="f803b-121">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="f803b-122">Sélectionnez l’option **Chiffrement transparent des données**</span><span class="sxs-lookup"><span data-stu-id="f803b-122">Select the **Transparent data encryption** option</span></span>
4. <span data-ttu-id="f803b-123">Sélectionnez le paramètre **Désactivé**, puis **Enregistrer**</span><span class="sxs-lookup"><span data-stu-id="f803b-123">Select the **Off** setting, and then select **Save**</span></span>

<!--Anchors-->
<span data-ttu-id="f803b-124">[Chiffrement transparent des données (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx</span><span class="sxs-lookup"><span data-stu-id="f803b-124">[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx</span></span>


<!--Image references-->
[1]: ./media/sql-server-stretch-database-encryption-tde/stretchtde1.png
[2]: ./media/sql-server-stretch-database-encryption-tde/stretchtde2.png


<!--Link references-->
