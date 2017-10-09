---
title: aaaCreate une application de la fonction de hello portail Azure | Documents Microsoft
description: "Créer une nouvelle application de fonction dans Azure App Service à partir du portail de hello."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/11/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: c531fc71c798edf22e25a5f4b79c15413809dc86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-from-hello-azure-portal"></a><span data-ttu-id="062e5-103">Créer une application de la fonction à partir de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="062e5-103">Create a function app from hello Azure portal</span></span>

<span data-ttu-id="062e5-104">Les applications Azure (fonction) utilise l’infrastructure de Service d’applications Azure hello.</span><span class="sxs-lookup"><span data-stu-id="062e5-104">Azure Function Apps uses hello Azure App Service infrastructure.</span></span> <span data-ttu-id="062e5-105">Cette rubrique vous montre comment toocreate une application de la fonction Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="062e5-105">This topic shows you how toocreate a function app in hello Azure portal.</span></span> <span data-ttu-id="062e5-106">Une application de la fonction est un conteneur hello qui héberge l’exécution de hello des fonctions individuelles.</span><span class="sxs-lookup"><span data-stu-id="062e5-106">A function app is hello container that hosts hello execution of individual functions.</span></span> <span data-ttu-id="062e5-107">Lorsque vous créez une application de la fonction Bonjour plan d’hébergement du Service d’applications, votre application de la fonction peut utiliser toutes les fonctionnalités de hello du Service d’application.</span><span class="sxs-lookup"><span data-stu-id="062e5-107">When you create a function app in hello App Service hosting plan, your function app can use all hello features of App Service.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="062e5-108">Créer une Function App</span><span class="sxs-lookup"><span data-stu-id="062e5-108">Create a function app</span></span>

[!INCLUDE [functions-create-function-app-portal](../../includes/functions-create-function-app-portal.md)]

<span data-ttu-id="062e5-109">Lorsque vous créez une Function App, vous devez entrer un **nom d’application** valide, qui peut seulement contenir des lettres, des chiffres et des traits d’union.</span><span class="sxs-lookup"><span data-stu-id="062e5-109">When you create a function app, supply a valid **App name**, which can contain only letters, numbers, and hyphens.</span></span> <span data-ttu-id="062e5-110">Le trait de soulignement (**_**) n’est pas un caractère autorisé.</span><span class="sxs-lookup"><span data-stu-id="062e5-110">Underscore (**_**) is not an allowed character.</span></span>

<span data-ttu-id="062e5-111">Les noms des comptes de stockage doivent comporter entre 3 et 24 caractères, uniquement des lettres minuscules et des chiffres.</span><span class="sxs-lookup"><span data-stu-id="062e5-111">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span> <span data-ttu-id="062e5-112">Le nom de votre compte de stockage doit être unique dans Azure.</span><span class="sxs-lookup"><span data-stu-id="062e5-112">Your storage account name must be unique within Azure.</span></span> 

