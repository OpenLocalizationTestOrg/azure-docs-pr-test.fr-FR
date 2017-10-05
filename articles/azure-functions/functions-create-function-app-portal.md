---
title: "Créer une Function App à l’aide du Portail Azure | Microsoft Docs"
description: "Créez une Function App dans Azure App Service à l’aide du portail."
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
ms.openlocfilehash: 85a88c537415cd6f2b6bc005cc18e3baaa29e9a4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-app-from-the-azure-portal"></a><span data-ttu-id="0aefa-103">Créer une Function App à l’aide du Portail Azure</span><span class="sxs-lookup"><span data-stu-id="0aefa-103">Create a function app from the Azure portal</span></span>

<span data-ttu-id="0aefa-104">Azure Function App utilise l’infrastructure Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="0aefa-104">Azure Function Apps uses the Azure App Service infrastructure.</span></span> <span data-ttu-id="0aefa-105">Cette rubrique vous montre comment créer une Function App dans le Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0aefa-105">This topic shows you how to create a function app in the Azure portal.</span></span> <span data-ttu-id="0aefa-106">Une Function App est un conteneur qui héberge l’exécution de fonctions individuelles.</span><span class="sxs-lookup"><span data-stu-id="0aefa-106">A function app is the container that hosts the execution of individual functions.</span></span> <span data-ttu-id="0aefa-107">Lorsque vous créez une Function App dans le plan d’hébergement App Service, elle peut utiliser toutes les fonctionnalités d’App Service.</span><span class="sxs-lookup"><span data-stu-id="0aefa-107">When you create a function app in the App Service hosting plan, your function app can use all the features of App Service.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="0aefa-108">Créer une Function App</span><span class="sxs-lookup"><span data-stu-id="0aefa-108">Create a function app</span></span>

[!INCLUDE [functions-create-function-app-portal](../../includes/functions-create-function-app-portal.md)]

<span data-ttu-id="0aefa-109">Lorsque vous créez une Function App, vous devez entrer un **nom d’application** valide, qui peut seulement contenir des lettres, des chiffres et des traits d’union.</span><span class="sxs-lookup"><span data-stu-id="0aefa-109">When you create a function app, supply a valid **App name**, which can contain only letters, numbers, and hyphens.</span></span> <span data-ttu-id="0aefa-110">Le trait de soulignement (**_**) n’est pas un caractère autorisé.</span><span class="sxs-lookup"><span data-stu-id="0aefa-110">Underscore (**_**) is not an allowed character.</span></span>

<span data-ttu-id="0aefa-111">Les noms des comptes de stockage doivent comporter entre 3 et 24 caractères, uniquement des lettres minuscules et des chiffres.</span><span class="sxs-lookup"><span data-stu-id="0aefa-111">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span> <span data-ttu-id="0aefa-112">Le nom de votre compte de stockage doit être unique dans Azure.</span><span class="sxs-lookup"><span data-stu-id="0aefa-112">Your storage account name must be unique within Azure.</span></span> 

