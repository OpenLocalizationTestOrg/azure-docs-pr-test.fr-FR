---
title: "fonctionnalités du Shell du Cloud (version préliminaire) aaaAzure | Documents Microsoft"
description: "Vue d’ensemble des fonctionnalités d’Azure Cloud Shell"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 65482ca6caeac01dda18a6b12eabe943e3d68a96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="features-and-tools-for-azure-cloud-shell"></a>Fonctionnalités et outils pour Azure Cloud Shell
Azure Cloud Shell est un toomanage d’expérience basée sur navigateur de shell et développer des ressources Azure.

Shell de cloud computing offre un navigateur accessible, préconfiguré expérience d’interpréteur de commandes pour la gestion des ressources Azure sans surcharge hello de l’installation, le contrôle de version et la gestion d’un ordinateur vous-même.

Cloud Shell approvisionne les machines à la demande ; par conséquent, leur état n’est pas persistant d’une session à l’autre. Cloud Shell étant conçu pour les sessions interactives, les shells s’arrêtent automatiquement après 20 minutes d’inactivité.

## <a name="bash-in-cloud-shell"></a>Bash dans Cloud Shell
### <a name="tools"></a>Outils
|Catégorie   |Nom   |
|---|---|
|Interpréteur de commandes Linux|Bash<br> sh               |
|Outils Azure            |[Azure CLI 2.0](https://github.com/Azure/azure-cli) et [1.0](https://github.com/Azure/azure-xplat-cli)<br> [AZCopy](https://docs.microsoft.com/azure/storage/storage-use-azcopy)<br> [Lot chantier](https://github.com/Azure/batch-shipyard)     |
|Éditeurs de texte           |vim<br> nano<br> emacs       |
|Contrôle de code source         |git                    |
|Outils de génération            |make<br> maven<br> npm<br> pip         |
|Conteneurs             |[Docker CLI](https://github.com/docker/cli)/[Docker Machine](https://github.com/docker/machine)<br> [Kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/)<br> [Draft](https://github.com/Azure/draft)<br> [CLI DC/OS](https://github.com/dcos/dcos-cli)         |
|Bases de données              |Client MySQL<br> Client PostgreSQL<br> [Utilitaire sqlcmd](https://docs.microsoft.com/sql/tools/sqlcmd-utility)<br> [mssql-scripter](https://github.com/Microsoft/sql-xplat-cli) |
|Autres                  |Client iPython<br> [CLI Cloud Foundry](https://github.com/cloudfoundry/cli)<br> |

### <a name="language-support"></a>Support multilingue
|language   |Version   |
|---|---|
|.NET       |1.01       |
|Go         |1.7        |
|Java       |1.8        |
|Node.js    |6.9.4      |
|Python     |2.7 et 3.5 (par défaut)|

## <a name="secure-automatic-authentication"></a>Authentification automatique sécurisée
Cloud Shell automatiquement et en toute sécurité authentifie l’accès de compte pour hello Azure CLI 2.0.

## <a name="azure-files-persistence"></a>Persistance Azure Files
Cloud Shell étant alloué à la demande à l’aide d’un ordinateur temporaire, les fichiers qui ne se trouvent pas dans $Home et l’état de l’ordinateur ne sont pas persistants d’une session à l’autre.
fichiers toopersist entre les sessions, vous guident dans l’attachement d’un fichier Azure partagez parcours de Cloud Shell sur le premier lancement.
Par la suite, Cloud Shell associera automatiquement votre espace de stockage pour toutes les sessions à venir.

[En savoir plus sur l’attachement de partages de fichiers Azure tooCloud Shell.](persisting-shell-storage.md)

## <a name="next-steps"></a>Étapes suivantes
[Démarrage rapide de Cloud Shell](quickstart.md) <br>
[En savoir plus sur Azure CLI 2.0](https://docs.microsoft.com/cli/azure/) <br>