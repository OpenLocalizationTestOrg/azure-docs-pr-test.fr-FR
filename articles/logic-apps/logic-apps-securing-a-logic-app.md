---
title: "aaaSecure accéder aux applications de la logique de tooAzure | Documents Microsoft"
description: "Ajoutez la sécurité pour la protection d’accès tootriggers, entrées et sorties, paramètres d’action et services utilisés avec les flux de travail dans Azure Logic Apps."
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 11/22/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: abda2179e4cc2d2295cd8332ec017c848a456264
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-access-tooyour-logic-apps"></a>Sécuriser l’accès aux applications de la logique de tooyour

Il existe des nombreux toohelp disponible outils vous sécurisez votre application logique.

* Sécurisation des accès tootrigger une logique d’application (déclencheur de demande HTTP)
* Sécurisation des accès toomanage, modifier, ou une application de la logique de lecture
* Sécurisation de toocontents d’accès d’entrées et sorties pour une exécution
* Sécurisation des paramètres ou des entrées dans des actions d’un flux de travail
* Sécurisation des accès tooservices qui reçoivent des requêtes à partir d’un flux de travail

## <a name="secure-access-tootrigger"></a>Sécuriser l’accès tootrigger

Lorsque vous travaillez avec une application de la logique qui se déclenche sur une requête HTTP ([demande](../connectors/connectors-native-reqres.md) ou [Webhook](../connectors/connectors-native-webhook.md)), vous pouvez restreindre l’accès afin que seuls les clients autorisés peuvent déclencher l’application logique de hello. Toutes les requêtes dans une application logique sont chiffrées et sécurisées via SSL.

### <a name="shared-access-signature"></a>Signature d’accès partagé