<span data-ttu-id="0aefa-113">Une fois la Function App créée, vous pouvez créer des fonctions individuelles à l’aide d’un ou plusieurs langages</span><span class="sxs-lookup"><span data-stu-id="0aefa-113">After the function app is created, you can create individual functions in one or more different languages.</span></span> <span data-ttu-id="0aefa-114">[en utilisant le portail](functions-create-first-azure-function.md#create-function), le [déploiement continu](functions-continuous-deployment.md) ou le [téléchargement par FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).</span><span class="sxs-lookup"><span data-stu-id="0aefa-114">Create functions [by using the portal](functions-create-first-azure-function.md#create-function), [continuous deployment](functions-continuous-deployment.md), or by [uploading with FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).</span></span>

## <a name="service-plans"></a><span data-ttu-id="0aefa-115">Plans de service</span><span class="sxs-lookup"><span data-stu-id="0aefa-115">Service plans</span></span>

<span data-ttu-id="0aefa-116">Azure Functions contient deux plans de service différents : le plan de consommation et le plan App Service.</span><span class="sxs-lookup"><span data-stu-id="0aefa-116">Azure Functions has two different service plans: Consumption plan and App Service plan.</span></span> <span data-ttu-id="0aefa-117">Le plan de consommation alloue automatiquement la puissance de calcul lors de l’exécution du code, augmente la taille des instances quand c’est nécessaire pour gérer la charge, puis diminue leur taille lorsque le code n’est pas en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="0aefa-117">The Consumption plan automatically allocates compute power when your code is running, scales-out as necessary to handle load, and then scales-in when code is not running.</span></span> <span data-ttu-id="0aefa-118">Le plan App Service donne à votre Function App l’accès à toutes les fonctions d’App Service.</span><span class="sxs-lookup"><span data-stu-id="0aefa-118">The App Service plan gives your function app access to all the facilities of App Service.</span></span> <span data-ttu-id="0aefa-119">Vous devez choisir votre plan de service lors de la création de votre Function App. Il ne peut pas être modifié actuellement.</span><span class="sxs-lookup"><span data-stu-id="0aefa-119">You must choose your service plan when your function app is created, and it cannot currently be changed.</span></span> <span data-ttu-id="0aefa-120">Pour plus d’informations, consultez [Choisir un plan d’hébergement Azure Functions](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="0aefa-120">For more information, see [Choose an Azure Functions hosting plan](functions-scale.md).</span></span>

<span data-ttu-id="0aefa-121">Si vous prévoyez d’exécuter des fonctions JavaScript sur un plan App Service, vous devez choisir un plan avec moins de cœurs.</span><span class="sxs-lookup"><span data-stu-id="0aefa-121">If you are planning to run JavaScript functions on an App Service plan, you should choose a plan with fewer cores.</span></span> <span data-ttu-id="0aefa-122">Pour plus d’informations, consultez les [informations de référence sur JavaScript pour Functions](functions-reference-node.md#choose-single-core-app-service-plans).</span><span class="sxs-lookup"><span data-stu-id="0aefa-122">For more information, see the [JavaScript reference for Functions](functions-reference-node.md#choose-single-core-app-service-plans).</span></span>

<a name="storage-account-requirements"></a>

## <a name="storage-account-requirements"></a><span data-ttu-id="0aefa-123">Conditions requises pour le compte de stockage</span><span class="sxs-lookup"><span data-stu-id="0aefa-123">Storage account requirements</span></span>

<span data-ttu-id="0aefa-124">Lorsque vous créez une Function App dans App Service, vous devez créer ou établir avec une liaison avec un compte de stockage Azure à usage général qui prend en charge le Stockage Blob, File d’attente et Table.</span><span class="sxs-lookup"><span data-stu-id="0aefa-124">When creating a function app in App Service, you must create or link to a general-purpose Azure Storage account that supports Blob, Queue, and Table storage.</span></span> <span data-ttu-id="0aefa-125">En interne, Azure Functions utilise le stockage pour les opérations telles que la gestion des déclencheurs et la journalisation des exécutions de fonctions.</span><span class="sxs-lookup"><span data-stu-id="0aefa-125">Internally, Functions uses Storage for operations such as managing triggers and logging function executions.</span></span> <span data-ttu-id="0aefa-126">Certains comptes de stockage ne prennent pas en charge les files d’attente et les tables, comme les comptes de stockage Blob uniquement, le stockage Premium Azure et les comptes de stockage à usage général avec la réplication ZRS.</span><span class="sxs-lookup"><span data-stu-id="0aefa-126">Some storage accounts do not support queues and tables, such as blob-only storage accounts, Azure Premium Storage, and general-purpose storage accounts with ZRS replication.</span></span> <span data-ttu-id="0aefa-127">Ces comptes sont filtrés à partir du panneau du compte de stockage lors de la création d’une Function App.</span><span class="sxs-lookup"><span data-stu-id="0aefa-127">These accounts are filtered out of from the Storage Account blade when creating a function app.</span></span>

>[!NOTE]
><span data-ttu-id="0aefa-128">Lorsque vous utilisez le plan d’hébergement de la consommation, les fichiers de code de fonction et de configuration de liaison sont stockés sur le Stockage Fichier Azure dans le compte de stockage principal.</span><span class="sxs-lookup"><span data-stu-id="0aefa-128">When using the Consumption hosting plan, your function code and binding configuration files are stored in Azure File storage in the main storage account.</span></span> <span data-ttu-id="0aefa-129">Lorsque vous supprimez le compte de stockage principal, ce contenu est supprimé et ne peut pas être récupéré.</span><span class="sxs-lookup"><span data-stu-id="0aefa-129">When you delete the main storage account, this content is deleted and cannot be recovered.</span></span>

<span data-ttu-id="0aefa-130">Pour en savoir plus sur les types de compte de stockage, consultez [Présentation des services Stockage Azure](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).</span><span class="sxs-lookup"><span data-stu-id="0aefa-130">To learn more about storage account types, see [Introducing the Azure Storage Services](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0aefa-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0aefa-131">Next steps</span></span>

[!INCLUDE [Functions quickstart next steps](../../includes/functions-quickstart-next-steps.md)]



