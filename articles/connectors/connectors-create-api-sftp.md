---
title: aaaLearn comment toouse hello connecteur SFTP dans vos applications logiques | Documents Microsoft
description: "Créez des applications logiques avec Azure App Service. Se connecter tooSFTP API toosend et recevoir des fichiers. Vous pouvez effectuer diverses opérations, telles que créer, mettre à jour, obtenir ou supprimer des fichiers."
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
ms.openlocfilehash: 3f50570191c9b9339fe6584b9056b2549512b789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sftp-connector"></a><span data-ttu-id="99327-105">Prise en main connecteur SFTP hello</span><span class="sxs-lookup"><span data-stu-id="99327-105">Get started with hello SFTP connector</span></span>
<span data-ttu-id="99327-106">Utilisez hello SFTP connecteur tooaccess un toosend de compte SFTP et recevoir des fichiers.</span><span class="sxs-lookup"><span data-stu-id="99327-106">Use hello SFTP connector tooaccess an SFTP account toosend and receive files.</span></span> <span data-ttu-id="99327-107">Vous pouvez effectuer diverses opérations, telles que créer, mettre à jour, obtenir ou supprimer des fichiers.</span><span class="sxs-lookup"><span data-stu-id="99327-107">You can perform various operations such as create, update, get or delete files.</span></span>  

<span data-ttu-id="99327-108">toouse [n’importe quel connecteur](apis-list.md), vous devez tout d’abord toocreate une application logique.</span><span class="sxs-lookup"><span data-stu-id="99327-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="99327-109">Vous pouvez démarrer maintenant en [créant une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="99327-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toosftp"></a><span data-ttu-id="99327-110">Se connecter tooSFTP</span><span class="sxs-lookup"><span data-stu-id="99327-110">Connect tooSFTP</span></span>
<span data-ttu-id="99327-111">Avant que votre application logique peut accéder à n’importe quel service, vous devez tout d’abord toocreate un *connexion* toohello service.</span><span class="sxs-lookup"><span data-stu-id="99327-111">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="99327-112">Une [connexion](connectors-overview.md) permet d’assurer la connectivité entre une application logique et un autre service.</span><span class="sxs-lookup"><span data-stu-id="99327-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-toosftp"></a><span data-ttu-id="99327-113">Créer un tooSFTP de connexion</span><span class="sxs-lookup"><span data-stu-id="99327-113">Create a connection tooSFTP</span></span>
> [!INCLUDE [Steps toocreate a connection tooSFTP](../../includes/connectors-create-api-sftp.md)]
> 
> 

## <a name="use-an-sftp-trigger"></a><span data-ttu-id="99327-114">Utiliser un déclencheur SFTP</span><span class="sxs-lookup"><span data-stu-id="99327-114">Use an SFTP trigger</span></span>
<span data-ttu-id="99327-115">Un déclencheur est un événement qui peut être utilisé toostart hello flux de travail défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="99327-115">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="99327-116">[En savoir plus sur les déclencheurs](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="99327-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="99327-117">Dans cet exemple, hello **SFTP - lorsqu’un fichier est ajouté ou modifié** déclencheur est tooinitiate utilisé un flux de travail logique application lorsqu’un fichier est ajouté à ou modifié sur un serveur SFTP.</span><span class="sxs-lookup"><span data-stu-id="99327-117">In this example, hello **SFTP - When a file is added or modified** trigger is used tooinitiate a logic app workflow when a file is added to, or modified on, an SFTP server.</span></span> <span data-ttu-id="99327-118">Vous ajoutez également une condition qui vérifie le contenu de hello du fichier nouveau ou modifié de hello et le rend une décision tooextract hello si son contenu indique qu’il doit être extrait avant d’utiliser le contenu de hello.</span><span class="sxs-lookup"><span data-stu-id="99327-118">You also add a condition that checks hello contents of hello new or modified file, and makes a decision tooextract hello file if its contents indicate that it should be extracted before using hello contents.</span></span> <span data-ttu-id="99327-119">Enfin, ajouter un contenu de hello tooextract action d’un fichier et placer le contenu de hello extrait dans un dossier sur le serveur SFTP de hello.</span><span class="sxs-lookup"><span data-stu-id="99327-119">Finally, add an action tooextract hello contents of a file, and place hello extracted contents in a folder on hello SFTP server.</span></span> 

<span data-ttu-id="99327-120">Dans un exemple d’entreprise, vous pouvez utiliser cette toomonitor déclencheur un dossier SFTP pour les nouveaux fichiers qui représentent des commandes client.</span><span class="sxs-lookup"><span data-stu-id="99327-120">In an enterprise example, you could use this trigger toomonitor an SFTP folder for new files that represent customer orders.</span></span>  <span data-ttu-id="99327-121">Vous pouvez ensuite utiliser une action de connecteur SFTP, tel que **obtenir le contenu du fichier**, contenu de hello tooget de commande hello pour poursuivre le traitement et de stockage dans une base de données de commandes.</span><span class="sxs-lookup"><span data-stu-id="99327-121">You could then use an SFTP connector action, such as **Get file content**, tooget hello contents of hello order for further processing and storage in an orders database.</span></span>

> [!INCLUDE [Steps toocreate an SFTP trigger](../../includes/connectors-create-api-sftp-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="99327-122">Ajouter une condition</span><span class="sxs-lookup"><span data-stu-id="99327-122">Add a condition</span></span>
> [!INCLUDE [Steps tooadd a condition](../../includes/connectors-create-api-sftp-condition.md)]
> 
> 

## <a name="use-an-sftp-action"></a><span data-ttu-id="99327-123">Utiliser une action SFTP</span><span class="sxs-lookup"><span data-stu-id="99327-123">Use an SFTP action</span></span>
<span data-ttu-id="99327-124">Une action est une opération effectuée par flux de travail hello défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="99327-124">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="99327-125">[En savoir plus sur les actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="99327-125">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps toocreate an SFTP action](../../includes/connectors-create-api-sftp-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="99327-126">Détails spécifiques du connecteur</span><span class="sxs-lookup"><span data-stu-id="99327-126">Connector-specific details</span></span>

<span data-ttu-id="99327-127">Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/sftpconnector/).</span><span class="sxs-lookup"><span data-stu-id="99327-127">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/sftpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="99327-128">Autres connecteurs</span><span class="sxs-lookup"><span data-stu-id="99327-128">More connectors</span></span>
<span data-ttu-id="99327-129">Revenir en arrière toohello [liste des API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="99327-129">Go back toohello [APIs list](apis-list.md).</span></span>
