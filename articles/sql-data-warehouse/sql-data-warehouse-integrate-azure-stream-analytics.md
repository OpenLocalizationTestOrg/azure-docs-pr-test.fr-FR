---
title: "aaaUse Analytique de flux de données Azure SQL Data Warehouse | Documents Microsoft"
description: "Conseils sur l’utilisation d’Azure Stream Analytics avec Azure SQL Data Warehouse pour le développement de solutions."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 8aeb2247-20c5-4a29-b327-30a8ce09dfdc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 1278197a6764864124fd92fc672de00b83ec343f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-with-sql-data-warehouse"></a><span data-ttu-id="5b70e-103">Utiliser Azure Stream Analytics avec SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="5b70e-103">Use Azure Stream Analytics with SQL Data Warehouse</span></span>
<span data-ttu-id="5b70e-104">Analytique de flux de données Azure est un service entièrement géré qui fournit le traitement des événements complexes de faible latence, hautement disponible et évolutif sur la diffusion en continu des données dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="5b70e-104">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable complex event processing over streaming data in hello cloud.</span></span> <span data-ttu-id="5b70e-105">Vous pouvez principes hello en lisant [tooAzure de présentation des flux de données Analytique][Introduction tooAzure Stream Analytics].</span><span class="sxs-lookup"><span data-stu-id="5b70e-105">You can learn hello basics by reading [Introduction tooAzure Stream Analytics][Introduction tooAzure Stream Analytics].</span></span> <span data-ttu-id="5b70e-106">Vous pouvez ensuite apprendre comment toocreate une solution de bout en bout avec flux de données Analytique en suivant hello [prise en main Azure flux Analytique] [ Get started using Azure Stream Analytics] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="5b70e-106">You can then learn how toocreate an end-to-end solution with Stream Analytics by following hello [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>

<span data-ttu-id="5b70e-107">Dans cet article, vous allez apprendre comment toouse votre entrepôt de données SQL Azure de base de données en tant que récepteur de sortie pour vos tâches de flux Analytique.</span><span class="sxs-lookup"><span data-stu-id="5b70e-107">In this article, you will learn how toouse your Azure SQL Data Warehouse database as an output sink for your Steam Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b70e-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5b70e-108">Prerequisites</span></span>
<span data-ttu-id="5b70e-109">Commencez par exécuter via hello comme suit dans hello [prise en main Azure flux Analytique] [ Get started using Azure Stream Analytics] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="5b70e-109">First, run through hello following steps in hello [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>  

1. <span data-ttu-id="5b70e-110">Création d’une entrée de hub d’événements</span><span class="sxs-lookup"><span data-stu-id="5b70e-110">Create an Event Hub input</span></span>
2. <span data-ttu-id="5b70e-111">Configuration et démarrage de l’application de génération d’événements</span><span class="sxs-lookup"><span data-stu-id="5b70e-111">Configure and start event generator application</span></span>
3. <span data-ttu-id="5b70e-112">Configuration d’un travail Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5b70e-112">Provision a Stream Analytics job</span></span>
4. <span data-ttu-id="5b70e-113">Spécification d’une entrée de travail et d’une requête</span><span class="sxs-lookup"><span data-stu-id="5b70e-113">Specify job input and query</span></span>

<span data-ttu-id="5b70e-114">Ensuite, créez une base de données SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="5b70e-114">Then, create an Azure SQL Data Warehouse database</span></span>

## <a name="specify-job-output-azure-sql-data-warehouse-database"></a><span data-ttu-id="5b70e-115">Spécifier la sortie du travail : base de données Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="5b70e-115">Specify job output: Azure SQL Data Warehouse database</span></span>
### <a name="step-1"></a><span data-ttu-id="5b70e-116">Étape 1</span><span class="sxs-lookup"><span data-stu-id="5b70e-116">Step 1</span></span>
<span data-ttu-id="5b70e-117">Dans votre tâche de flux de données Analytique, cliquez sur **sortie** de haut hello de hello page, puis cliquez sur **ajouter une sortie**.</span><span class="sxs-lookup"><span data-stu-id="5b70e-117">In your Stream Analytics job click **OUTPUT** from hello top of hello page, and then click **ADD OUTPUT**.</span></span>

### <a name="step-2"></a><span data-ttu-id="5b70e-118">Étape 2</span><span class="sxs-lookup"><span data-stu-id="5b70e-118">Step 2</span></span>
<span data-ttu-id="5b70e-119">Sélectionnez Base de données SQL, puis cliquez sur suivant.</span><span class="sxs-lookup"><span data-stu-id="5b70e-119">Select SQL Database and click next.</span></span>

![][add-output]

### <a name="step-3"></a><span data-ttu-id="5b70e-120">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="5b70e-120">Step 3</span></span>
<span data-ttu-id="5b70e-121">Entrez hello valeurs suivantes sur la page suivante de hello :</span><span class="sxs-lookup"><span data-stu-id="5b70e-121">Enter hello following values on hello next page:</span></span>

* <span data-ttu-id="5b70e-122">*Alias de sortie*: entrez un nom convivial pour cette sortie de travail.</span><span class="sxs-lookup"><span data-stu-id="5b70e-122">*Output Alias*: Enter a friendly name for this job output.</span></span>
* <span data-ttu-id="5b70e-123">*Abonnement*:</span><span class="sxs-lookup"><span data-stu-id="5b70e-123">*Subscription*:</span></span>
  * <span data-ttu-id="5b70e-124">Si votre base de données SQL Data Warehouse Bonjour même abonnement en tant que tâche de flux de données Analytique hello, sélectionnez de base de données SQL d’utilisation de l’abonnement actuel.</span><span class="sxs-lookup"><span data-stu-id="5b70e-124">If your SQL Data Warehouse database is in hello same subscription as hello Stream Analytics job, select Use SQL Database from Current Subscription.</span></span>
  * <span data-ttu-id="5b70e-125">Si votre base de données se trouve dans un autre abonnement, sélectionnez Utiliser la base de données SQL d’un autre abonnement.</span><span class="sxs-lookup"><span data-stu-id="5b70e-125">If your database is in a different subscription, select Use SQL Database from Another Subscription.</span></span>
* <span data-ttu-id="5b70e-126">*Base de données*: spécifiez le nom hello d’une base de données de destination.</span><span class="sxs-lookup"><span data-stu-id="5b70e-126">*Database*: Specify hello name of a destination database.</span></span>
* <span data-ttu-id="5b70e-127">*Nom du serveur*: spécifiez le nom du serveur de base de données hello vous venez de spécifier hello.</span><span class="sxs-lookup"><span data-stu-id="5b70e-127">*Server Name*: Specify hello server name for hello database you just specified.</span></span> <span data-ttu-id="5b70e-128">Vous pouvez utiliser cette toofind du portail classique Azure hello.</span><span class="sxs-lookup"><span data-stu-id="5b70e-128">You can use hello Azure Classic Portal toofind this.</span></span>

![][server-name]

* <span data-ttu-id="5b70e-129">*Nom d’utilisateur*: spécifiez le nom d’utilisateur hello d’un compte qui dispose des autorisations d’écriture pour la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="5b70e-129">*User Name*: Specify hello user name of an account that has write permissions for hello database.</span></span>
* <span data-ttu-id="5b70e-130">*Mot de passe*: fournir un mot de passe hello pour hello de compte d’utilisateur spécifié.</span><span class="sxs-lookup"><span data-stu-id="5b70e-130">*Password*: Provide hello password for hello specified user account.</span></span>
* <span data-ttu-id="5b70e-131">*Table*: spécifier le nom hello de la table cible hello dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="5b70e-131">*Table*: Specify hello name of hello target table in hello database.</span></span>

![][add-database]

### <a name="step-4"></a><span data-ttu-id="5b70e-132">Étape 4</span><span class="sxs-lookup"><span data-stu-id="5b70e-132">Step 4</span></span>
<span data-ttu-id="5b70e-133">Cliquez sur tooadd de bouton de vérification hello cette tooverify qu’Analytique de flux de connexion de base de données toohello et sortie des tâches.</span><span class="sxs-lookup"><span data-stu-id="5b70e-133">Click hello check button tooadd this job output and tooverify that Stream Analytics can successfully connect toohello database.</span></span>

![][test-connection]

<span data-ttu-id="5b70e-134">Lors de la base de données toohello hello connexion réussit, vous voyez une notification bas hello du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="5b70e-134">When hello connection toohello database succeeds, you will see a notification at hello bottom of hello portal.</span></span> <span data-ttu-id="5b70e-135">Vous pouvez cliquer sur Tester la connexion à base de données hello bas tootest hello connexion toohello.</span><span class="sxs-lookup"><span data-stu-id="5b70e-135">You can click Test Connection at hello bottom tootest hello connection toohello database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b70e-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5b70e-136">Next steps</span></span>
<span data-ttu-id="5b70e-137">Pour une vue d’ensemble de l’intégration, consultez [Vue d’ensemble sur l’intégration de SQL Data Warehouse][SQL Data Warehouse integration overview].</span><span class="sxs-lookup"><span data-stu-id="5b70e-137">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span></span>

<span data-ttu-id="5b70e-138">Pour obtenir des conseils supplémentaires en matière de développement, consultez l’article [Vue d’ensemble sur le développement SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="5b70e-138">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

[add-output]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-output.png
[server-name]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/dw-server-name.png
[add-database]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-database.png
[test-connection]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/test-connection.png

<!--Article references-->

[Introduction tooAzure Stream Analytics]: ../stream-analytics/stream-analytics-introduction.md
[Get started using Azure Stream Analytics]: ../stream-analytics/stream-analytics-real-time-fraud-detection.md
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Stream Analytics documentation]: http://azure.microsoft.com/documentation/services/stream-analytics/
