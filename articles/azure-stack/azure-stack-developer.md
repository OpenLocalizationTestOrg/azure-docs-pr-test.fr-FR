---
title: applications aaaDevelop pour la pile de Azure | Documents Microsoft
description: "Découvrez les considérations relatives au développement pour le prototypage d’applications sur Azure Stack."
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: d3ebc6b1-0ffe-4d3e-ba4a-388239d6cdc3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: 9bea75d0f0ecf19c05ff55ac3ef4e778d53a1912
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-stack"></a><span data-ttu-id="00e29-103">Développer pour Azure Stack</span><span class="sxs-lookup"><span data-stu-id="00e29-103">Develop for Azure Stack</span></span>
<span data-ttu-id="00e29-104">Vous pouvez commencer à développer applications aujourd'hui, même si vous n’avez pas accès tooan Azure environnement à pile.</span><span class="sxs-lookup"><span data-stu-id="00e29-104">You can get started developing applications today, even if you don't have access tooan Azure Stack environment.</span></span> <span data-ttu-id="00e29-105">Étant donné que la pile de Azure fournit des services de Microsoft Azure qui s’exécutent dans votre centre de données, vous pouvez utiliser similaire toodevelop outils et processus par rapport à la pile de Azure comme vous le feriez avec Azure.</span><span class="sxs-lookup"><span data-stu-id="00e29-105">Because Azure Stack delivers Microsoft Azure services that run in your datacenter, you can use similar tools and processes toodevelop against Azure Stack as you would with Azure.</span></span>  <span data-ttu-id="00e29-106">Avec un peu de préparation et de recommandations de hello rubriques suivantes, vous pouvez utiliser Azure tooemulate un environnement Azure pile :</span><span class="sxs-lookup"><span data-stu-id="00e29-106">With a bit of preparation and guidance from hello following topics, you can use Azure tooemulate an Azure Stack environment:</span></span>

* <span data-ttu-id="00e29-107">Dans Azure, vous pouvez créer des modèles Azure Resource Manager tooAzure déployable pile.</span><span class="sxs-lookup"><span data-stu-id="00e29-107">In Azure, you can create Azure Resource Manager templates that are also deployable tooAzure Stack.</span></span>  <span data-ttu-id="00e29-108">Consultez [considérations relatives au modèle](azure-stack-develop-templates.md) pour obtenir des conseils sur le développement de votre portabilité tooensure de modèles.</span><span class="sxs-lookup"><span data-stu-id="00e29-108">See [template considerations](azure-stack-develop-templates.md) for guidance on developing your templates tooensure portability.</span></span>
* <span data-ttu-id="00e29-109">Il existe une différence de disponibilité de service et de gestion des versions de services entre Azure et Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="00e29-109">There is a delta in service availability and service versioning between Azure and Azure Stack.</span></span> <span data-ttu-id="00e29-110">Vous pouvez utiliser hello [module de stratégie Azure pile](azure-stack-policy-module.md) toowhat types toorestrict service Azure disponibilité et les ressources de disponible dans la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="00e29-110">You can use hello [Azure Stack policy module](azure-stack-policy-module.md) toorestrict Azure service availability and resource types toowhat's available in Azure Stack.</span></span> <span data-ttu-id="00e29-111">Restriction des services disponibles aidera à votre application de s’appuient sur les services tooAzure disponible pile.</span><span class="sxs-lookup"><span data-stu-id="00e29-111">Constraining available services will help your application rely on services available tooAzure Stack.</span></span>
* <span data-ttu-id="00e29-112">Hello [modèles de démarrage rapide Azure pile](https://github.com/Azure/AzureStack-QuickStart-Templates) sont des exemples de scénarios courants de façon toodevelop vos modèles de sorte qu’ils peuvent être déploiement tooboth Azure et la pile d’Azure.</span><span class="sxs-lookup"><span data-stu-id="00e29-112">hello [Azure Stack Quickstart Templates](https://github.com/Azure/AzureStack-QuickStart-Templates) are common scenario examples of how toodevelop your templates so they can be deployed tooboth Azure and Azure Stack.</span></span>


