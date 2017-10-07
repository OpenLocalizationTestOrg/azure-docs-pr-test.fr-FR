---
title: "Préparer la cible (tooAzure physique) | Documents Microsoft"
description: "Cet article décrit comment tooprepare votre toostart environnement Azure réplication des serveurs physiques exécutant tooAzure Windows ou Linux."
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhemraj
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 5/31/2017
ms.author: bsiva
ms.openlocfilehash: 126fb86133e1a00f5669410943565c4cd78e4369
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-target-vmware-tooazure"></a>Préparer la cible (tooAzure VMware)
> [!div class="op_single_selector"]
> * [VMware tooAzure](./site-recovery-prepare-target-vmware-to-azure.md)
> * [TooAzure physique](./site-recovery-prepare-target-physical-to-azure.md)

Cet article décrit comment tooprepare votre toostart environnement Azure réplication des serveurs physiques (x 64) exécutant Windows ou Linux dans Azure.

## <a name="prerequisites"></a>Composants requis

article de Hello suppose hello qui suit :
- Vous avez créé un tooprotect coffre Recovery Services vos serveurs physiques. Vous pouvez créer un coffre Recovery Services depuis hello [portail Azure](http://portal.azure.com "portail Azure").
- Vous avez [le programme d’installation de votre environnement local](./site-recovery-set-up-physical-to-azure.md) tooreplicate serveurs physiques tooAzure.

## <a name="prepare-target"></a>Préparer la cible

Après avoir effectué hello **objectif de Protection étape 1 : sélectionnez** et **étape 2 : préparer la Source**, vous accédez trop**étape 3 : cible**

![Préparer la cible](./media/site-recovery-prepare-target-physical-to-azure/prepare-target-physical-to-azure.png)

1. **L’abonnement :** de hello menu déroulant, sélectionnez hello abonnement que vous souhaitez tooreplicate vos serveurs physiques.
2. **Modèle de déploiement :** modèle de déploiement hello Select (Gestionnaire de ressources ou classique)

En fonction de hello choisi le modèle de déploiement, une validation est exécutée tooensure avoir au moins un compte de stockage compatible et le réseau virtuel dans tooreplicate d’abonnement hello cible et le basculement de vos serveurs physiques à.

Une fois les validations hello se terminent correctement, cliquez sur OK toogo toohello prochaine étape.

Si vous n’avez pas un compte de stockage compatible avec le Gestionnaire de ressources ou d’un réseau virtuel, ou que vous voulez que tooadd plus, vous pouvez le faire en cliquant sur hello **+ compte de stockage** ou **+ réseau** boutons haut hello Hello panneau.

## <a name="next-steps"></a>Étapes suivantes
[Configurer les paramètres de réplication](./site-recovery-setup-replication-settings-vmware.md)
