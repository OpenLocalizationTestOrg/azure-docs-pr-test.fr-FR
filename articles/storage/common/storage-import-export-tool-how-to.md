---
title: "Utilisation de l’outil Azure Import/Export | Microsoft Docs"
description: "Découvrez comment utiliser l’outil d’importation/exportation pour préparer les disques durs pour un travail d’importation, réparer un travail d’importation ou un travail d’exportation."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: f77535bb-d577-438a-bdd3-e15a82e0c543
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 20a720833842f9579fd4fccaa39e964def48197e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="using-the-azure-importexport-tool"></a><span data-ttu-id="5ad45-103">Utilisation de l’outil Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="5ad45-103">Using the Azure Import/Export Tool</span></span> 

<span data-ttu-id="5ad45-104">L’outil Azure Import/Export (WAImportExport.exe) sert à créer et gérer des travaux pour le service Azure Import/Export, ce qui vous permet de transférer de grandes quantités de données vers ou à partir du Stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="5ad45-104">The Azure Import/Export Tool (WAImportExport.exe) is used to create and manage jobs for the Azure Import/Export service, enabling you to transfer large amounts of data into or out of Azure Blob Storage.</span></span>

<span data-ttu-id="5ad45-105">Cette documentation s’applique à la version la plus récente de l’outil Azure Import/Export.</span><span class="sxs-lookup"><span data-stu-id="5ad45-105">This documentation is for the most recent version of the Azure Import/Export Tool.</span></span> <span data-ttu-id="5ad45-106">Pour plus d’informations sur l’utilisation du modèle de déploiement classique, consultez [Utilisation de l’outil Azure Import/Export v1](storage-import-export-tool-how-to-v1.md).</span><span class="sxs-lookup"><span data-stu-id="5ad45-106">For information about using the classic deployment model, see [Using the Azure Import/Export Tool v1](storage-import-export-tool-how-to-v1.md).</span></span>

<span data-ttu-id="5ad45-107">Les articles suivants vous montrent comment :</span><span class="sxs-lookup"><span data-stu-id="5ad45-107">The following articles show you how to:</span></span>  

- <span data-ttu-id="5ad45-108">Installer et configurer l’outil Azure Import/Export.</span><span class="sxs-lookup"><span data-stu-id="5ad45-108">Install and set up the Azure Import/Export Tool.</span></span>
- <span data-ttu-id="5ad45-109">Préparer vos disques durs pour un travail dans lequel vous importez des données à partir de vos disques vers le Stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="5ad45-109">Prepare your hard drives for a job where you import data from your drives to Azure Blob Storage.</span></span>
- <span data-ttu-id="5ad45-110">Vérifier l’état d’un travail avec les fichiers journaux de copie.</span><span class="sxs-lookup"><span data-stu-id="5ad45-110">Review the status of a job with Copy Log Files.</span></span> 
- <span data-ttu-id="5ad45-111">Réparer un travail d’importation.</span><span class="sxs-lookup"><span data-stu-id="5ad45-111">Repair an import job.</span></span> 
- <span data-ttu-id="5ad45-112">Réparer un travail d’exportation.</span><span class="sxs-lookup"><span data-stu-id="5ad45-112">Repair an export job.</span></span> 
- <span data-ttu-id="5ad45-113">Résoudre les problèmes liés à l’outil Azure Import/Export.</span><span class="sxs-lookup"><span data-stu-id="5ad45-113">Troubleshoot the Azure Import/Export Tool.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5ad45-114">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5ad45-114">Next steps</span></span>

* [<span data-ttu-id="5ad45-115">Configuration de l’outil WAImportExport</span><span class="sxs-lookup"><span data-stu-id="5ad45-115">Setting up the WAImportExport tool</span></span>](storage-import-export-tool-setup.md)