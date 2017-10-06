---
title: "aaaCreate une passerelle d’Application Azure - modèles | Documents Microsoft"
description: "Cette page fournit des instructions toocreate une passerelle d’application Windows Azure à l’aide du modèle de gestionnaire de ressources Azure hello"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: fc18e553852551326d6a302abe2c7f8a08c2eb6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-resource-manager-template"></a>Créer une passerelle d’application à l’aide du modèle de gestionnaire de ressources Azure hello

> [!div class="op_single_selector"]
> * [Portail Azure](application-gateway-create-gateway-portal.md)
> * [Commandes PowerShell pour Azure Resource Manager](application-gateway-create-gateway-arm.md)
> * [Azure Classic PowerShell](application-gateway-create-gateway.md)
> * [Modèle Azure Resource Manager](application-gateway-create-gateway-arm-template.md)
> * [Interface de ligne de commande Azure](application-gateway-create-gateway-cli.md)

La passerelle Azure Application Gateway est un équilibreur de charge de couche 7. Il fournit de basculement et le routage des performances des requêtes HTTP entre différents serveurs, qu’ils soient sur le cloud de hello ou localement. Application Gateway offre de nombreuses fonctionnalités de contrôleur de livraison d’applications (ADC) : équilibrage de charge HTTP, affinité de session basée sur les cookies, déchargement SSL (Secure Sockets Layer), sondes d’intégrité personnalisées, prise en charge de plusieurs sites, etc. toofind une liste complète des fonctionnalités prises en charge, visitez [vue d’ensemble de la passerelle d’Application](application-gateway-introduction.md)

Cet article vous guide par le biais du téléchargement et modification d’un modèle Azure Resource Manager existant à partir de GitHub et le déploiement de modèle hello à partir de GitHub, PowerShell et hello CLI d’Azure.

Si vous déployez simplement modèle du Gestionnaire de ressources Azure hello directement à partir de GitHub sans aucune modification, ignorez toodeploy un modèle à partir de GitHub.

## <a name="scenario"></a>Scénario

Dans ce scénario, vous allez :

* créer une passerelle d’application avec le pare-feu d’applications web ;
* créer un réseau virtuel nommé VirtualNetwork1 avec un bloc CIDR réservé de 10.0.0.0/16 ;
* créer un sous-réseau appelé Appgatewaysubnet qui utilise 10.0.0.0/28 comme bloc CIDR ;
* Configurer deux adresses IP principale précédemment configurés pour les serveurs web hello souhaité tooload équilibrer hello du trafic. Dans cet exemple de modèle, hello principal des adresses IP sont 10.0.1.10 et 10.0.1.11.

> [!NOTE]
> Ces paramètres sont des paramètres de hello pour ce modèle. toocustomize modèle de hello, vous pouvez modifier les règles, port d’écoute hello, SSL et autres options dans le fichier de azuredeploy.json hello.

![Scénario](./media/application-gateway-create-gateway-arm-template/scenario.png)

## <a name="download-and-understand-hello-azure-resource-manager-template"></a>Télécharger et de comprendre le modèle de gestionnaire de ressources Azure hello

Vous pouvez télécharger hello existant Azure Resource Manager modèle toocreate un réseau virtuel et deux sous-réseaux à partir de GitHub, apporter des modifications que vous souhaitez et la réutiliser. toodo utilisez donc hello comme suit :

1. Accédez trop[créer une Application passerelle avec pare-feu d’applications web activé](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).
1. Cliquez sur **azuredeploy.json**, puis sur **RAW**.
1. Enregistrez le dossier local de hello fichier tooa sur votre ordinateur.
1. Si vous êtes familiarisé avec les modèles Azure Resource Manager, ignorez toostep 7.
1. Ouvrez le fichier hello que vous avez enregistré et examinez le contenu de hello sous **paramètres** en ligne
1. Les paramètres du modèle Azure Resource Manager fournissent un espace réservé pour les valeurs à remplir lors du déploiement.

  | Paramètre | Description |
  | --- | --- |
  | **subnetPrefix** |Bloc CIDR pour le sous-réseau de passerelle d’application hello. |
  | **applicationGatewaySize** | Taille de la passerelle d’application hello.  Le pare-feu d’applications web autorise uniquement les tailles moyenne et grande. |
  | **backendIpaddress1** |Adresse IP du premier serveur web de hello. |
  | **backendIpaddress2** |Adresse IP du serveur web de la deuxième hello. |
  | **wafEnabled** | La définition de toodetermine WAF est activé.|
  | **wafMode** | Mode de pare-feu d’applications web hello.  Les options disponibles sont **prévention** ou **détection**.|
  | **wafRuleSetType** | Type de groupe de règles du pare-feu d’applications web.  Actuellement OWASP avoir est hello pris en charge uniquement les option. |
  | **wafRuleSetVersion** |Version de groupe de règles. Options de hello pris en charge sont actuellement OWASP CRS 2.2.9 et 3.0. |

