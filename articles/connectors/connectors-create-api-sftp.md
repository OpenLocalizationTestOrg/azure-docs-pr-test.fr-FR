---
title: "Découvrez comment utiliser le connecteur SFTP dans vos applications logiques | Microsoft Docs"
description: "Créez des applications logiques avec Azure App Service. Connectez-vous à l’API SFTP pour envoyer et recevoir des fichiers. Vous pouvez effectuer diverses opérations, telles que créer, mettre à jour, obtenir ou supprimer des fichiers."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 697eb8b0-4a66-40c7-be7b-6aa6b131c7ad
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/20/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 31253d8daee1581167a96a20ba8ad529a04b3e92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-sftp-connector"></a><span data-ttu-id="19e20-105">Prise en main du connecteur SFTP</span><span class="sxs-lookup"><span data-stu-id="19e20-105">Get started with the SFTP connector</span></span>
<span data-ttu-id="19e20-106">Utilisez le connecteur SFTP pour accéder à un compte SFTP afin d’envoyer et de recevoir des fichiers.</span><span class="sxs-lookup"><span data-stu-id="19e20-106">Use the SFTP connector to access an SFTP account to send and receive files.</span></span> <span data-ttu-id="19e20-107">Vous pouvez effectuer diverses opérations, telles que créer, mettre à jour, obtenir ou supprimer des fichiers.</span><span class="sxs-lookup"><span data-stu-id="19e20-107">You can perform various operations such as create, update, get or delete files.</span></span>  

<span data-ttu-id="19e20-108">Pour utiliser [n’importe quel connecteur](apis-list.md), vous devez commencer par créer une application logique.</span><span class="sxs-lookup"><span data-stu-id="19e20-108">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="19e20-109">Vous pouvez démarrer maintenant en [créant une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="19e20-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-sftp"></a><span data-ttu-id="19e20-110">Se connecter à SFTP</span><span class="sxs-lookup"><span data-stu-id="19e20-110">Connect to SFTP</span></span>
<span data-ttu-id="19e20-111">Pour que votre application logique puisse accéder à un service, vous devez commencer par créer une *connexion* à celui-ci.</span><span class="sxs-lookup"><span data-stu-id="19e20-111">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="19e20-112">Une [connexion](connectors-overview.md) permet d’assurer la connectivité entre une application logique et un autre service.</span><span class="sxs-lookup"><span data-stu-id="19e20-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-sftp"></a><span data-ttu-id="19e20-113">Créer une connexion à SFTP</span><span class="sxs-lookup"><span data-stu-id="19e20-113">Create a connection to SFTP</span></span>
> [!INCLUDE [Steps to create a connection to SFTP](../../includes/connectors-create-api-sftp.md)]
> 
> 

## <a name="use-an-sftp-trigger"></a><span data-ttu-id="19e20-114">Utiliser un déclencheur SFTP</span><span class="sxs-lookup"><span data-stu-id="19e20-114">Use an SFTP trigger</span></span>
<span data-ttu-id="19e20-115">Un déclencheur est un événement qui peut être utilisé pour lancer le flux de travail défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="19e20-115">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="19e20-116">[En savoir plus sur les déclencheurs](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="19e20-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="19e20-117">Dans cet exemple,nous utilisons le déclencheur **SFTP - Lors de l’ajout ou de la modification d’un fichier**, un déclencheur est utilisé pour initialiser un flux de travail d’application logique lorsqu’un fichier est ajouté à un serveur SFTP ou modifié sur ce dernier.</span><span class="sxs-lookup"><span data-stu-id="19e20-117">In this example, the **SFTP - When a file is added or modified** trigger is used to initiate a logic app workflow when a file is added to, or modified on, an SFTP server.</span></span> <span data-ttu-id="19e20-118">Vous ajoutez une condition qui vérifie le contenu du fichier nouveau ou modifié, puis prend une décision pour extraire le fichier si son contenu indique qu’il doit être extrait avant d’être utilisé.</span><span class="sxs-lookup"><span data-stu-id="19e20-118">You also add a condition that checks the contents of the new or modified file, and makes a decision to extract the file if its contents indicate that it should be extracted before using the contents.</span></span> <span data-ttu-id="19e20-119">Enfin, ajoutez une action pour extraire le contenu d’un fichier et placer le contenu extrait dans un dossier du serveur SFTP.</span><span class="sxs-lookup"><span data-stu-id="19e20-119">Finally, add an action to extract the contents of a file, and place the extracted contents in a folder on the SFTP server.</span></span> 

<span data-ttu-id="19e20-120">Dans un contexte d’entreprise, vous pourriez utiliser ce déclencheur pour surveiller l’apparition dans un dossier SFTP de nouveaux fichiers représentant les commandes des clients.</span><span class="sxs-lookup"><span data-stu-id="19e20-120">In an enterprise example, you could use this trigger to monitor an SFTP folder for new files that represent customer orders.</span></span>  <span data-ttu-id="19e20-121">Vous pourriez ensuite utiliser une action de connecteur SFTP telle que **Obtenir le contenu d’un fichier** pour récupérer le contenu de la commande à des fins de traitement ultérieur et de stockage dans une base de données de commandes.</span><span class="sxs-lookup"><span data-stu-id="19e20-121">You could then use an SFTP connector action, such as **Get file content**, to get the contents of the order for further processing and storage in an orders database.</span></span>

> [!INCLUDE [Steps to create an SFTP trigger](../../includes/connectors-create-api-sftp-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="19e20-122">Ajouter une condition</span><span class="sxs-lookup"><span data-stu-id="19e20-122">Add a condition</span></span>
> [!INCLUDE [Steps to add a condition](../../includes/connectors-create-api-sftp-condition.md)]
> 
> 

## <a name="use-an-sftp-action"></a><span data-ttu-id="19e20-123">Utiliser une action SFTP</span><span class="sxs-lookup"><span data-stu-id="19e20-123">Use an SFTP action</span></span>
<span data-ttu-id="19e20-124">Une action est une opération effectuée par le flux de travail défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="19e20-124">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="19e20-125">[En savoir plus sur les actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="19e20-125">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps to create an SFTP action](../../includes/connectors-create-api-sftp-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="19e20-126">Détails spécifiques aux connecteurs</span><span class="sxs-lookup"><span data-stu-id="19e20-126">Connector-specific details</span></span>

<span data-ttu-id="19e20-127">Consultez tous les déclencheurs et les actions définies dans le swagger, ainsi que les éventuelles limites dans les [détails des connecteurs](/connectors/sftpconnector/).</span><span class="sxs-lookup"><span data-stu-id="19e20-127">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sftpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="19e20-128">Autres connecteurs</span><span class="sxs-lookup"><span data-stu-id="19e20-128">More connectors</span></span>
<span data-ttu-id="19e20-129">Revenir à la [liste des API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="19e20-129">Go back to the [APIs list](apis-list.md).</span></span>