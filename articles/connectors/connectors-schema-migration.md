---
title: aaaHow toomigrate logique applications tooschema version 2015-08-01-preview | Documents Microsoft
description: "Vous pouvez facilement migrer votre version du schéma logique applications toohello plus récente. Suivez simplement cette procédure."
services: logic-apps
documentationcenter: 
author: MSFTMAN
manager: erikre
editor: 
tags: connectors
ms.assetid: 3e177e49-fd69-43e9-9b9b-218abb250c31
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2016
ms.author: deonhe
ms.openlocfilehash: c7b42aaec547eddd28b0c649a3c0625047f9f805
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-logic-apps-tooschema-version-2015-08-01-preview"></a><span data-ttu-id="9ca84-104">Comment toomigrate logique applications tooschema version 2015-08-01-preview</span><span class="sxs-lookup"><span data-stu-id="9ca84-104">How toomigrate logic apps tooschema version 2015-08-01-preview</span></span>
<span data-ttu-id="9ca84-105">toomove votre logique applications toohello nouveau schéma existant, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="9ca84-105">toomove your existing logic apps toohello new schema, do hello following:</span></span>  

1. <span data-ttu-id="9ca84-106">Ouvrez votre application de la logique dans hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="9ca84-106">Open your logic app in hello Azure portal</span></span>  
2. <span data-ttu-id="9ca84-107">Cliquez sur Mettre à jour le schéma.</span><span class="sxs-lookup"><span data-stu-id="9ca84-107">Click Update Schema:</span></span>
   
   <span data-ttu-id="9ca84-108">![Icône API][step1] </span><span class="sxs-lookup"><span data-stu-id="9ca84-108">![API Icon][step1] </span></span>  
   <span data-ttu-id="9ca84-109">page de mise à jour du schéma de Hello affiche et fournit un document tooa lien qui fournissent des détails sur les améliorations de hello dans le nouveau schéma de hello : ![icône de l’API][step2]</span><span class="sxs-lookup"><span data-stu-id="9ca84-109">hello Update Schema page displays and provides a link tooa document that provide details on hello improvements in hello new schema: ![API Icon][step2]</span></span>

> [!NOTE]
> <span data-ttu-id="9ca84-110">Lorsque vous sélectionnez **mise à jour de schéma**, nous automatiquement d’exécuter les étapes de migration hello et fournir le code de sortie de hello pour vous.</span><span class="sxs-lookup"><span data-stu-id="9ca84-110">When you select **Update Schema**, we automatically run hello migration steps and provide hello code output for you.</span></span> <span data-ttu-id="9ca84-111">Vous pouvez utiliser, ce tooupdate votre définition, toutefois, vérifiez que vous suivez les bonnes pratiques de codage telles que celles décrites dans hello **meilleures pratiques** section ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="9ca84-111">You can use this tooupdate your definition, however, ensure you follow good coding practices such as those outlined in hello **Best practices** section below.</span></span>
> 
> 

## <a name="best-practices-when-migrating-your-logic-apps-toohello-latest-schema-version"></a><span data-ttu-id="9ca84-112">Meilleures pratiques lors de la migration de votre version de schéma logique applications toohello dernière :</span><span class="sxs-lookup"><span data-stu-id="9ca84-112">Best practices when migrating your Logic apps toohello latest schema version:</span></span>
* <span data-ttu-id="9ca84-113">Hello de copie migré script tooa nouvelle logique d’application - ne pas remplacer hello ancien jusqu'à ce que vous avez terminé votre application migrée hello confirmée et de test fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="9ca84-113">Copy hello migrated script tooa new Logic App - don't overwrite hello old one until you've completed your testing and confirmed hello migrated app works as expected.</span></span>
* <span data-ttu-id="9ca84-114">Testez votre application logique **avant** sa mise en production</span><span class="sxs-lookup"><span data-stu-id="9ca84-114">Test your Logic app **before** putting in production</span></span>
* <span data-ttu-id="9ca84-115">Une fois la migration terminée, démarrez votre hello de toouse applications logique de mise à jour [API managées](apis-list.md) lorsque cela est possible.</span><span class="sxs-lookup"><span data-stu-id="9ca84-115">After migration completes, start updating your Logic apps toouse hello [managed APIs](apis-list.md) where possible.</span></span> <span data-ttu-id="9ca84-116">Par exemple, vous pouvez commencer à utiliser DropBox v2 partout où vous utilisez DropBox v1.</span><span class="sxs-lookup"><span data-stu-id="9ca84-116">For example, you can start using Dropbox v2, whereever you are using DropBox v1.</span></span>

## <a name="whats-next"></a><span data-ttu-id="9ca84-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9ca84-117">What's next</span></span>
* [<span data-ttu-id="9ca84-118">Découvrez comment toomanually migrer vos applications logiques</span><span class="sxs-lookup"><span data-stu-id="9ca84-118">Learn how toomanually migrate your Logic apps</span></span>](../logic-apps/logic-apps-schema-2015-08-01.md)

<!--Icon references-->
[step1]: ./media/connectors-schema-migration/migrateschema1.png
[step2]: ./media/connectors-schema-migration/migrateschema2.png






