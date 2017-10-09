---
title: "aaaConfiguring et à l’aide de hello l’émulateur de stockage avec Visual Studio | Documents Microsoft"
description: "Configuration et l’utilisation de l’émulateur de stockage de hello avec Visual Studio"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: c8e7996f-6027-4762-806e-614b93131867
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/17/2017
ms.author: kraigb
ms.openlocfilehash: d590f21146c86bcb7bfa6b6164b92c6df5938d5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-and-using-hello-storage-emulator-with-visual-studio"></a>Configuration et l’utilisation de l’émulateur de stockage de hello avec Visual Studio
[!INCLUDE [storage-try-azure-tools](../includes/storage-try-azure-tools.md)]

## <a name="overview"></a>Vue d'ensemble
environnement de développement Azure SDK Hello inclut un utilitaire qui simule hello Blob, file d’attente et Table de services de stockage disponibles dans Azure sur votre ordinateur de développement local, émulateur de stockage hello. Si vous ne générez un service cloud qui utilise les services de stockage Azure hello ou écrivez une application externe que les appels hello des services de stockage, vous pouvez tester localement votre code sur l’émulateur de stockage hello. Bonjour Azure Tools pour Microsoft Visual Studio intégrer la gestion de l’émulateur de stockage hello dans Visual Studio. Bonjour Azure Tools initialiser la base de données émulateur de stockage hello lors de la première utilisation, démarre hello service émulateur de stockage lorsque vous exécutez ou déboguez votre code à partir de Visual Studio et fournit des données d’émulateur de stockage d’accès en lecture seule toohello via hello Explorateur de stockage Azure.

Pour plus d’informations sur l’émulateur de stockage hello, y compris la configuration système requise et les instructions de configuration personnalisée, consultez [hello d’utilisation émulateur de stockage pour le développement et le test](storage/common/storage-use-emulator.md).

> [!NOTE]
> Il existe quelques différences de fonctionnalités entre la simulation de l’émulateur hello stockage et les services de stockage Azure hello. Consultez [hello différences entre l’émulateur de stockage et les Services de stockage Azure](storage/common/storage-use-emulator.md) Bonjour documentation du SDK Azure pour plus d’informations sur les différences spécifiques hello.
> 
> 

## <a name="configuring-a-connection-string-for-hello-storage-emulator"></a>Configuration d’une chaîne de connexion pour l’émulateur de stockage hello
émulateur de stockage tooaccess hello depuis du code dans un rôle, vous pouvez tooconfigure une connexion de chaîne que l’émulateur de stockage toohello points et qui pourront ensuite être modifiés toopoint tooan compte de stockage Azure. Une chaîne de connexion est un paramètre de configuration que votre rôle peut lire à partir du compte de stockage runtime tooconnect tooa. Pour plus d’informations sur la façon toocreate les chaînes de connexion, consultez [hello de configuration d’Application Azure](https://msdn.microsoft.com/library/azure/2da5d6ce-f74d-45a9-bf6b-b3a60c5ef74e#BK_SettingsPage).

> [!NOTE]
> Vous pouvez retourner un compte d’émulateur de stockage référence toohello à partir de votre code à l’aide de hello **DevelopmentStorageAccount** propriété. Cette approche fonctionne correctement si vous souhaitez tooaccess hello émulateur de stockage à partir de votre code, mais si vous envisagez de toopublish tooAzure de votre application, vous devez toocreate un tooaccess de chaîne de connexion à votre compte de stockage Azure et modifier votre code toouse qui chaîne de connexion avant de le publier. Si vous basculez entre le compte d’émulateur de stockage hello et un compte de stockage Azure fréquemment, une chaîne de connexion simplifiera ce processus.
> 
> 

## <a name="initializing-and-running-hello-storage-emulator"></a>Initialisation et exécution de l’émulateur de stockage hello
Vous pouvez spécifier que lorsque vous exécutez ou déboguez votre service dans Visual Studio, Visual Studio lance automatiquement l’émulateur de stockage hello. Dans l’Explorateur de solutions, ouvrez le menu contextuel hello votre **Azure** de projet et choisissez **propriétés**. Sur hello **développement** onglet hello **démarrer l’émulateur de stockage Azure** , choisissez **True** (s’il n’est pas déjà toothat valeur).

Hello la première fois que vous exécutez ou déboguez votre service à partir de Visual Studio, l’émulateur de stockage hello lance un processus d’initialisation. Ce processus réserve des ports locaux pour l’émulateur de stockage hello et crée la base de données émulateur de stockage hello. Une fois terminé, ce processus ne doit pas toorun à nouveau à moins que la base de données émulateur de stockage hello est supprimé.

> [!NOTE]
> À compter de version de juin 2012 hello Hello Azure Tools, l’émulateur de stockage hello s’exécute, par défaut, dans SQL Express LocalDB. Dans les versions antérieures de Windows Azure Tools de hello, émulateur de stockage hello s’exécute sur une instance par défaut de SQL Express 2005 ou 2008, que vous devez installer avant que vous pouvez installer hello Azure SDK. Vous pouvez également exécuter l’émulateur de stockage hello sur une instance nommée de SQL Express ou un jeu nommé ou une instance par défaut de Microsoft SQL Server. Si vous devez tooconfigure hello stockage émulateur toorun par rapport à une instance autre que de l’instance par défaut de hello, consultez [hello d’utilisation émulateur de stockage pour le développement et le test](storage/common/storage-use-emulator.md).
> 
> 

l’émulateur de stockage Hello indique l’état utilisateur interface tooview hello de services de stockage local hello et toostart, arrêter et les réinitialiser. Une fois que le service de l’émulateur hello stockage a été démarré, vous pouvez afficher l’interface utilisateur hello démarrer ou arrêter le service en cliquant sur icône de zone de notification de hello pour hello hello émulateur Microsoft Azure dans la barre des tâches de Windows hello.

## <a name="viewing-storage-emulator-data-in-server-explorer"></a>Affichage des données de l’émulateur de stockage dans l’Explorateur de serveurs
le nœud de stockage Azure Hello dans l’Explorateur de serveurs vous tooview données et modifier les paramètres pour l’objet blob et des données de table dans vos comptes de stockage, y compris hello émulateur de stockage. Consultez [Gérer les ressources Stockage Blob Azure avec l’explorateur de stockage (préversion)](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs) pour plus d’informations.

