---
title: "aaaCreate une identité ou d’établissement scolaire dans AAD pour Linux | Documents Microsoft"
description: "Découvrez comment toocreate une identité ou d’établissement scolaire dans toouse Azure Active Directory avec vos machines virtuelles de Linux."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: b0f86d77-c669-4aa1-a095-c2aa4d9105fe
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/23/2016
ms.author: rasquill
ms.openlocfilehash: 54c3d0b0e89fe1b2d6a9b58a46776fe446ed72b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-work-or-school-identity-in-azure-active-directory-toouse-with-linux-vms"></a>Création d’une identité d’entreprise ou école dans toouse Azure Active Directory avec les machines virtuelles Linux
Si vous avez créé un compte Azure personnel ou que vous disposer d’un abonnement MSDN personnel créé parti de tootake compte Azure hello de crédits de MSDN Azure hello--que vous avez utilisé un *compte Microsoft* identité toocreate il. Nombreuses fonctionnalités d’Azure-- [modèles de groupe de ressources](../../azure-resource-manager/resource-group-overview.md) est un exemple--requièrent un compte professionnel ou scolaire (une identité géré par Azure Active Directory) toowork. Vous pouvez suivre les instructions hello ci-dessous toocreate nouveau Professionnel ou scolaire compte étant Heureusement, un des principaux avantages de votre compte Azure personnel hello qui l’accompagne un domaine d’Azure Active Directory par défaut que vous pouvez utiliser toocreate nouveau Professionnel ou scolaire compte que vous pouvez utiliser avec les fonctionnalités Azure qui en ont besoin.

Toutefois, les modifications récentes rendent possible toomanage votre abonnement avec n’importe quel type de compte Azure à l’aide de hello `azure login` méthode de connexion interactive décrite [ici](../../xplat-cli-connect.md). Vous pouvez utiliser ce mécanisme, ou vous pouvez suivre les instructions hello qui suivent. Vous pouvez également [créer une identité ou d’établissement scolaire dans toouse Azure Active Directory avec les machines virtuelles Windows](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

[!INCLUDE [virtual-machines-common-create-aad-work-id](../../../includes/virtual-machines-common-create-aad-work-id.md)]

