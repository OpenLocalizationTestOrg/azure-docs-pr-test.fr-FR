---
title: "aaaAzure chiffrement de Service de stockage à l’aide du client de clé gérée dans le coffre de clés Azure | Documents Microsoft"
description: "Utilisez tooencrypt de fonctionnalité de chiffrement de Service de stockage Azure hello votre stockage d’objets Blob Azure sur le côté du service hello lors du stockage des données de hello, déchiffrer lors de la récupération des données hello à l’aide du client géré clés."
services: storage
documentationcenter: .net
author: lakasa
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: lakasa
ms.openlocfilehash: 870cae2f258b356aa234f8bba65a023ac389be10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="storage-service-encryption-using-customer-managed-keys-in-azure-key-vault"></a>Chiffrement du service de stockage à l’aide de clés gérées par le client dans Azure Key Vault

Microsoft Azure est engage toohelping protéger et de protéger vos données toomeet votre engagements de conformité et de sécurité de l’organisation.  Vous pouvez protéger vos données au repos consiste toouse stockage Service de chiffrement (SSE), qui chiffre vos données lors de l’écriture de toostorage automatiquement et déchiffre les données lors de leur récupération. Hello de chiffrement et de déchiffrement est complètement transparente et automatique utilise 256 bits [chiffrement AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), un des blocs les plus forts de hello chiffrements disponibles.

Vous pouvez utiliser des clés de chiffrement gérées par Microsoft avec SSE ou utiliser vos propres clés de chiffrement. Cet article aborderons hello ce dernier. Pour plus d’informations sur l’utilisation de clés gérées par Microsoft, ou sur SSE en général, consultez [Azure Storage Service Encryption pour les données au repos](storage-service-encryption.md).

tooprovide toouse de capacité hello vos propres clés de chiffrement, SSE pour le stockage d’objets Blob est intégré avec Azure Key Vault (AKV). Vous pouvez créer vos propres clés de chiffrement et les stocker dans AKV, ou vous pouvez utiliser des clés de chiffrement toogenerate d’AKV API. Non seulement AKV vous toomanage et contrôler vos clés, il permet également de vous tooaudit votre utilisation de la clé. 

Pourquoi vous souhaiteriez toocreate vos propres clés ? Elle vous donne plus de souplesse, y compris hello capacité toocreate, faire pivoter, désactiver et définir des contrôles d’accès et tooaudit hello chiffrement clés utilisées tooprotect vos données.

## <a name="sse-with-customer-managed-keys-preview"></a>SSE avec clés gérées par le client (préversion)

Actuellement, cette fonctionnalité est uniquement disponible en tant que version préliminaire. toouse cette fonctionnalité, vous devez toocreate un compte de stockage. Vous pouvez créer un coffre de clés et une clé, ou vous pouvez utiliser un coffre de clés et une clé existants. compte de stockage Hello et coffre de clés hello doivent être Bonjour même région, mais ils peuvent être dans différents abonnements.

Contactez le tooparticipate en version préliminaire de hello [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com). Nous fournissons un tooparticipate lien spécial dans l’aperçu de hello.

