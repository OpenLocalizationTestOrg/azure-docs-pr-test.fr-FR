---
title: "aaaHow toodeploy un Service Web toomultiple régions | Documents Microsoft"
description: "Étapes toodeploy (copier) un régions tooother de nouveau Service Web."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: cgronlun
ms.assetid: 36c60411-f2db-4ee2-9b66-b1f1d77a8f44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 21fcdb96f118c60ed98b60b1b2df833766c7c8bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-web-service-toomultiple-regions"></a>Comment toodeploy un Service Web toomultiple régions
Hello nouveaux Services Web de Azure permettent tooeasily déployer un régions toomultiple du service web sans avoir besoin de plusieurs abonnements ou les espaces de travail. 

La tarification est région spécifique, que vous devez donc définir un plan de facturation pour chaque région dans laquelle vous allez déployer le service web de hello.

## <a name="toocreate-a-plan-in-another-region"></a>toocreate un plan dans une autre région
1. Connectez-vous aux [services web Microsoft Azure Machine Learning](https://services.azureml.net/).
2. Cliquez sur hello **Plans** option de menu.
3. Dans les Plans de hello sur la page de vue, cliquez sur **nouveau**.
4. À partir de hello **abonnement** liste déroulante, abonnement hello sélectionnez réside dans le hello nouveau plan.
5. À partir de hello **région** liste déroulante, sélectionnez une région pour le nouveau plan de hello. Hello Options du Plan pour la région sélectionnée hello affichera Bonjour **Options du Plan** section de la page de hello.
6. À partir de hello **groupe de ressources** liste déroulante, sélectionnez une ressource de groupe pour le plan de hello. Pour plus d’informations sur les groupes de ressources, consultez [Vue d’ensemble d’Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
7. Dans **le nom du Plan** nom hello du type de plan de hello.
8. Sous **des Options Plan**, cliquez sur le niveau facturation hello pour le nouveau plan de hello.
9. Cliquez sur **Créer**.

## <a name="deploying-hello-web-service-tooanother-region"></a>Déploiement de service tooanother région hello web
1. Cliquez sur hello **Services Web** option de menu.
2. Sélectionnez Service Web que vous déployez tooa nouvelle région de hello.
3. Cliquez sur **Copy**.
4. Dans **nom du Service Web**, tapez un nouveau nom pour le service web de hello.
5. Dans **description du service Web**, tapez une description de service web de hello.
6. À partir de hello **abonnement** liste déroulante, abonnement hello sélectionnez réside dans le hello nouveau service web.
7. À partir de hello **groupe de ressources** liste déroulante, sélectionnez une ressource de groupe pour le service web de hello. Pour plus d’informations sur les groupes de ressources, consultez [Vue d’ensemble d’Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
8. À partir de hello **région** liste déroulante, la région de hello select dans le service web qui toodeploy hello.
9. À partir de hello **compte de stockage** liste déroulante, sélectionnez un compte de stockage dans le hello toostore de service web.
10. À partir de hello **Plan tarifaire** liste déroulante, sélectionnez un plan dans la région de hello sélectionnée à l’étape 8.
11. Cliquez sur **Copy**.