<span data-ttu-id="062e5-113">Après que application de fonction hello est créée, vous pouvez créer des fonctions individuelles dans une ou plusieurs langues différentes.</span><span class="sxs-lookup"><span data-stu-id="062e5-113">After hello function app is created, you can create individual functions in one or more different languages.</span></span> <span data-ttu-id="062e5-114">Créer des fonctions [à l’aide du portail de hello](functions-create-first-azure-function.md#create-function), [déploiement continu](functions-continuous-deployment.md), ou par [télécharger avec FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).</span><span class="sxs-lookup"><span data-stu-id="062e5-114">Create functions [by using hello portal](functions-create-first-azure-function.md#create-function), [continuous deployment](functions-continuous-deployment.md), or by [uploading with FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).</span></span>

## <a name="service-plans"></a><span data-ttu-id="062e5-115">Plans de service</span><span class="sxs-lookup"><span data-stu-id="062e5-115">Service plans</span></span>

<span data-ttu-id="062e5-116">Azure Functions contient deux plans de service différents : le plan de consommation et le plan App Service.</span><span class="sxs-lookup"><span data-stu-id="062e5-116">Azure Functions has two different service plans: Consumption plan and App Service plan.</span></span> <span data-ttu-id="062e5-117">plan de la consommation Hello alloue automatiquement la puissance de calcul lorsque votre code s’exécute, échelles montée en tant que charge de toohandle nécessaires, puis, dans l’échelle lorsque le code n’est pas en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="062e5-117">hello Consumption plan automatically allocates compute power when your code is running, scales-out as necessary toohandle load, and then scales-in when code is not running.</span></span> <span data-ttu-id="062e5-118">Hello plan App Service permet à votre fonction application tooall hello les lieux de Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="062e5-118">hello App Service plan gives your function app access tooall hello facilities of App Service.</span></span> <span data-ttu-id="062e5-119">Vous devez choisir votre plan de service lors de la création de votre Function App. Il ne peut pas être modifié actuellement.</span><span class="sxs-lookup"><span data-stu-id="062e5-119">You must choose your service plan when your function app is created, and it cannot currently be changed.</span></span> <span data-ttu-id="062e5-120">Pour plus d’informations, consultez [Choisir un plan d’hébergement Azure Functions](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="062e5-120">For more information, see [Choose an Azure Functions hosting plan](functions-scale.md).</span></span>

<span data-ttu-id="062e5-121">Si vous prévoyez toorun les fonctions JavaScript sur un plan App Service, vous devez choisir un plan avec moins de cœurs.</span><span class="sxs-lookup"><span data-stu-id="062e5-121">If you are planning toorun JavaScript functions on an App Service plan, you should choose a plan with fewer cores.</span></span> <span data-ttu-id="062e5-122">Pour plus d’informations, consultez hello [référence JavaScript pour les fonctions](functions-reference-node.md#choose-single-core-app-service-plans).</span><span class="sxs-lookup"><span data-stu-id="062e5-122">For more information, see hello [JavaScript reference for Functions](functions-reference-node.md#choose-single-core-app-service-plans).</span></span>

<a name="storage-account-requirements"></a>

## <a name="storage-account-requirements"></a><span data-ttu-id="062e5-123">Conditions requises pour le compte de stockage</span><span class="sxs-lookup"><span data-stu-id="062e5-123">Storage account requirements</span></span>

<span data-ttu-id="062e5-124">Lorsque vous créez une application de la fonction dans le Service d’applications, vous devez créer ou lier tooa à usage général compte de stockage Azure qui prend en charge le stockage Blob, file d’attente et Table.</span><span class="sxs-lookup"><span data-stu-id="062e5-124">When creating a function app in App Service, you must create or link tooa general-purpose Azure Storage account that supports Blob, Queue, and Table storage.</span></span> <span data-ttu-id="062e5-125">En interne, Azure Functions utilise le stockage pour les opérations telles que la gestion des déclencheurs et la journalisation des exécutions de fonctions.</span><span class="sxs-lookup"><span data-stu-id="062e5-125">Internally, Functions uses Storage for operations such as managing triggers and logging function executions.</span></span> <span data-ttu-id="062e5-126">Certains comptes de stockage ne prennent pas en charge les files d’attente et les tables, comme les comptes de stockage Blob uniquement, le stockage Premium Azure et les comptes de stockage à usage général avec la réplication ZRS.</span><span class="sxs-lookup"><span data-stu-id="062e5-126">Some storage accounts do not support queues and tables, such as blob-only storage accounts, Azure Premium Storage, and general-purpose storage accounts with ZRS replication.</span></span> <span data-ttu-id="062e5-127">Ces comptes sont exclus du panneau du compte de stockage hello lors de la création d’une application de la fonction.</span><span class="sxs-lookup"><span data-stu-id="062e5-127">These accounts are filtered out of from hello Storage Account blade when creating a function app.</span></span>

>[!NOTE]
><span data-ttu-id="062e5-128">Lorsque vous utilisez un plan d’hébergement hello consommation, vos fichiers de configuration de liaison et le code de fonction sont stockés dans le stockage de fichiers Azure hello principal compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="062e5-128">When using hello Consumption hosting plan, your function code and binding configuration files are stored in Azure File storage in hello main storage account.</span></span> <span data-ttu-id="062e5-129">Lorsque vous supprimez le compte de stockage principal hello, ce contenu est supprimé et ne peut pas être récupéré.</span><span class="sxs-lookup"><span data-stu-id="062e5-129">When you delete hello main storage account, this content is deleted and cannot be recovered.</span></span>

<span data-ttu-id="062e5-130">toolearn savoir plus sur les types de compte de stockage, consultez [présentation des Services de stockage Azure hello](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).</span><span class="sxs-lookup"><span data-stu-id="062e5-130">toolearn more about storage account types, see [Introducing hello Azure Storage Services](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="062e5-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="062e5-131">Next steps</span></span>

[!INCLUDE [Functions quickstart next steps](../../includes/functions-quickstart-next-steps.md)]