1. Vérifiez le contenu de hello sous **ressources** et avis hello les propriétés suivantes :

   * **type**. Type de ressource en cours de création par le modèle de hello. Dans ce cas, le type de hello est `Microsoft.Network/applicationGateways`, qui représente une passerelle d’application.
   * **name**. Nom de ressource de hello. Utilisation de hello avis de `[parameters('applicationGatewayName')]`, ce qui signifie que ce nom hello est fourni en tant qu’entrée par vous ou par un fichier de paramètres au cours du déploiement.
   * **properties**. Liste de propriétés pour la ressource de hello. Ce modèle utilise un réseau virtuel de hello et l’adresse IP publique lors de la création de passerelle d’application.

   > [!NOTE]
   > Pour plus d’informations sur les modèles, consultez [Référence sur les modèles Resource Manager](/templates/).

1. Naviguer vers l’arrière trop[https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).
1. Cliquez sur **azuredeploy-parameters.json**, puis sur **RAW**.
1. Enregistrez le dossier local de hello fichier tooa sur votre ordinateur.
1. Ouvrir le fichier hello que vous avez enregistré et modifier les valeurs hello pour les paramètres de hello. Utilisez hello suivant la passerelle d’application hello toodeploy valeurs décrite dans notre scénario.

    ```json
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "addressPrefix": {
            "value": "10.0.0.0/16"
            },
            "subnetPrefix": {
            "value": "10.0.0.0/28"
            },
            "applicationGatewaySize": {
            "value": "WAF_Medium"
            },
            "capacity": {
            "value": 2
            },
            "backendIpAddress1": {
            "value": "10.0.1.10"
            },
            "backendIpAddress2": {
            "value": "10.0.1.11"
            },
            "wafEnabled": {
            "value": true
            },
            "wafMode": {
            "value": "Detection"
            },
            "wafRuleSetType": {
            "value": "OWASP"
            },
            "wafRuleSetVersion": {
            "value": "3.0"
            }
        }
    }
    ```