Chaque point de terminaison de demande pour une application logique inclut un [Signature d’accès partagé (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) dans le cadre de l’URL de hello. Chaque URL contient un paramètre de requête `sp`, `sv` et `sig`. Les autorisations sont spécifiées par `sp`, et elles correspondent à des méthodes tooHTTP autorisées, `sv` est hello version utilisée toogenerate, et `sig` est tootrigger d’accès tooauthenticate utilisé. signature de Hello est généré à l’aide d’algorithme de hello SHA256 avec une clé secrète sur tous les chemins d’accès des URL hello et propriétés. clé secrète de Hello n’est jamais exposée et publiée et sont chiffrées et stockées dans le cadre de l’application logique de hello. Votre application logique autorise uniquement les déclencheurs qui contiennent une signature valide créée avec une clé secrète hello.

#### <a name="regenerate-access-keys"></a>Régénération de clés d'accès

Vous pouvez régénérer une clé sécurisée au niveau à tout moment via le portail d’API REST ou Azure hello. Toutes les URL actuelles qui ont été créés précédemment à l’aide de la clé d’anciens hello sont application logique de hello toofire invalidé et ne sont plus autorisés.

1. Bonjour portail Azure, ouvrez hello logique application tooregenerate une clé
1. Cliquez sur hello **clés d’accès** élément de menu sous **paramètres**
1. Choisissez tooregenerate de clé hello et processus de hello terminée

Après la régénération de récupérer les URL sont signés avec la nouvelle clé d’accès hello.

#### <a name="creating-callback-urls-with-an-expiration-date"></a>Création d’URL de rappel avec une date d’expiration

Si vous partagez avec d’autres parties hello URL, vous pouvez générer des URL avec des clés spécifiques et les dates d’expiration en fonction des besoins. Vous pouvez accéder en toute transparence substituer les clés, ou vérifiez toofire d’accès à une application est restreint tooa certaine timespan. Vous pouvez spécifier une date d’expiration pour une URL via hello [logique applications API REST](https://docs.microsoft.com/rest/api/logic/workflowtriggers):

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

Dans le corps de hello, inclure la propriété de hello `NotAfter` comme une chaîne de date JSON, qui retourne une URL de rappel qui est uniquement valide jusqu'à hello `NotAfter` date et heure.

#### <a name="creating-urls-with-primary-or-secondary-secret-key"></a>Création d’URL avec une clé de secret principale ou secondaire

Lorsque vous générez ou répertoriez les URL de rappel pour les déclencheurs de demande de, vous pouvez également spécifier des URL hello toosign toouse clé.  Vous pouvez générer une URL signée par une clé spécifique via hello [logique applications API REST](https://docs.microsoft.com/rest/api/logic/workflowtriggers) comme suit :

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

Dans le corps de hello, inclure la propriété de hello `KeyType` en tant que `Primary` ou `Secondary`.  Cela retourne une URL signée par hello de clé sécurisée spécifiée.

### <a name="restrict-incoming-ip-addresses"></a>Limiter les adresses IP entrantes

En outre toohello Signature d’accès partagé, vous pouvez toorestrict appelant une application logique uniquement à partir de clients spécifiques.  Par exemple, si vous gérez votre point de terminaison via la gestion des API Azure, vous pouvez limiter la logique de hello application tooonly accepter la demande de hello lors de la demande de hello provient hello adresse IP d’instance gestion des API.

Ce paramètre peut être configuré dans les paramètres de l’application hello logique :

1. Bonjour portail Azure, ouvrez hello logique application tooadd restrictions par adresse IP
1. Cliquez sur hello **configuration de contrôle d’accès** élément de menu sous **paramètres**
1. Spécifiez la liste hello de toobe de plages d’adresses IP accepté par le déclencheur de hello

Une plage IP valide prend le format de hello `192.168.1.1/255`. Si vous souhaitez hello logique application tooonly incendie comme application logique imbriquées, sélectionnez hello **seulement d’autres applications logique** option. Cette option écrit une ressource de toohello tableau vide, ce qui signifie que seuls les appels à partir de hello service proprement dit (applications de logique parent) incendie avec succès.

> [!NOTE]
> Vous pouvez toujours exécuter une application logique avec un déclencheur de la demande via l’API REST de hello / gestion `/triggers/{triggerName}/run` , quelle que soit l’IP. Ce scénario requiert une authentification par rapport à hello API REST Azure, et tous les événements apparaît dans les journaux d’Audit Azure de hello. Définissez les stratégies de contrôle d’accès en conséquence.

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a>Définition de plages d’adresses IP sur la définition de ressource hello

Si vous utilisez un [modèle de déploiement](logic-apps-create-deploy-template.md) tooautomate vos déploiements, les paramètres des plages IP hello peuvent être configurés sur le modèle de ressource hello.  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "triggers": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}

```

### <a name="adding-azure-active-directory-oauth-or-other-security"></a>Ajout d’Azure Active Directory, d’OAuth ou d’une autre sécurité

tooadd d’autorisation de plusieurs protocoles sur une application logique, [gestion des API Azure](https://azure.microsoft.com/services/api-management/) offre riche analyse, sécurité, la stratégie et documentation pour n’importe quel point de terminaison avec hello fonctionnalité tooexpose une application logique en tant qu’une API. Gestion des API Azure peuvent exposer un point de terminaison public ou privé pour l’application hello logique, pouvant utiliser Azure Active Directory, certificat, OAuth ou autres normes de sécurité. Lorsqu’une demande est reçue, gestion des API Azure transfère hello demande toohello logique application (exécution de toutes les transformations nécessaires ou les restrictions en cours). Vous pouvez utiliser la plage IP entrant de hello paramètres hello logique application tooonly autorisent hello logique application toobe déclenchée à partir de la gestion des API.

## <a name="secure-access-toomanage-or-edit-logic-apps"></a>Sécuriser l’accès aux applications de logique toomanage ou modifier

Vous pouvez limiter les opérations d’accès toomanagement sur une logique d’application afin que seuls des utilisateurs ou groupes soient tooperform en mesure des opérations sur les ressources hello. Les applications de logique utilisent hello Azure [contrôle d’accès en fonction du rôle (RBAC)](../active-directory/role-based-access-control-configure.md) fonctionnalité et peut être personnalisée avec hello mêmes outils.  Il existe quelques rôles intégrés, que vous pouvez affecter des membres de votre abonnement de tooas bien :

* **Collaboration d’application logique** -fournit l’accès tooview, modifier et mettre à jour une application logique.  Impossible de supprimer la ressource de hello ou effectuer des opérations d’administration.
* **Opérateur d’application logique** : peut afficher l’application logique de hello et l’historique d’exécution et activer ou désactiver.  Impossible de modifier ou de mettre à jour de définition de hello.

Vous pouvez également utiliser [verrou de ressource Azure](../azure-resource-manager/resource-group-lock-resources.md) tooprevent changement ou suppression d’applications de la logique. Cette fonctionnalité est tooprevent précieuses ressources de production à partir de la modification ou suppression.

## <a name="secure-access-toocontents-of-hello-run-history"></a>Toocontents de sécuriser l’accès de l’historique d’exécution de hello

Vous pouvez limiter toocontents d’accès de l’entrée ni sortie à partir de précédentes plages d’adresses IP toospecific s’exécute.  

Toutes les données de l’exécution d’un flux de travail sont chiffrées pendant le transit et au repos. Lors de l’appel toorun historique, service de hello authentifie hello demande et fournit des liens toohello demande et les entrées de la réponse et les sorties. Ce lien peut être protégé par conséquent, seules les demandes tooview le contenu à partir d’une plage d’adresses IP désigné retourner le contenu de hello. Vous pouvez utiliser cette fonctionnalité pour obtenir un contrôle d’accès supplémentaire. Vous pouvez également spécifier une adresse IP telle que `0.0.0.0` afin que personne ne puisse accéder aux entrées/sorties. Seule une personne disposant d’autorisations d’administrateur a supprimer cette restriction, en fournissant la possibilité de hello pour le contenu tooworkflow d’accès de « juste-à-temps ».

Ce paramètre peut être configuré dans les paramètres de ressource hello Hello portail Azure :

1. Bonjour portail Azure, ouvrez hello logique application tooadd restrictions par adresse IP
1. Cliquez sur hello **configuration de contrôle d’accès** élément de menu sous **paramètres**
1. Spécifiez la liste hello de plages d’adresses IP pour un accès toocontent

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a>Définition de plages d’adresses IP sur la définition de ressource hello

Si vous utilisez un [modèle de déploiement](logic-apps-create-deploy-template.md) tooautomate vos déploiements, les paramètres des plages IP hello peuvent être configurés sur le modèle de ressource hello.  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "contents": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}
```

## <a name="secure-parameters-and-inputs-within-a-workflow"></a>Sécuriser les paramètres et les entrées dans un flux de travail

Vous pourriez tooparameterize certains aspects d’une définition de flux de travail pour le déploiement dans des environnements. En outre, certains paramètres peuvent être des paramètres sécurisés, vous ne souhaitez pas tooappear lors de la modification d’un flux de travail, telles qu’un ID client et la clé secrète du client pour [l’authentification Azure Active Directory](../connectors/connectors-native-http.md#authentication) d’une action HTTP.

### <a name="using-parameters-and-secure-parameters"></a>Utilisation des paramètres et des paramètres sécurisés

hello tooaccess hello valeur d’un paramètre de ressource lors de l’exécution, [langage de définition de flux de travail](http://aka.ms/logicappsdocs) fournit une `@parameters()` opération. En outre, vous pouvez [spécifier les paramètres de modèle de déploiement de ressources hello](../azure-resource-manager/resource-group-authoring-templates.md#parameters). Mais si vous spécifiez le type de paramètre hello en tant que `securestring`, paramètre hello ne sera pas renvoyée avec rest hello de définition de ressource hello et ne seront pas accessible en consultant les ressources hello après le déploiement.

> [!NOTE]
> Si votre paramètre est utilisé dans les en-têtes de hello ou de corps d’une requête, le paramètre hello peut être visible en accédant à l’historique de hello exécuter et de la demande HTTP sortante. Assurez-vous que tooset vos stratégies d’accès au contenu en conséquence.
> Les en-têtes d’autorisation ne sont jamais visibles par le biais d’entrées ou de sorties. Par conséquent, si le secret de hello il est utilisé, secret de hello n’est pas récupérable.

#### <a name="resource-deployment-template-with-secrets"></a>Modèle de déploiement de ressource avec des clés secrètes

Hello suivant montre un déploiement qui fait référence à un paramètre sécurisé de `secret` lors de l’exécution. Dans un fichier de paramètres distincts, vous pouvez spécifier la valeur d’environnement hello pour hello `secret`, ou utilisez [Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) secrets tooretrieve au niveau du déploiement.

``` json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "secretDeploymentParam": {
      "type": "securestring"
    }
  },
  "variables": {},
  "resources": [
    {
      "name": "secret-deploy",
      "type": "Microsoft.Logic/workflows",
      "location": "westus",
      "tags": {
        "displayName": "LogicApp"
      },
      "apiVersion": "2016-06-01",
      "properties": {
        "definition": {
          "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "actions": {
            "Call_External_API": {
              "type": "http",
              "inputs": {
                "headers": {
                  "Authorization": "@parameters('secret')"
                },
                "body": "This is hello request"
              },
              "runAfter": {}
            }
          },
          "parameters": {
            "secret": {
              "type": "SecureString"
            }
          },
          "triggers": {
            "manual": {
              "type": "Request",
              "kind": "Http",
              "inputs": {
                "schema": {}
              }
            }
          },
          "contentVersion": "1.0.0.0",
          "outputs": {}
        },
        "parameters": {
          "secret": {
            "value": "[parameters('secretDeploymentParam')]"
          }
        }
      }
    }
  ],
  "outputs": {}
}
```

## <a name="secure-access-tooservices-receiving-requests-from-a-workflow"></a>Sécuriser l’accès aux demandes de réception tooservices à partir d’un flux de travail

Il existe de nombreuses façons toohelp sécurisé que tooaccess a besoin de n’importe quelle application de la logique de point de terminaison hello.

### <a name="using-authentication-on-outbound-requests"></a>Utilisation de l’authentification sur les requêtes sortantes

Lorsque vous travaillez avec un HTTP, HTTP + Swagger (API Open) ou l’opération de Webhook, vous pouvez ajouter l’authentification toohello envoyé. Vous pouvez inclure l’authentification de base, l’authentification par certificat ou l’authentification Azure Active Directory. Plus d’informations sur comment tooconfigure cette authentification peut être détectée [dans cet article](../connectors/connectors-native-http.md#authentication).

### <a name="restricting-access-toologic-app-ip-addresses"></a>Limitation des adresses IP de l’accès toologic application

Tous les appels d’applications logiques proviennent d’un ensemble spécifique d’adresses IP par région. Vous pouvez ajouter un filtrage supplémentaire tooonly accepter les demandes de celles désigné des adresses IP. Pour obtenir la liste de ces adresses IP, consultez [Limites et configuration des applications logiques](logic-apps-limits-and-config.md#configuration).

### <a name="on-premises-connectivity"></a>Connectivité locale

Logique applications fournissent l’intégration avec plusieurs services tooprovide, sécurisée et fiable local communication.

#### <a name="on-premises-data-gateway"></a>Passerelle de données locale

Plusieurs connecteurs gérés pour les applications de la logique fournissent une connectivité sécurisée des systèmes de site tooon, y compris le système de fichiers, SQL, SharePoint, DB2 et bien plus encore. passerelle de Hello transmet des données à partir de sources locales sur des canaux chiffrés via hello Azure Service Bus. Tout le trafic provient sécurisé trafic sortant à partir de l’agent de passerelle hello. En savoir plus sur [le fonctionnement de la passerelle de données hello](logic-apps-gateway-install.md#gateway-cloud-service).

#### <a name="azure-api-management"></a>Gestion des API Azure

[Gestion des API Azure](https://azure.microsoft.com/services/api-management/) a des options de connectivité locale, y compris l’intégration de site à site VPN et ExpressRoute pour les systèmes de site tooon proxy et la communication sécurisées. Dans le Concepteur d’application logique de hello, vous pouvez sélectionner rapidement une API exposée à partir de la gestion des API Azure dans un flux de travail, les systèmes de site tooon fournissent un accès rapide.

#### <a name="hybrid-connections-from-azure-app-service"></a>Connexions hybrides à partir des services d’application Azure

Vous pouvez utiliser la fonctionnalité de connexion hybride hello local pour API Azure et Web apps toocommunicate local.  Plus d’informations sur les connexions hybrides et comment vous pouvez trouver tooconfigure [dans cet article](../app-service-web/web-sites-hybrid-connection-get-started.md).

## <a name="next-steps"></a>Étapes suivantes
[Créer un modèle de déploiement](logic-apps-create-deploy-template.md)  
[Gestion des exceptions](logic-apps-exception-handling.md)  
[Analyser vos applications logiques](logic-apps-monitor-your-logic-apps.md)  
[Diagnostic des échecs et problèmes d’applications logiques](logic-apps-diagnosing-failures.md)  