toolearn plus, consultez toohello [FAQ](#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).

> [!IMPORTANT]
> Vous devez vous inscrire pour hello aperçu préalable toofollowing hello étapes décrites dans cet article. Sans accès en version préliminaire, à ne pas être en mesure de tooenable cette fonctionnalité dans le portail de hello.

## <a name="getting-started"></a>Mise en route
## <a name="step-1-create-a-new-storage-accountstorage-create-storage-accountmd"></a>Étape 1 : [Créer un compte de stockage](storage-create-storage-account.md)

## <a name="step-2-enable-encryption"></a>Étape 2 : Activer le chiffrement
Vous pouvez activer SSE hello compte de stockage à l’aide de hello [portail Azure](https://portal.azure.com). Panneau de paramètres hello pour le compte de stockage hello, recherchez hello section Service Blob comme indiqué dans la figure ci-dessous et cliquez sur le chiffrement.

![Capture d’écran du portail affichant l’option de chiffrement](./media/storage-service-encryption/image1.png)
<br/>*Activer SSE pour le service BLOB*

Si vous souhaitez tooprogrammatically activer ou désactivez hello chiffrement de Service de stockage sur un compte de stockage, vous pouvez utiliser hello [API REST de fournisseur de ressources de stockage Azure](https://docs.microsoft.com/en-us/rest/api/storagerp/?redirectedfrom=MSDN), hello [bibliothèque de Client de fournisseur de ressources de stockage pour .NET](https://docs.microsoft.com/en-us/dotnet/api/?redirectedfrom=MSDN), [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview?view=azurermps-4.0.0), ou hello [CLI d’Azure](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli).

Dans cet écran, si vous ne voyez pas case à cocher de hello « utiliser votre propre clé », vous n’avez été approuvé pour l’aperçu de hello. Veuillez envoyer un message électronique trop[ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) et demander l’approbation.

![Capture d’écran du portail affichant le chiffrement (préversion)](./media/storage-service-encryption-customer-managed-keys/ssecmk1.png)

Par défaut, SSE utilise les clés gérées par Microsoft. toouse vos propres clés, la case de hello. Puis vous pouvez spécifier l’URI de votre clé, ou sélectionner une clé et un coffre de clés dans le sélecteur de hello.

## <a name="step-3-select-your-key"></a>Étape 3 : Sélectionner votre clé

![Capture d’écran du portail affichant l’option de chiffrement Utiliser votre propre clé](./media/storage-service-encryption-customer-managed-keys/ssecmk2.png)

![Capture d’écran du portail affichant l’option de chiffrement avec saisie de l’URI de la clé](./media/storage-service-encryption-customer-managed-keys/ssecmk3.png)

Si le compte de stockage hello n’a pas accès toohello le coffre de clés, vous pouvez exécuter suivant de hello commande à l’aide de comptes Azure Powershell toogrant accès toohello stockage toohello requis coffre de clés.

![Capture d’écran du portail affichant l’accès refusé au coffre de clés](./media/storage-service-encryption-customer-managed-keys/ssecmk4.png)

Vous pouvez également accorder l’accès via hello portail Azure en accédant toohello Azure Key Vault Bonjour portail Azure et de l’octroi au compte de stockage toohello accès.

## <a name="step-4-copy-data-toostorage-account"></a>Étape 4 : Copie compte toostorage de données
Si vous souhaitez que les données tootransfer dans votre compte de stockage afin qu’il est chiffré, consultez trop[étape 3 de prise en main du chiffrement de Service de stockage pour les données au repos](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-3-copy-data-to-storage-account).

## <a name="step-5-query-hello-status-of-hello-encrypted-data"></a>Étape 5 : Requête d’état hello Hello des données chiffrées
état de hello tooquery de données de hello chiffré, consultez trop[étape 4 de prise en main du chiffrement de Service de stockage pour les données au repos](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-4-query-the-status-of-the-encrypted-data).

## <a name="frequently-asked-questions-about-storage-service-encryption-for-data-at-rest"></a>Forum Aux Questions Azure Storage Service Encryption pour les données au repos
**Q : J’utilise le stockage Premium. Puis-je utiliser SSE avec des clés gérées par le client ?**

R : Oui, SSE avec des clés gérées par Microsoft ou par le client est pris en charge sur le stockage Standard et sur le stockage Premium. 

**Q : Puis-je créer des comptes de stockage dans lesquels SSE avec clés de gérées par le client est activé à l’aide d’Azure PowerShell et de l’interface de ligne de commande Azure ?**

R. : Oui.

**Q : Quel est le coût de stockage Azure si SSE avec clés gérées par le client est activé ?**

R : Un coût spécifique est associé à l’utilisation d’Azure Key Vault. Pour plus d’informations, consultez [Tarification d’Azure Key Vault](https://azure.microsoft.com/en-us/pricing/details/key-vault/). L’utilisation de SSE n’entraîne aucun coût supplémentaire.

**Q : puis-je révoquer les clés de chiffrement toohello accès ?**

R : Oui, vous pouvez révoquer l’accès à tout moment. Il existe plusieurs façons toorevoke touches d’accès tooyour rapide. Reportez-vous trop[Azure Key Vault PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.0.0) et [CLI d’Azure Key Vault](https://docs.microsoft.com/en-us/cli/azure/keyvault) pour plus d’informations. Révocation de l’accès sera effectivement accès tooall objets BLOB de blocs dans le compte de stockage hello comme hello clé de chiffrement de compte n’est pas accessible par le stockage Azure.

**Q : Puis-je créer un compte de stockage et une clé dans autre région ?**

R : non, compte de stockage hello et toobe besoin de clés/clé de coffre dans hello même région. 

**Q : puis-je activer SSE avec les clés gérées par le client lors de la création du compte de stockage hello ?**

R : Non. Lorsque vous activez SSE lors de la création du compte de stockage hello, vous pouvez uniquement utiliser des touches de gérée par Microsoft. Si vous souhaitez que les clés toouse géré par le client, vous devez tooupdate les propriétés hello du compte de stockage. Vous pouvez utiliser REST ou un des tooprogrammatically de bibliothèques de client de stockage hello mettre à jour de votre compte de stockage, ou mettre à jour les propriétés du compte de stockage hello à l’aide de hello portail Azure après avoir créé le compte de hello.

**Q : Puis-je désactiver le chiffrement lorsque j’utilise SSE avec des clés gérées par le client ?**

R : Non, vous ne pouvez pas désactiver le chiffrement lorsque vous utilisez SSE avec des clés gérées par le client. le chiffrement toodisable, vous devez tooswitch toousing gérée par Microsoft clés. Pour cela, à l’aide de hello portail Azure ou PowerShell.

**Q : Est-ce que SSE est activé par défaut lorsque je crée un compte de stockage ?**

R : SSE n’est pas activée par défaut ; Vous pouvez utiliser hello tooenable portail Azure il. Vous pouvez également programmer activer cette fonctionnalité à l’aide de hello API REST de fournisseur de ressource de stockage. 

**Q : Je ne peux pas activer le chiffrement sur mon compte de stockage.**

R : S’agit-il d’un compte de stockage Resource Manager ? Les comptes de stockage classiques ne sont pas pris en charge. SSE avec clés gérées par le client peut aussi être activé, mais uniquement sur les comptes de stockage de Gestionnaire des ressources nouvellement créés.

**Q : SSE avec clés gérées par le client est-il uniquement autorisé dans des régions spécifiques ?**

R : SSE est disponible uniquement dans certaines régions pour le stockage d’objets blob dans le cadre de cette préversion. Envoyez un message électronique [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) toocheck pour la disponibilité et des détails sur la version préliminaire. 

**Q : comment contacter une personne si vous rencontrez des problèmes ou que vous souhaitez tooprovide commentaires ?**

R : Veuillez contacter [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) pour tous les problèmes connexes tooStorage chiffrement du Service. 

## <a name="next-steps"></a>Étapes suivantes

*   Pour plus d’informations sur l’ensemble complet de hello de la sécurité de fonctionnalités qui aident les développeurs à créer des applications sécurisées, consultez hello [Guide de sécurité de stockage](https://docs.microsoft.com/en-us/azure/storage/storage-security-guide).
*   Pour plus d’informations générales sur Azure Key Vault, consultez [Qu’est-ce qu’Azure Key Vault ?](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis).
*   Pour prendre en main Azure Key Vault, consultez [Prise en main d’Azure Key Vault](../key-vault/key-vault-get-started.md).
