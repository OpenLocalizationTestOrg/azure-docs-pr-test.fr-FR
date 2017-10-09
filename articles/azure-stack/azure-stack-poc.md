---
title: "aaaWhat est la pile de Azure ? | Microsoft Docs"
description: "Le Kit de développement Azure Stack est un environnement qui permet d’évaluer les scénarios et fonctionnalités d’Azure Stack."
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: d9e6aee1-4cba-4df5-b5a3-6f38da9627a3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: helaw
ms.custom: mvc
ms.openlocfilehash: 3f7c84f2302a6411f49a07de171501fbd72812e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-stack"></a>Qu’est-ce qu’Azure Stack ?

Microsoft Azure Stack est une plateforme cloud hybride permettant de créer des services Azure à partir du centre de données de votre organisation.  Pile Azure est conçue toohelp dans des scénarios clés, telles que des exigences de sécurité et conformité, ou lorsque vous devez tooaccess des ressources Azure sans connectivité internet.  

## <a name="azure-stack-development-kit"></a>Kit de développement Azure Stack
Kit de développement Microsoft Azure pile est une version à un seul nœud de pile Azure, que vous pouvez utiliser tooevaluate et en savoir plus sur la pile de Azure.  Vous pouvez également utiliser le Kit de développement Azure Stack comme environnement de développement, où vous pouvez développer à l’aide d’API et d’outils cohérents.  

Notez les points suivants concernant le Kit de développement Azure Stack :

* Vous ne devez pas utiliser le Kit de développement Azure Stack comme un environnement de production, mais uniquement à des fins de test, d’évaluation et de démonstration.  
* Votre déploiement d’Azure Stack est associé à un seul fournisseur d’identité Azure Active Directory ou AD FS (Active Directory Federation Services). Vous pouvez créer plusieurs utilisateurs dans ce répertoire et affecter les abonnements tooeach utilisateur.
* Avec tous les composants sont déployés sur un seul ordinateur de hello, limité de ressources physiques sont disponibles pour les ressources du client. Cette configuration n’est pas destinée à l’évaluation des performances ou de la mise à l’échelle.
* Scénarios de mise en réseau sont limités en raison de l’exigence de carte réseau/hôte unique toohello.

## <a name="next-steps"></a>Étapes suivantes
[Principaux concepts et fonctionnalités](azure-stack-key-features.md)

[Hybrid Application innovation with Azure and Azure Stack (pdf) (Innovation d’application hybride avec Azure et Azure Stack (pdf)](https://go.microsoft.com/fwlink/?LinkId=842846&clcid=0x409)

