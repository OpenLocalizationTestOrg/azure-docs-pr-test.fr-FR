---
title: Connecteur Outlook.com dans Azure Logic Apps | Documents Microsoft
description: "Créez des applications logiques avec Azure App Service. Le connecteur Outlook.com vous permet de gérer votre messagerie, les calendriers et les contacts. Vous pouvez effectuer différentes actions comme envoyer un message, planifier des réunions, ajouter des contacts, etc."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 87113c85-d158-4dd5-9ed5-5748130003d6
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: bde1629504c97cf6706b42219570ffa6243073dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-outlookcom-connector"></a><span data-ttu-id="acf1a-105">Prise en main du connecteur Outlook.com</span><span class="sxs-lookup"><span data-stu-id="acf1a-105">Get started with the Outlook.com connector</span></span>
<span data-ttu-id="acf1a-106">Le connecteur Outlook.com vous permet de gérer votre messagerie, les calendriers et les contacts.</span><span class="sxs-lookup"><span data-stu-id="acf1a-106">Outlook.com connector allows you to manage your mail, calendars, and contacts.</span></span> <span data-ttu-id="acf1a-107">Vous pouvez effectuer différentes actions comme envoyer un message, planifier des réunions, ajouter des contacts, etc.</span><span class="sxs-lookup"><span data-stu-id="acf1a-107">You can perform various actions such as send mail, schedule meetings, add contacts, etc.</span></span>

<span data-ttu-id="acf1a-108">Vous pouvez commencer par créer une application logique. Pour cela, consultez [Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="acf1a-108">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-outlookcom"></a><span data-ttu-id="acf1a-109">Créer une connexion à Outlook.com</span><span class="sxs-lookup"><span data-stu-id="acf1a-109">Create a connection to Outlook.com</span></span>
<span data-ttu-id="acf1a-110">Pour créer des applications logiques avec Outlook.com, vous devez d’abord créer une **connexion**, puis fournir les détails pour les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="acf1a-110">To create Logic apps with Outlook.com, you must first create a **connection** then provide the details for the following properties:</span></span>

| <span data-ttu-id="acf1a-111">Propriété</span><span class="sxs-lookup"><span data-stu-id="acf1a-111">Property</span></span> | <span data-ttu-id="acf1a-112">Requis</span><span class="sxs-lookup"><span data-stu-id="acf1a-112">Required</span></span> | <span data-ttu-id="acf1a-113">Description</span><span class="sxs-lookup"><span data-stu-id="acf1a-113">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="acf1a-114">Jeton</span><span class="sxs-lookup"><span data-stu-id="acf1a-114">Token</span></span> |<span data-ttu-id="acf1a-115">Oui</span><span class="sxs-lookup"><span data-stu-id="acf1a-115">Yes</span></span> |<span data-ttu-id="acf1a-116">Fournir des informations d’identification Outlook.com</span><span class="sxs-lookup"><span data-stu-id="acf1a-116">Provide Outlook.com Credentials</span></span> |

<span data-ttu-id="acf1a-117">Après avoir créé la connexion, vous pouvez l’utiliser pour exécuter les actions et écouter les déclencheurs décrits dans cet article.</span><span class="sxs-lookup"><span data-stu-id="acf1a-117">After you create the connection, you can use it to execute the actions and listen for the triggers described in this article.</span></span>

> [!INCLUDE [Steps to create a connection to Outlook.com](../../includes/connectors-create-api-outlook.md)]
>

## <a name="connector-specific-details"></a><span data-ttu-id="acf1a-118">Détails spécifiques aux connecteurs</span><span class="sxs-lookup"><span data-stu-id="acf1a-118">Connector-specific details</span></span>

<span data-ttu-id="acf1a-119">Consultez tous les déclencheurs et les actions définies dans le swagger, ainsi que les éventuelles limites dans les [détails des connecteurs](/connectors/outlook/).</span><span class="sxs-lookup"><span data-stu-id="acf1a-119">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/outlook/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="acf1a-120">Autres connecteurs</span><span class="sxs-lookup"><span data-stu-id="acf1a-120">More connectors</span></span>
<span data-ttu-id="acf1a-121">Revenir à la [liste des API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="acf1a-121">Go back to the [APIs list](apis-list.md).</span></span>