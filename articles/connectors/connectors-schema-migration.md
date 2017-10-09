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
# <a name="how-toomigrate-logic-apps-tooschema-version-2015-08-01-preview"></a>Comment toomigrate logique applications tooschema version 2015-08-01-preview
toomove votre logique applications toohello nouveau schéma existant, procédez comme hello suivant :  

1. Ouvrez votre application de la logique dans hello portail Azure  
2. Cliquez sur Mettre à jour le schéma.
   
   ![Icône API][step1]   
   page de mise à jour du schéma de Hello affiche et fournit un document tooa lien qui fournissent des détails sur les améliorations de hello dans le nouveau schéma de hello : ![icône de l’API][step2]

> [!NOTE]
> Lorsque vous sélectionnez **mise à jour de schéma**, nous automatiquement d’exécuter les étapes de migration hello et fournir le code de sortie de hello pour vous. Vous pouvez utiliser, ce tooupdate votre définition, toutefois, vérifiez que vous suivez les bonnes pratiques de codage telles que celles décrites dans hello **meilleures pratiques** section ci-dessous.
> 
> 

## <a name="best-practices-when-migrating-your-logic-apps-toohello-latest-schema-version"></a>Meilleures pratiques lors de la migration de votre version de schéma logique applications toohello dernière :
* Hello de copie migré script tooa nouvelle logique d’application - ne pas remplacer hello ancien jusqu'à ce que vous avez terminé votre application migrée hello confirmée et de test fonctionne comme prévu.
* Testez votre application logique **avant** sa mise en production
* Une fois la migration terminée, démarrez votre hello de toouse applications logique de mise à jour [API managées](apis-list.md) lorsque cela est possible. Par exemple, vous pouvez commencer à utiliser DropBox v2 partout où vous utilisez DropBox v1.

## <a name="whats-next"></a>Étapes suivantes
* [Découvrez comment toomanually migrer vos applications logiques](../logic-apps/logic-apps-schema-2015-08-01.md)

<!--Icon references-->
[step1]: ./media/connectors-schema-migration/migrateschema1.png
[step2]: ./media/connectors-schema-migration/migrateschema2.png






