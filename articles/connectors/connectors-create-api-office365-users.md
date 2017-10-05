---
title: "Ajouter le connecteur Office 365 Users à des applications logiques | Microsoft Docs"
description: "Vue d’ensemble du connecteur Office 365 Users avec les paramètres de l’API REST"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b2146481-9105-4f56-b4c2-7ae340cb922f
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 330f733440932a769eb0fe6031cd0d947a820080
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-office-365-users-connector"></a><span data-ttu-id="6f9c1-103">Prise en main du connecteur Office 365 Users</span><span class="sxs-lookup"><span data-stu-id="6f9c1-103">Get started with the Office 365 Users connector</span></span>
<span data-ttu-id="6f9c1-104">Connexion à Office 365 Users pour obtenir des profils, rechercher des utilisateurs, et plus encore.</span><span class="sxs-lookup"><span data-stu-id="6f9c1-104">Connect to Office 365 Users to get profiles, search users, and more.</span></span> <span data-ttu-id="6f9c1-105">Avec Office 365 Users, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="6f9c1-105">With Office 365 Users, you can:</span></span>

* <span data-ttu-id="6f9c1-106">Créer votre flux d’activité en fonction des données que vous obtenez d’Office 365 Users.</span><span class="sxs-lookup"><span data-stu-id="6f9c1-106">Build your business flow based on the data you get from Office 365 Users.</span></span> 
* <span data-ttu-id="6f9c1-107">Utilisez des actions qui permettent d’obtenir les collaborateurs, le profil utilisateur d’un responsable, et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="6f9c1-107">Use actions that get direct reports, get a manager's user profile, and more.</span></span> <span data-ttu-id="6f9c1-108">Ces actions obtiennent une réponse, puis mettent la sortie à la disposition d'autres actions.</span><span class="sxs-lookup"><span data-stu-id="6f9c1-108">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="6f9c1-109">Vous pouvez, par exemple, obtenir les collaborateurs d’une personne, puis prendre ces informations et mettre à jour une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="6f9c1-109">For example, get a person's direct reports, and then take this information and update a SQL Azure database.</span></span> 

<span data-ttu-id="6f9c1-110">Vous pouvez commencer par créer une application logique. Pour cela, consultez [Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="6f9c1-110">You can get started by creating a logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-office-365-users"></a><span data-ttu-id="6f9c1-111">Créer une connexion à Office 365 Users</span><span class="sxs-lookup"><span data-stu-id="6f9c1-111">Create a connection to Office 365 Users</span></span>
<span data-ttu-id="6f9c1-112">Quand vous ajoutez ce connecteur à vos applications logiques, vous devez vous connecter à votre compte Office 365 Users et autoriser les applications logiques à se connecter à votre compte.</span><span class="sxs-lookup"><span data-stu-id="6f9c1-112">When you add this connector to your logic apps, you must sign-in to your Office 365 Users account and allow logic apps to connect to your account.</span></span>

> [!INCLUDE [Steps to create a connection to Office 365 Users](../../includes/connectors-create-api-office365users.md)]
> 
> 

<span data-ttu-id="6f9c1-113">Après avoir créé la connexion, vous entrez les propriétés Office 365 Users, notamment l’ID client.</span><span class="sxs-lookup"><span data-stu-id="6f9c1-113">After you create the connection, you enter the Office 365 Users properties, like the user ID.</span></span> <span data-ttu-id="6f9c1-114">La section **Informations de référence sur l’API REST** dans cette rubrique décrit ces propriétés.</span><span class="sxs-lookup"><span data-stu-id="6f9c1-114">The **REST API reference** in this topic describes these properties.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="6f9c1-115">Détails spécifiques aux connecteurs</span><span class="sxs-lookup"><span data-stu-id="6f9c1-115">Connector-specific details</span></span>

<span data-ttu-id="6f9c1-116">Consultez tous les déclencheurs et les actions définies dans le swagger, ainsi que les éventuelles limites dans les [détails des connecteurs](/connectors/officeusers/).</span><span class="sxs-lookup"><span data-stu-id="6f9c1-116">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/officeusers/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="6f9c1-117">Autres connecteurs</span><span class="sxs-lookup"><span data-stu-id="6f9c1-117">More connectors</span></span>
<span data-ttu-id="6f9c1-118">Revenir à la [liste des API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="6f9c1-118">Go back to the [APIs list](apis-list.md).</span></span>