1. Enregistrez le fichier de hello. Vous pouvez tester le modèle JSON hello et modèle de paramètre à l’aide des outils de validation JSON en ligne comme [JSlint.com](http://www.jslint.com/).

## <a name="deploy-hello-azure-resource-manager-template-by-using-powershell"></a>Déployer le modèle de hello Azure Resource Manager à l’aide de PowerShell

Si vous n’avez jamais utilisé Azure PowerShell, visitez : [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) et suivez hello instructions toosign dans Azure et sélectionnez votre abonnement.

1. Connexion tooPowerShell

    ```powershell
    Login-AzureRmAccount
    ```

1. Vérifiez les abonnements hello pour le compte de hello.

    ```powershell
    Get-AzureRmSubscription
    ```

    Vous êtes invité à tooauthenticate avec vos informations d’identification.

1. Choisissez parmi vos toouse abonnements Azure.

    ```powershell
    Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
    ```

1. Si nécessaire, créez un groupe de ressources à l’aide de hello **New-AzureResourceGroup** applet de commande. Bonjour l’exemple suivant, vous créez un groupe de ressources appelé AppgatewayRG dans l’emplacement de l’est des États-Unis.

    ```powershell
    New-AzureRmResourceGroup -Name AppgatewayRG -Location "West US"
    ```

1. Exécutez hello **New-AzureRmResourceGroupDeployment** applet de commande toodeploy hello nouveau réseau virtuel à l’aide de hello précédant les fichiers de modèle et les paramètres vous avez téléchargé et modifié.
    
    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestAppgatewayDeployment -ResourceGroupName AppgatewayRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-hello-azure-cli"></a>Déploiement de modèle de gestionnaire de ressources Azure hello à l’aide de hello CLI d’Azure

modèle de gestionnaire de ressources Azure hello toodeploy vous avez téléchargé à l’aide de CLI d’Azure, suivez hello comme suit :

1. Si vous n’avez jamais utilisé CLI d’Azure, consultez [installer et configurer hello CLI d’Azure](/cli/azure/install-azure-cli) et suivez les instructions de hello point toohello où vous sélectionnez votre compte Azure et votre abonnement.

1. Si nécessaire, hello exécution `az group create` commande toocreate un groupe de ressources, comme indiqué dans hello suivant extrait de code. Notez la sortie hello de commande hello. liste de Hello affiché après la sortie de hello explique paramètres hello utilisés. Pour plus d’informations sur les groupes de ressources, consultez la page [Vue d’ensemble d’Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

    ```azurecli
    az group create --location westus --name appgatewayRG
    ```
    
    **-n (ou --name)**. Nom du nouveau groupe de ressources hello. Pour notre scénario, il s’agit de *appgatewayRG*.
    
    **-l (ou --location)**. Région Azure où le nouveau groupe de ressources hello est créé. Pour notre scénario, il s’agit de *westus*.

1. Exécutez hello `az group deployment create` applet de commande toodeploy hello nouveau réseau virtuel à l’aide des paramètres et modèle de hello fichiers vous téléchargé et modifié dans hello précédant l’étape. liste de Hello affiché après la sortie de hello explique paramètres hello utilisés.

    ```azurecli
    az group deployment create --resource-group appgatewayRG --name TestAppgatewayDeployment --template-file azuredeploy.json --parameters @azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-click-to-deploy"></a>Déployer le modèle de gestionnaire de ressources Azure de hello à l’aide de clic sur le déploiement

Cliquez sur le déploiement est un autre moyen toouse modèles Azure Resource Manager. Il s’agit de des modèles de toouse facilement avec hello portail Azure.

1. Accédez trop[créer une passerelle d’application avec le pare-feu d’applications web](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).

1. Cliquez sur **déployer tooAzure**.

    ![Déployer tooAzure](./media/application-gateway-create-gateway-arm-template/deploytoazure.png)
    
1. Renseignez les paramètres hello hello modèle de déploiement sur le portail hello et cliquez sur **OK**.

    ![Paramètres](./media/application-gateway-create-gateway-arm-template/ibiza1.png)
    
1. Sélectionnez **J’accepte les conditions susmentionnées générales toohello** et cliquez sur **bon**.

1. Dans le panneau de déploiement personnalisée hello, cliquez sur **créer**.

## <a name="providing-certificate-data-tooresource-manager-templates"></a>Fournissant des certificats données tooResource Gestionnaire de modèles

Lors de l’utilisation de SSL avec un modèle de certificat de hello doit toobe fourni dans une chaîne base64, au lieu d’en cours de téléchargement. tooconvert base64 tooa .pfx ou .cer chaîne utilisez hello suivant les commandes. Hello les commandes suivantes convertissent hello certificat tooa chaîne base64, qui peut être fourni toohello modèle. Hello attendu la sortie est une chaîne qui peut être stockée dans une variable et collée dans le modèle de hello.

### <a name="macos"></a>macOS
```bash
cert=$( base64 <certificate path and name>.pfx )
echo $cert
```

### <a name="windows"></a>Windows
```powershell
[System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("<certificate path and name>.pfx"))
```

## <a name="delete-all-resources"></a>Supprimer toutes les ressources

toodelete toutes les ressources créées dans cet article, effectuez l’une de hello comme suit :

### <a name="powershell"></a>PowerShell

```powershell
Remove-AzureRmResourceGroup -Name appgatewayRG
```

### <a name="azure-cli"></a>Interface de ligne de commande Azure

```azurecli
az group delete --name appgatewayRG
```

## <a name="next-steps"></a>Étapes suivantes

Si vous souhaitez tooconfigure le déchargement SSL, visitez : [configurer une passerelle d’application pour le déchargement SSL](application-gateway-ssl.md).

Si vous voulez tooconfigure un toouse de passerelle d’application avec un équilibrage de charge interne, visitez : [créer une passerelle d’application avec un équilibreur de charge interne (ILB)](application-gateway-ilb.md).

Si vous souhaitez plus d’informations sur les options d’équilibrage de charge en général, visitez :

* [Équilibrage de charge Azure](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

