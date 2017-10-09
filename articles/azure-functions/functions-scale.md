---
title: plans de consommation de fonctions et le Service application aaaAzure | Documents Microsoft
description: "Comprendre comment les fonctions Azure met à l’échelle toomeet les besoins de hello de vos charges de travail pilotée par événements."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, fonctions, traitement des événements, webhooks, calcul dynamique, architecture sans serveur"
ms.assetid: 5b63649c-ec7f-4564-b168-e0a74cb7e0f3
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/12/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3826915b93328635d9295efe90ecc421e6c56af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-consumption-and-app-service-plans"></a>Plans Consommation et App Service d’Azure Functions 

## <a name="introduction"></a>Introduction

Vous pouvez exécuter la solution Azure Functions dans deux modes : le plan Consommation et le plan Azure App Service. plan de la consommation Hello alloue automatiquement la puissance de calcul lorsque votre code est en cours d’exécution, peut évoluer en tant que charge de toohandle nécessaires, puis met à l’échelle vers le bas lorsque le code n’est pas en cours d’exécution. Par conséquent, vous n’avez toopay pour les machines virtuelles inactives et n’avez pas la capacité de tooreserve à l’avance. Cet article se concentre sur le plan de la consommation hello. Pour plus d’informations sur le fonctionne de hello plan App Service, consultez hello [vue d’ensemble approfondie des plans de Service d’applications Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

Si vous n’êtes pas familiarisé avec les fonctions d’Azure, consultez hello [vue d’ensemble des fonctions d’Azure](functions-overview.md).

Lorsque vous créez une application de la fonction, vous devez configurer un plan d’hébergement pour les fonctions contient cette application hello. Dans les deux modes, une instance de hello *hôte des fonctions d’Azure* exécute les fonctions hello. type Hello des contrôles de plan :

* la façon dont les instances d’hôte font l’objet d’une augmentation de taille ;
* ressources Hello disponible tooeach hôte.

Actuellement, vous devez choisir le type de plan hello lors de la création de hello d’application de fonction hello. Vous ne pouvez pas en changer ultérieurement. 

Vous pouvez mettre à l’échelle entre les couches sur hello plan App Service. Sur le plan de la consommation de hello, les fonctions Azure gère automatiquement toute allocation de ressources.

## <a name="consumption-plan"></a>Plan de consommation

Lorsque vous utilisez un plan de la consommation, les instances d’hôte de fonctions d’Azure hello sont ajoutés et supprimés dynamiquement en fonction de nombre hello d’événements entrants. Ce plan est mis à l’échelle automatiquement, et vous êtes facturé pour les ressources de calcul uniquement quand vos fonctions sont exécutées. Dans un plan Consommation, une fonction peut s’exécuter pendant 10 minutes au plus. 

> [!NOTE]
> délai d’attente par défaut de Hello pour les fonctions sur un plan de la consommation est de 5 minutes. valeur de Hello peut être accrue too10 minutes hello fonction application en modifiant la propriété de hello `functionTimeout` dans [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).

La facturation est basée sur la durée d’exécution et la mémoire utilisée. Elle est agrégée dans toutes les fonctions d’une application de fonction. Pour plus d’informations, consultez hello [fonctions Azure page de tarification].

plan de la consommation Hello est hello par défaut et offre hello avantages suivants :
- Paiement uniquement à l’exécution de vos fonctions
- Augmentation automatique de la taille des instances même pendant les périodes de charge élevée

## <a name="app-service-plan"></a>Plan App Service

Bonjour du Service d’applications planifier, vos applications de la fonction exécutent sur des machines virtuelles dédiées sur Basic, Standard et Premium SKU, tooWeb applications similaires. Machines virtuelles dédiés sont des applications de Service d’applications tooyour alloué, ce qui signifie que l’hôte de fonctions hello est toujours en cours d’exécution.

Considérez un plan App Service Bonjour suivant cas :
- Vous disposez de machines virtuelles existantes, sous-utilisées qui exécutent déjà d’autres instances App Service.
- Vous attendez votre toorun d’applications de fonction en continu, ou presque en continu.
- Vous avez besoin de plus d’options de mémoire ou de processeur que celle fournie sur le plan de la consommation hello.
- Vous devez toorun plu de hello durée d’exécution maximale autorisée sur le plan de la consommation hello.

L’utilisation d’une machine virtuelle dissocie le coût de l’exécution et de la taille de mémoire. Par conséquent, vous ne payez plus à celui de l’instance de machine virtuelle hello que vous allouez de hello. Pour plus d’informations sur le fonctionne de hello plan App Service, consultez hello [vue d’ensemble approfondie des plans de Service d’applications Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

Avec un plan App Service, vous pouvez augmenter manuellement la taille des instances en ajoutant des instances de machine virtuelle, ou vous pouvez activer la mise à l’échelle automatique. Pour plus d’informations, consultez [Mettre à l’échelle le nombre d’instances manuellement ou automatiquement](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json). Vous pouvez également effectuer une montée en puissance en choisissant un autre plan App Service. Pour plus d’informations, consultez [Faire monter en puissance une application web dans Azure](../app-service-web/web-sites-scale.md). Si vous prévoyez toorun les fonctions JavaScript sur un plan App Service, vous devez choisir un plan qui a moins de cœurs. Pour plus d’informations, consultez hello [référence JavaScript pour les fonctions](functions-reference-node.md#choose-single-core-app-service-plans).  

<!-- Note: hello portal links toothis section via fwlink https://go.microsoft.com/fwlink/?linkid=830855 --> 
<a name="always-on"></a>
### Toujours actif

Si vous exécutez sur un plan App Service, vous devez activer hello **Always On** paramètre afin que votre application de la fonction s’exécute correctement. Sur un plan App Service, hello fonctions runtime devient inactif après quelques minutes d’inactivité, donc seuls les déclencheurs HTTP « réveille » vos fonctions. Il s’agit de toohow similaire que tâches Web doivent avoir Always On est activé. 

Le paramètre Toujours actif est disponible uniquement dans un plan App Service. Sur un plan de la consommation, plateforme de hello active automatiquement les applications de la fonction.

## <a name="storage-account-requirements"></a>Conditions requises pour le compte de stockage

Dans un plan Consommation ou un plan App Service, une application de fonction nécessite un compte de stockage Azure qui prend en charge les stockages Azure Blob, File d’attente et Table. En interne, Azure Functions utilise le stockage Azure pour les opérations telles que la gestion des déclencheurs et la journalisation des exécutions de fonctions. Certains comptes de stockage ne prennent pas en charge les files d’attente et les tables, comme les comptes de stockage Blob uniquement (notamment le stockage Premium) et les comptes de stockage à usage général avec la réplication ZRS. Ces comptes sont filtrés à partir de hello **compte de stockage** panneau lorsque vous créez une application de la fonction.

toolearn savoir plus sur les types de compte de stockage, consultez [présentation des services de stockage Azure hello](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).

## <a name="how-hello-consumption-plan-works"></a>Fonctionne du plan de la consommation de hello

plan de la consommation Hello s’ajuste automatiquement les ressources processeur et mémoire en ajoutant des instances supplémentaires de l’hôte de fonctions hello, en fonction du nombre de hello d’événements déclenchés sur ses fonctions. Chaque instance d’hôte de fonctions hello est limitée too1.5 Go de mémoire.

Lorsque vous utilisez hello consommation plan d’hébergement, les fichiers de code de fonction sont stockés sur des partages de fichiers Azure hello principal compte de stockage. Lorsque vous supprimez le compte de stockage principal hello, ce contenu est supprimé et ne peut pas être récupéré.

> [!NOTE]
> Lorsque vous utilisez un déclencheur d’objets blob sur un plan de la consommation, il peut être d’un délai de 10 minutes tooa lors du traitement de nouveaux objets BLOB si une application de la fonction est devenu inactive. Après que application de fonction hello est en cours d’exécution, les objets BLOB est traitées immédiatement. tooavoid initiale de ce délai, envisagez l’une des options suivantes de hello :
> - Utilisez un plan App Service avec le paramètre Toujours actif activé.
> - Utiliser un autre mécanisme tootrigger hello objet blob de traitement, par exemple un message de la file d’attente qui contient le nom d’objet blob hello. Pour un exemple, consultez [Déclencheur de file d’attente avec liaison d’entrée d’objet blob](functions-bindings-storage-blob.md#input-sample).

### <a name="runtime-scaling"></a>Mise à l’échelle du runtime

Les fonctions Azure utilise un composant appelé hello *contrôleur de mise à l’échelle* toomonitor hello taux d’événements et de déterminer si tooscale du délai d’attente ou à l’échelle. contrôleur d’échelle Hello utilise l’heuristique pour chaque type de déclencheur. Par exemple, lorsque vous utilisez un déclencheur de stockage de file d’attente Azure, il met à l’échelle en fonction de la longueur de file d’attente hello et l’âge de hello du plus ancien message de file d’attente hello.

Hello l’unité d’échelle est application de fonction hello. Lors de l’application de fonction hello est remontée, davantage de ressources sont allouées toorun plusieurs instances d’hôte de fonctions d’Azure hello. À l’inverse, en tant que calcul de la demande est réduite, contrôleur de mise à l’échelle hello supprime les instances d’hôte (fonction). nombre de Hello d’instances est réduite par la suite toozero lorsque aucune fonction ne s’exécutent au sein d’une application de la fonction.

![Contrôleur de mise à l’échelle surveillant les événements et créant des instances](./media/functions-scale/central-listener.png)

### <a name="billing-model"></a>Modèle de facturation

Facturation de plan de la consommation hello est décrite en détail sur hello [fonctions Azure page de tarification]. L’utilisation est agrégée au niveau application de fonction hello et compte uniquement les temps de hello code de fonction est en cours d’exécution. unités pour la facturation sont les suivantes de Hello : 
* **Consommation des ressources en gigaoctet/seconde (Go/s)**. Calcul effectué d’après une combinaison de la taille de la mémoire et de la durée d’exécution pour toutes les fonctions d’une application de fonction. 
* **Exécutions**. Compté chaque fois qu’une fonction est exécutée dans l’événement tooan de réponse, déclenché par une liaison.

[fonctions Azure page de tarification]: https://azure.microsoft.com/pricing/details/functions
