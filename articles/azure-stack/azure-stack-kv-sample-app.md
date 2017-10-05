---
title: "Autoriser l’application à récupérer les secrets d’un coffre de clés dans Azure Stack | Microsoft Docs"
description: "Utiliser un exemple d’application à utiliser avec Azure Stack Key Vault"
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
ms.openlocfilehash: 4b517526d89e7f6c2649e2f12810b4db705defa3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="run-the-sample-application-for-key-vault"></a>Exécutez l’exemple d’application pour le coffre de clés

Dans ce guide, vous utiliserez un exemple d’application pour extraire les secrets et des mots de passe à partir du coffre de clés.

## <a name="download-the-samples-and-prepare"></a>Télécharger les exemples et préparer
Télécharger les exemples de client Azure Key Vault à partir de la [page d’exemples de client Azure Key Vault](https://www.microsoft.com/en-us/download/details.aspx?id=45343).

Extrayez le contenu du fichier .zip sur votre ordinateur local.

Lecture la **README.md** fichier (il s’agit d’un fichier texte), puis suivez les instructions.

## <a name="run-sample-1--hellokeyvault"></a>Exécuter l’exemple #1--HelloKeyVault
HelloKeyVault est une application console qui vous guide à travers les scénarios clés qui sont prises en charge par le coffre de clés :

1. Créer et d’importation d’une clé (clé de module de sécurité matériel ou logiciel)
2. Chiffrer une clé secrète à l’aide d’une clé de contenu
3. Encapsuler la clé de contenu à l’aide d’une clé de coffre de clés
4. Désencapsuler la clé de contenu
5. Déchiffrer la clé secrète
6. Définir une clé secrète

Cette application de console doit s’exécuter sans modification, à ceci près que les paramètres de configuration appropriés dans App.Config seront mise à jour après les étapes suivantes :

1. Mettre à jour les paramètres de configuration d’application dans HelloKeyVault\App.config avec votre URL du coffre, un ID d’application principal et un secret. Les informations peuvent également être générées à l’aide de **scripts\GetAppConfigSettings.ps1**.
2. Mettre à jour les valeurs des variables obligatoires dans GetAppConfigSettings.ps1.
3. Lancez la fenêtre Windows PowerShell.
4. Dans la fenêtre PowerShell, exécutez le script GetAppConfigSettings.ps1.
5. Copier les résultats du script dans le fichier HelloKeyVault\App.config.

## <a name="next-steps"></a>Étapes suivantes
[Déployer une machine virtuelle avec un mot de passe Key Vault](azure-stack-kv-deploy-vm-with-secret.md)

[Déployer une machine virtuelle avec un certificat Key Vault](azure-stack-kv-push-secret-into-vm.md)

