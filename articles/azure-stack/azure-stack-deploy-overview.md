---
title: "démarrage rapide de déploiement aaaAzure Kit de développement de pile | Documents Microsoft"
description: "Découvrez comment toodeploy hello Kit de développement de pile Azure"
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: erikje
ms.custom: mvc
ms.openlocfilehash: 7f9fcd3a620e2916a24e57990d93dc9ace2b1129
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stack-development-kit-deployment-quickstart"></a>Démarrage rapide du déploiement du Kit de développement Azure Stack

Hello [Kit de développement Azure pile](azure-stack-poc.md) est un environnement de développement et de test que vous pouvez déployer tooevaluate et illustrer les fonctionnalités de la pile d’Azure et les services. tooget, configurez-le et en cours d’exécution, vous aurez besoin de matériel d’environnement tooprepare hello et exécuter des scripts (Ceci peut prendre plusieurs heures). Après cela, vous pouvez connectez-vous toohello admin et locataire portails toomanage Azure pile et tester des offres. 

1. [**Planifiez votre matériel, vos logiciels et votre réseau**](azure-stack-deploy.md). ordinateur Hello qui héberge le kit de développement hello (hôte de kit de développement hello) doit respecter la configuration réseau requise, logiciel et matériel. Vous devez également déterminer si vous allez utiliser Azure Active Directory ou les services de fédération Active Directory (AD FS). Être toocomply que ces conditions préalables avant de commencer votre déploiement afin que le processus d’installation Bonjour s’exécute correctement. 

2. [**Téléchargez et extrayez le package de déploiement hello**](azure-stack-run-powershell-script.md#download-and-extract-the-development-kit). Vous pouvez télécharger ordinateur hôte du kit de développement hello déploiement package toohello ou tooa un autre ordinateur. Hello extraites des fichiers prennent jusqu'à 60 Go d’espace disque libre, donc à l’aide d’un autre ordinateur peut aider à réduire hello configuration matérielle requise pour hôte de kit de développement hello de déploiement.

3. [**Préparer l’hôte de kit de développement hello** ](azure-stack-run-powershell-script.md#prepare-the-development-kit-host) à l’aide du programme d’installation hello. Après cette étape, hôte de kit de développement hello démarrera toohello Cloudbuilder.vhdx (un disque dur virtuel qui inclut un système d’exploitation amorçable et le hello Azure pile installer les fichiers).

4. [**Déployer le kit de développement hello** ](azure-stack-run-powershell-script.md#deploy-the-development-kit) sur l’hôte de kit de développement hello.

5. Si votre déploiement Azure pile utilise Azure Active Directory, vous devez [inscrire la pile d’Azure avec Azure](azure-stack-register.md) afin que vous puissiez [télécharger les éléments d’Azure marketplace](azure-stack-download-azure-marketplace-item.md) tooAzure pile.

Après toutes ces étapes, l’environnement pour le Kit de développement est prêt, avec les portails de l’administrateur et du client. Ensuite, vous pouvez [vous connecter et connectez-vous](azure-stack-connect-azure-stack.md) toohello portal. Vous pouvez ensuite démarrer un déploiement de fournisseurs de ressources, la création de [offre](azure-stack-key-features.md#regions-services-plans-offers-and-subscriptions), et le remplissage hello Azure pile [marketplace](azure-stack-marketplace.md).
