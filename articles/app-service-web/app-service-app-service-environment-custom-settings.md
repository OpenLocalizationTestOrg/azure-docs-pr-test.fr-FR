---
title: "paramètres d’aaaCustom pour les environnements de Service d’application"
description: "Paramètres de configuration personnalisés pour les environnements App Service"
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 1d1d85f3-6cc6-4d57-ae1a-5b37c642d812
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: stefsch
ms.openlocfilehash: 3d140688c88b389e71bfdd465c418339cccab3a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-configuration-settings-for-app-service-environments"></a>Paramètres de configuration personnalisés pour les environnements App Service
## <a name="overview"></a>Vue d'ensemble
Environnements de Service d’application étant tooa isolé un seul client, il existe certains des paramètres de configuration qui peuvent être appliqués tooApp exclusivement les environnements de Service. Ce article les documents hello différentes personnalisations spécifiques qui sont disponibles pour les environnements de Service d’application.

Si vous n’avez pas d’un environnement App Service, consultez [comment tooCreate un environnement App Service](app-service-web-how-to-create-an-app-service-environment.md).

Vous pouvez stocker les personnalisations de l’environnement App Service en utilisant un tableau Bonjour nouvelle **clusterSettings** attribut. Cet attribut est trouvé dans le dictionnaire de « Propriétés » hello Hello *hostingEnvironments* entité d’Azure Resource Manager.

Hello abrégé Gestionnaire de ressources du modèle extrait de code suivant montre hello **clusterSettings** attribut :

    "resources": [
    {
       "apiVersion": "2015-08-01",
       "type": "Microsoft.Web/hostingEnvironments",
       "name": ...,
       "location": ...,
       "properties": {
          "clusterSettings": [
             {
                 "name": "nameOfCustomSetting",
                 "value": "valueOfCustomSetting"
             }
          ],
          "workerPools": [ ...],
          etc...
       }
    }

Hello **clusterSettings** attribut peut être inclus dans un Bonjour de tooupdate de modèle de gestionnaire de ressources environnement App Service.

## <a name="use-azure-resource-explorer-tooupdate-an-app-service-environment"></a>Utilisez l’Explorateur de ressources Azure tooupdate un environnement App Service
Ou bien, vous pouvez mettre à jour hello environnement App Service à l’aide de [Explorateur de ressources Azure](https://resources.azure.com).  

1. Dans l’Explorateur de ressources, accédez au nœud toohello hello environnement App Service (**abonnements** > **resourceGroups** > **fournisseurs**  >  **Microsoft.Web** > **hostingEnvironments**). Puis cliquez sur hello environnement App Service spécifique que vous souhaitez tooupdate.
2. Dans le volet droit de hello, cliquez sur **en lecture/écriture** dans tooallow de barre d’outils supérieure hello interactif de modification dans l’Explorateur de ressources.  
3. Cliquez sur hello bleu **modifier** modifiable de modèle de gestionnaire de ressources du hello toomake bouton.
4. Défilement vers le bas toohello du volet de droite hello. Hello **clusterSettings** attribut est à hello tout en bas, où vous pouvez entrer ou mettre à jour sa valeur.
5. Tableau de hello type (ou copier et coller) de valeurs de configuration souhaitée dans hello **clusterSettings** attribut.  
6. Cliquez sur hello verte **PUT** bouton qui est située en haut de hello de hello volet droit toocommit hello modification toohello environnement App Service.

Toutefois, vous envoyez la modification de hello, dure environ 30 minutes pour multiplié par nombre de hello de frontaux Bonjour environnement App Service pour modifier un effet de tootake hello.
Par exemple, si un environnement App Service a quatre frontaux, il prendra environ deux heures pour toofinish de mise à jour de configuration hello. Lors de la modification de la configuration hello est déployée, aucune autre mise à l’échelle des opérations ou des opérations de modification de configuration ne peuvent avoir lieu dans hello environnement App Service.

## <a name="disable-tls-10"></a>Désactivation de TLS 1.0
Une question récurrente de clients, notamment les clients qui traitent avec mise en conformité PCI audits, est comment tooexplicitly désactiver TLS 1.0 pour leurs applications.

TLS 1.0 peut être désactivé via les éléments suivants de hello **clusterSettings** entrée :

        "clusterSettings": [
            {
                "name": "DisableTls1.0",
                "value": "1"
            }
        ],

## <a name="change-tls-cipher-suite-order"></a>Modifier l’ordre des suites de chiffrement TLS
Une autre question à partir de clients est si ils peuvent modifier la liste de hello de chiffrements négocié par leur serveur et que cela est possible en modifiant hello **clusterSettings** comme indiqué ci-dessous. liste de Hello des suites de chiffrement disponibles peut être récupérée à partir de [cet article MSDN](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).

        "clusterSettings": [
            {
                "name": "FrontEndSSLCipherSuiteOrder",
                "value": "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384_P256,TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA_P256"
            }
        ],

> [!WARNING]
> Si des valeurs incorrectes sont définies pour la suite de chiffrement de hello SChannel ne peut pas comprendre, tous les serveurs de tooyour communication TLS peuvent cesser de fonctionner. Dans ce cas, vous devez tooremove hello *FrontEndSSLCipherSuiteOrder* entrée à partir de **clusterSettings** et envoyer hello mis à jour le Gestionnaire de ressources du modèle toorevert toohello différé par défaut chiffrement paramètres de la suite.  Utilisez cette fonctionnalité avec précaution.
> 
> 

## <a name="get-started"></a>Prise en main
site de modèle de gestionnaire de ressources du démarrage rapide Azure Hello comprend un modèle avec la définition de base hello pour [création d’un environnement App Service](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).

<!-- LINKS -->

<!-- IMAGES -->
