---
title: "modèles d’aaaDeploy avec ligne de commande hello dans la pile de Azure | Documents Microsoft"
description: "Découvrez comment toouse hello inter-plateformes interface de ligne de commande (CLI) toodeploy modèles tooAzure pile."
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: 9584177f-4af3-4834-864d-930b09ae0995
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: 6fa6b19ac94d3f020008d04ff07f1ce489aa3418
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-templates-in-azure-stack-using-hello-command-line"></a>Déployer des modèles dans la pile d’Azure à l’aide de la ligne de commande hello
Utilisez Azure Resource Manager modèles toohello Kit de développement de pile Azure hello ligne de commande toodeploy. Les modèles de gestionnaire de ressources Azure déploiement et approvisionnement des toutes les ressources hello pour votre application dans une opération unique et coordonnée.

## <a name="before-you-begin"></a>Avant de commencer
 - [Installer et connecter](azure-stack-connect-cli.md) tooAzure pile avec CLI d’Azure
 - Télécharger les fichiers de hello *azuredeploy.json* et *azuredeploy.parameters.json* de hello [créer l’exemple de modèle compte de stockage](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-create-storage-account).
 
## <a name="deploy-template"></a>Déployer un modèle
Accédez dossier toohello où ces fichiers ont été téléchargés et exécutez hello suivant le modèle de commande toodeploy hello :

    azure group create "cliRG" "local" –f azuredeploy.json –d "testDeploy" –e azuredeploy.parameters.json

Cette commande déploie le groupe de ressources hello modèle toohello **cliRG** dans l’emplacement par défaut de hello Azure pile preuve de concept.

## <a name="validate-template-deployment"></a>Valider le déploiement du modèle
commandes de ce compte de stockage et le groupe de ressources, hello utilisation suivant toosee :

    azure group list

    azure storage account list

## <a name="next-steps"></a>Étapes suivantes
[Gérer les autorisations utilisateur](azure-stack-manage-permissions.md)

