---
title: aaaMonitor Surface Hub avec Analytique de journal Azure | Documents Microsoft
description: "Utilisez hello Surface Hub solution tootrack hello d’intégrité de votre Surface Hub et comprendre comment elles sont utilisées."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 8b4e56bc-2d4f-4648-a236-16e9e732ebef
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 623d30e749cafdd4a34ba0c5b3408164f1b4a95b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-surface-hubs-with-log-analytics-tootrack-their-health"></a>Surveiller la Surface Hub avec Analytique de journal tootrack leur intégrité

![Symbole de Surface Hub](./media/log-analytics-surface-hubs/surface-hub-symbol.png)

Cet article décrit comment vous pouvez utiliser hello solution de Surface Hub dans les appareils Microsoft Surface Hub Analytique de journal toomonitor avec hello Microsoft Operations Management Suite (OMS). Ouvrez une session permet d’Analytique suivre la santé hello de vos concentrateurs de Surface ainsi que pour comprendre comment elles sont utilisées.

Chaque Surface Hub a hello que Microsoft Monitoring Agent installé. Son via agent hello que vous pouvez envoyer des données à partir de votre tooOMS Surface Hub. Les fichiers journaux sont lus à partir de votre Surface Hub et le sont, puis sont envoyées service OMS de toohello. Problèmes comme serveurs est hors ligne, hello calendrier ne synchronise ne pas ou si le compte d’appareil hello est toolog impossible dans Skype sont affichés dans OMS dans le tableau de bord hello Surface Hub. À l’aide de données de salutation dans le tableau de bord hello, vous pouvez identifier les appareils qui ne sont pas en cours d’exécution, ou qui ont d’autres problèmes et éventuellement appliquer des correctifs pour les problèmes de hello détecté.

## <a name="installing-and-configuring-hello-solution"></a>L’installation et la configuration de solution de hello
Utilisez hello suivant tooinstall des informations et configurer une solution de hello. Dans l’ordre toomanage vos Hubs de Surface de hello Microsoft Operations Management Suite (OMS), vous devez hello suivant :

* Un abonnement valide trop[OMS](http://www.microsoft.com/oms).
* Un [abonnement OMS](https://azure.microsoft.com/pricing/details/log-analytics/) niveau qui prendra en charge hello nombre de périphériques vous souhaitez toomonitor. La tarification d’OMS varie selon le nombre d’appareils inscrits et la quantité de données traitées. Vous souhaiterez tootake cela en considération lorsque vous planifiez votre déploiement Surface Hub.

Ensuite, vous soit ajouter un abonnement Microsoft Azure OMS abonnement tooyour existant ou créer un espace de travail directement par le biais du portail OMS hello. Pour des instructions détaillées sur ces deux méthodes, voir [Prise en main de Log Analytics](log-analytics-get-started.md). Une fois hello abonnement OMS est configurée, il existe deux façons tooenroll vos appareils Surface Hub :

* automatiquement via Intune ;
* manuellement, via les **Paramètres** de votre appareil Surface Hub.

## <a name="set-up-monitoring"></a>Configurez l’analyse
Vous pouvez surveiller la santé hello et l’activité de votre Surface Hub à l’aide d’Analytique de journal d’OMS. Vous pouvez inscrire hello Surface Hub dans OMS à l’aide d’Intune ou localement à l’aide **paramètres** sur hello Surface Hub.

## <a name="connect-surface-hubs-toooms-through-intune"></a>Se connecter tooOMS de Surface Hub via Intune
Vous aurez besoin hello ID et la clé d’espace de travail pour espace de travail hello OMS destiné à gérer votre Surface Hub. Vous pouvez obtenir ceux à partir du portail OMS hello.

Intune est un produit Microsoft qui vous permet de toocentrally gérer les paramètres de configuration d’OMS hello tooone appliqué ou plus de vos appareils. Suivez ces étapes tooconfigure vos appareils via Intune :

1. Connectez-vous tooIntune.
2. Accédez trop**paramètres** > **Sources connectées**.
3. Créer ou modifier une stratégie basée sur le modèle de Surface Hub hello.
4. Accédez de section d’OMS (Azure Operational Insights) toohello de stratégie de hello et ajoutez hello *ID de l’espace de travail* et *clé de l’espace de travail* toohello stratégie.
5. Enregistrer la stratégie de hello.
6. Associer la stratégie de hello groupe approprié de hello d’appareils.

   ![Stratégie Intune](./media/log-analytics-surface-hubs/intune.png)

Intune puis de synchroniser les paramètres d’OMS hello avec des périphériques hello dans le groupe cible hello inscrivant dans votre espace de travail OMS.

## <a name="connect-surface-hubs-toooms-using-hello-settings-app"></a>Se connecter tooOMS Surface Hub à l’aide d’application des paramètres de hello
Vous aurez besoin hello ID et la clé d’espace de travail pour espace de travail hello OMS destiné à gérer votre Surface Hub. Vous pouvez obtenir ceux à partir du portail OMS hello.

Si vous n’utilisez pas Intune toomanage votre environnement, vous pouvez inscrire des appareils manuellement via **paramètres** sur chaque Surface Hub :

1. Sur votre Surface Hub, ouvrez **Paramètres**.
2. Entrez les informations d’identification d’admin de périphérique hello lorsque vous y êtes invité.
3. Cliquez sur **cet appareil**et hello sous **analyse**, cliquez sur **configurer les paramètres d’OMS**.
4. Sélectionnez **Activer l’analyse**.
5. Dans la boîte de dialogue Paramètres de OMS hello, tapez Bonjour **ID de l’espace de travail** et type Bonjour **clé de l’espace de travail**.  
   ![Paramètres](./media/log-analytics-surface-hubs/settings.png)
6. Cliquez sur **OK** configuration de hello toocomplete.

Une confirmation s’affiche vous indiquant ou non hello configuration OMS a été correctement appliquée toohello appareil. S’il est, un message s’affiche indiquant que l’agent hello correctement toohello OMS un service connecté. Appareil de Hello démarre ensuite l’envoi des données tooOMS où vous pouvez afficher et agir sur lui.

## <a name="monitor-surface-hubs"></a>Analyser les Surface Hubs
L’analyse de vos Surface Hubs à l’aide d’OMS est très similaire à l’analyse d’autres appareils inscrits.

1. Se connecter toohello portail OMS.
2. Accédez à tableau de bord du pack de solution toohello Surface Hub.
3. L’intégrité de votre appareil s’affiche.

   ![Tableau de bord de Surface Hub](./media/log-analytics-surface-hubs/surface-hub-dashboard.png)

Vous pouvez créer des [alertes](log-analytics-alerts.md) basées sur des recherches de journal existantes ou personnalisées. À l’aide de hello de données hello QU'OMS collecte à partir de votre Surface Hub, vous pouvez rechercher les problèmes et d’alerte sur les conditions de hello que vous définissez pour vos appareils.

## <a name="next-steps"></a>Étapes suivantes
* Utilisez [connecter recherche Analytique de journal](log-analytics-log-searches.md) tooview détaillé les données de la Surface Hub.
* Créer [alertes](log-analytics-alerts.md) toonotify lorsque des problèmes avec votre Surface Hub.
