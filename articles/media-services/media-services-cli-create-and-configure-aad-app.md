---
title: aaaUse CLI 2.0 toocreate une application Azure AD et configurez-le tooaccess API Azure Media Services | Documents Microsoft
description: Cette rubrique montre comment toouse CLI 2.0 toocreate une application Azure AD et configurez-le tooaccess API Azure Media Services.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: c865e2701722374b5dd17b0e20fa848c07065006
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-20-toocreate-an-aad-app-and-configure-it-tooaccess-azure-media-services-api"></a>Utilisez CLI 2.0 toocreate une application AAD et configurez-le tooaccess API Azure Media Services

Cette rubrique vous montre comment toouse CLI 2.0 toocreate une application Azure Active Directory (Azure AD) tooaccess principal du service Azure Media Services et ressources. 

## <a name="prerequisites"></a>Composants requis

- Un compte Azure. Pour plus d’informations, consultez la page [Version d’évaluation gratuite d’Azure](https://azure.microsoft.com/pricing/free-trial/). 
- Un compte Media Services. Pour plus d’informations, consultez [créer un compte Azure Media Services à l’aide de hello Azure portal](media-services-portal-create-account.md).

## <a name="use-hello-azure-cloud-shell"></a>Utilisez hello Azure Cloud Shell

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Lancez hello Cloud Shell à partir du volet de navigation supérieur hello du portail de hello.

    ![Cloud Shell](./media/media-services-cli-create-and-configure-aad-app/media-services-cli-create-and-configure-aad-app01.png) 

Pour plus d’informations, voir la [présentation d’Azure Cloud Shell](../cloud-shell/overview.md).

## <a name="create-an-azure-ad-app-and-configure-access-toohello-media-account-with-cli-20"></a>Créer une application Azure AD et configurer le compte d’accès toohello media avec CLI 2.0
 
```azurecli
az login
az ad sp create-for-rbac --name <appName> --password <strong password>
az role assignment create -- assignee < user/app id> --role Contributor --scope <subscription/subscription id>
```

Par exemple :

```azurecli
az role assignment create --assignee a3e068fa-f739-44e5-ba4d-ad57866e25a1 --role Contributor --scope /subscriptions/0b65e280-7917-4874-9fed-1307f2615ea2/resourceGroups/Default-AzureBatch-SouthCentralUS/providers/microsoft.media/mediaservices/sbbash
```

Dans cet exemple, hello **étendue** est chemin d’accès de ressource complet hello pour les médias de hello compte des services. Toutefois, hello **étendue** peut être n’importe quel niveau.

Par exemple, cela peut être un des hello suivant les niveaux :
 
* Hello **abonnement** niveau.
* Hello **groupe de ressources** niveau.
* Hello **ressource** niveau (par exemple, un compte de support).

Pour plus d’informations, voir [Créer un principal du service avec Azure CLI 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli).

Consultez également [Manage Role-Based le contrôle d’accès avec hello interface de ligne de commande Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md). 

## <a name="next-steps"></a>Étapes suivantes

Prise en main [téléchargement de fichiers tooyour compte](media-services-portal-upload-files.md).
