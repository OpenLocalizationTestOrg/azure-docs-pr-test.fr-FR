---
title: "les secrets de coffre de clés Azure pile aaaAllow application tooretrieve | Documents Microsoft"
description: "Utiliser un toowork d’application exemple avec la pile d’Azure Key Vault"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 3748b719-e269-4b48-8d7d-d75a84b0e1e5
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/04/2017
ms.author: sngun
ms.openlocfilehash: 2ff3f0bab86d9d1934b463f72124863d29dbe696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-sample-application-for-key-vault"></a>Exécutez l’exemple d’application hello pour le coffre de clés

Dans ce guide, vous allez utiliser un tooretrieve d’application exemple secrets et des mots de passe à partir du coffre de clés.

## <a name="download-hello-samples-and-prepare"></a>Télécharger les exemples hello et préparer
Télécharger des exemples de client de coffre de clés Azure hello de hello [page d’exemples de client Azure Key Vault](https://www.microsoft.com/en-us/download/details.aspx?id=45343).

Extrayez le contenu hello de l’ordinateur local du tooyour fichier .zip hello.

Hello de lecture **README.md** fichier (il s’agit d’un fichier texte), puis suivez les instructions de hello.

## <a name="run-sample-1--hellokeyvault"></a>Exécuter l’exemple #1--HelloKeyVault
HelloKeyVault est une application console qui vous guide à travers les scénarios clés hello qui sont pris en charge par le coffre de clés :

1. Créer et d’importation d’une clé (clé de module de sécurité matériel ou logiciel)
2. Chiffrer une clé secrète à l’aide d’une clé de contenu
3. Encapsuler la clé de contenu hello à l’aide d’une clé de coffre de clés
4. Désencapsuler la clé de contenu hello
5. Déchiffrer un secret de hello
6. Définir une clé secrète

Cette application de console doit s’exécuter sans modification, à ceci près que les paramètres de configuration appropriés hello dans App.Config seront mise à jour en fonction de toohello comme suit :

1. Mettre à jour les paramètres de configuration d’application hello dans HelloKeyVault\App.config avec votre URL du coffre, un ID d’application principal et un secret. informations de Hello peuvent également être générées à l’aide de **scripts\GetAppConfigSettings.ps1**.
2. Mettre à jour les valeurs hello des variables obligatoire de hello dans GetAppConfigSettings.ps1.
3. Lancez la fenêtre Windows PowerShell de hello.
4. Exécutez le script de GetAppConfigSettings.ps1 de hello dans la fenêtre de PowerShell hello.
5. Copier les résultats hello hello toohello HelloKeyVault\App.config du fichier de script.

## <a name="next-steps"></a>Étapes suivantes
[Déployer une machine virtuelle avec un mot de passe Key Vault](azure-stack-kv-deploy-vm-with-secret.md)

[Déployer une machine virtuelle avec un certificat Key Vault](azure-stack-kv-push-secret-into-vm.md)

