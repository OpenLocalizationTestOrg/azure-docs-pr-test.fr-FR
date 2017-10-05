---
title: SendGrid | Microsoft Docs
description: "Créez des applications logiques avec Azure App Service. Le fournisseur de connexion SendGrid vous permet d’envoyer un message électronique et de gérer les listes de destinataires."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: bc4f1fc2-824c-4ed7-8de8-e82baff3b746
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 9ff0591741899d65b8274fb14ab3f3c8db9abe36
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-sendgrid-connector"></a><span data-ttu-id="7c00c-104">Prise en main du connecteur SendGrid</span><span class="sxs-lookup"><span data-stu-id="7c00c-104">Get started with the SendGrid connector</span></span>
<span data-ttu-id="7c00c-105">Le fournisseur de connexion SendGrid vous permet d’envoyer un message électronique et de gérer les listes de destinataires.</span><span class="sxs-lookup"><span data-stu-id="7c00c-105">SendGrid Connection Provider lets you send email and manage recipient lists.</span></span>

<span data-ttu-id="7c00c-106">Vous pouvez commencer par créer une application logique. Pour cela, consultez [Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="7c00c-106">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-sendgrid"></a><span data-ttu-id="7c00c-107">Créer une connexion à SendGrid</span><span class="sxs-lookup"><span data-stu-id="7c00c-107">Create a connection to SendGrid</span></span>
<span data-ttu-id="7c00c-108">Pour créer des applications logiques avec SendGrid, vous devez d’abord créer une **connexion**, puis fournir les détails pour les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="7c00c-108">To create Logic apps with SendGrid, you must first create a **connection** then provide the details for the following properties:</span></span> 

| <span data-ttu-id="7c00c-109">Propriété</span><span class="sxs-lookup"><span data-stu-id="7c00c-109">Property</span></span> | <span data-ttu-id="7c00c-110">Requis</span><span class="sxs-lookup"><span data-stu-id="7c00c-110">Required</span></span> | <span data-ttu-id="7c00c-111">Description</span><span class="sxs-lookup"><span data-stu-id="7c00c-111">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7c00c-112">ApiKey</span><span class="sxs-lookup"><span data-stu-id="7c00c-112">ApiKey</span></span> |<span data-ttu-id="7c00c-113">Oui</span><span class="sxs-lookup"><span data-stu-id="7c00c-113">Yes</span></span> |<span data-ttu-id="7c00c-114">Fournir votre clé d’API SendGrid</span><span class="sxs-lookup"><span data-stu-id="7c00c-114">Provide Your SendGrid Api Key</span></span> |

> [!INCLUDE [Steps to create a connection to SendGrid](../../includes/connectors-create-api-sendgrid.md)]
> 


<span data-ttu-id="7c00c-115">Après avoir créé la connexion, vous pouvez l’utiliser pour exécuter les actions et écouter les déclencheurs.</span><span class="sxs-lookup"><span data-stu-id="7c00c-115">After you create the connection, you can use it to execute the actions and listen for the triggers.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="7c00c-116">Détails spécifiques aux connecteurs</span><span class="sxs-lookup"><span data-stu-id="7c00c-116">Connector-specific details</span></span>

<span data-ttu-id="7c00c-117">Consultez tous les déclencheurs et les actions définies dans le swagger, ainsi que les éventuelles limites dans les [détails des connecteurs](/connectors/sendgrid/).</span><span class="sxs-lookup"><span data-stu-id="7c00c-117">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sendgrid/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="7c00c-118">Autres connecteurs</span><span class="sxs-lookup"><span data-stu-id="7c00c-118">More connectors</span></span>
<span data-ttu-id="7c00c-119">Revenir à la [liste des API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="7c00c-119">Go back to the [APIs list](apis-list.md).</span></span>