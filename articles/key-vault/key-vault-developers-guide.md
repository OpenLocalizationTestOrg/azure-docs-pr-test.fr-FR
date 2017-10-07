---
title: "Guide du développeur aaaAzure Key Vault"
description: "Les développeurs peuvent utiliser des clés de chiffrement toomanage coffre de clés Azure au sein de l’environnement de Microsoft Azure hello."
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/04/2017
ms.author: bruceper
ms.openlocfilehash: 631cea1315964cd0b97e8b2cf3311754230fb801
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-developers-guide"></a>Guide du développeur de coffre de clés Azure

Le coffre de clés vous permet de toosecurely accès des informations sensibles dans vos applications :

- Clés et les secrets sont protégées sans avoir à code de hello toowrite vous-même et que vous êtes en mesure de facilement toouse à partir de vos applications.
- Vous toohave en mesure de vos clients propres et gérez leurs propres clés afin de vous concentrer sur les fonctionnalités du logiciel hello core. De cette façon, vos applications ne possédera pas responsabilité de hello ou responsabilité pour les clés de locataires de vos clients et les secrets.
- Votre application peut utiliser des clés pour la signature et chiffrement encore conserve la gestion de clés hello externe à partir de votre application, qui toobe de votre solution convient en tant qu’une application distribuée géographiquement.
- À compter de la version de septembre 2016 hello de coffre de clés, vos applications peuvent désormais utiliser le coffre de clés [certificats](https://docs.microsoft.com/rest/api/keyvault/certificate-operations). Pour plus d’informations, consultez [À propos des clés, des secrets et des certificats](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates).

Pour des informations plus générales sur le coffre de clés Azure Key Vault, voir [Qu’est-ce qu’Azure Key Vault ?](key-vault-whatis.md).

## <a name="public-previews"></a>Préversions publiques

Nous publions régulièrement la préversion publique d’une nouvelle fonctionnalité de Key Vault. Essayez-les et envoyez votre avis à azurekeyvault@microsoft.com, notre adresse e-mail dédiée aux commentaires.

### <a name="storage-account-keys---july-10-2017"></a>Clés de compte de stockage - 10 juillet 2017

>[!NOTE]
>Pour cette mise à jour de hello uniquement d’Azure Key Vault **clés de compte de stockage** fonctionnalité est en version préliminaire.

Cette préversion inclut notre nouvelle fonctionnalité Clés de compte de stockage, disponible par le biais de ces interfaces : [.NET/C#](https://docs.microsoft.com/dotnet/api/microsoft.azure.keyvault/), [REST](https://docs.microsoft.com/rest/api/keyvault/) et [PowerShell](https://docs.microsoft.com/powershell/module/azurerm.keyvault/). 

Pour plus d’informations sur la nouvelle fonctionnalité de clés de compte de stockage hello, consultez [présentation de clés de compte de stockage Azure Key Vault](key-vault-ovw-storage-keys.md).

## <a name="videos"></a>Vidéos

Cette vidéo vous montre comment votre propre clé de coffre toocreate et toouse à partir de hello, exemple d’application « Hello Key Vault ».

- [Développeur Key Vault - guide de démarrage rapide](https://channel9.msdn.com/Blogs/Azure/Azure-Key-Vault-Developer-Quick-Start/player)

Ressources mentionnées dans la vidéo ci-dessus :

- [Azure PowerShell](http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409)
- [Exemple de code de coffre de clés Azure](http://go.microsoft.com/fwlink/?LinkId=521527&clcid=0x409)

## <a name="creating-and-managing-key-vaults"></a>Création et gestion des coffres de clés

Avant d’utiliser le coffre de clés Azure dans votre code, vous pouvez créer et gérer les coffres via REST, les modèles de gestionnaire de ressources, PowerShell ou CLI, comme décrit dans hello suivant des articles :

- [Créer et gérer les coffres de clés avec REST](https://docs.microsoft.com/rest/api/keyvault/)
- [Créer et gérer les coffres de clés avec PowerShell](key-vault-get-started.md)
- [Créer et gérer les coffres de clés avec l'interface de ligne de commande](key-vault-manage-with-cli2.md)
- [Créer un coffre de clés et ajouter un secret via un modèle Azure Resource Manager](../azure-resource-manager/resource-manager-template-keyvault.md)

> [!NOTE]
> Les opérations sur les coffres de clés sont authentifiées via AAD et autorisées par une stratégie d’accès propre au coffre de clés.

## <a name="coding-with-key-vault"></a>Codage avec coffre de clés

Hello système de gestion de coffre de clés pour les programmeurs qui se compose de plusieurs interfaces, avec les autres en tant que base de hello. Via l’interface REST de hello, toutes vos ressources de coffres de clé sont accessibles. clés, des secrets et des certificats. [Informations de référence sur l’API REST Key Vault](https://docs.microsoft.com/rest/api/keyvault/) 

### <a name="supported-programming-languages"></a>Langages de programmation pris en charge

#### <a name="net"></a>.NET

- [Informations de référence sur l’API .NET pour Key Vault](https://docs.microsoft.com/dotnet/api/microsoft.azure.keyvault) 

Pour plus d’informations sur la version 2.x de hello Hello .NET SDK, consultez hello [notes de publication](key-vault-dotnet2api-release-notes.md).

#### <a name="java"></a>Java

- [Kit de développement logiciel (SDK) Java pour Key Vault](https://docs.microsoft.com/java/api/com.microsoft.azure.keyvault)

#### <a name="nodejs"></a>Node.js

Dans Node.js, les API de gestion de coffre hello et les API d’objet coffre hello sont distincts. Key Vault Management permet de créer et de mettre à jour les coffres de clés. L’API Key Vault Operations sert à travailler avec des objets de coffres, comme les clés, les secrets et les certificats. 

- [Informations de référence sur l’API Node.js pour Key Vault Management](http://azure.github.io/azure-sdk-for-node/azure-arm-keyvault/latest/)
- [Informations de référence sur l’API Node.js pour les opérations Key Vault](http://azure.github.io/azure-sdk-for-node/azure-keyvault/latest/) 

### <a name="quick-start"></a>Démarrage rapide

- [Création d'un coffre de clés](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
- [Bien démarrer avec Key Vault dans Node.js](https://azure.microsoft.com/en-us/resources/samples/key-vault-node-getting-started/)

### <a name="code-examples"></a>Exemples de code

Pour obtenir des exemples complets d’utilisation de Key Vault avec vos applications, voir :

- [Exemples de code Azure Key Vault](http://www.microsoft.com/download/details.aspx?id=45343) - exemple d’application .NET *HelloKeyVault* et exemple de service web Azure. 
- [Utilisez le coffre de clés Azure à partir d’une Application Web](key-vault-use-from-web-application.md) -didacticiel toohelp vous apprendre comment toouse Azure Key Vault à partir d’une application web dans Azure. 

## <a name="how-tos"></a>Procédures

Hello scénarios et les articles suivants fournissent des conseils spécifiques à une tâche pour l’utilisation avec Azure Key Vault :

- [ID de client de coffre de clés modifiées après l’abonnement déplacer](key-vault-subscription-move-fix.md) - lorsque vous déplacez votre abonnement Azure à partir d’un tootenant B de client, vos archivages clés existants ne sont pas accessibles par des principaux hello (utilisateurs et applications) dans le locataire correctif B. cette à l’aide de ce guide.
- [L’accès à la clé de coffre derrière des pare-feu](key-vault-access-behind-firewall.md) -tooaccess une clé de coffre de votre coffre de clés client application besoins toobe en mesure de tooaccess plusieurs points de terminaison pour différentes fonctionnalités.
- [Comment tooGenerate et les clés de Transfer HSM-Protected pour Azure Key Vault](key-vault-hsm-protected-keys.md) -cela vous permet de planifier, générer et transférer votre propre toouse clés protégées par HSM avec Azure Key Vault.
- [Comment toopass sécuriser les valeurs (telles que les mots de passe) au cours du déploiement](../azure-resource-manager/resource-manager-keyvault-parameter.md) - lorsque vous devez toopass une valeur sûre (par exemple, un mot de passe) en tant que paramètre pendant le déploiement, vous pouvez stocker cette valeur en tant que secret dans une valeur hello Azure Key Vault et une référence dans d’autres Modèles du Gestionnaire de ressources.
- [Comment toouse le coffre de clés pour la gestion de clés extensible avec SQL Server](https://msdn.microsoft.com/library/dn198405.aspx) -hello connecteur SQL Server pour Azure Key Vault permet à SQL Server et SQL dans VM tooleverage hello service Azure Key Vault comme fournisseur de gestion de clés Extensible (EKM) clés de son chiffrement tooprotect pour lier des applications ; Chiffrement transparent des données, le chiffrement de sauvegarde et le chiffrement au niveau colonne.
- [Comment toodeploy les tooVMs de certificats de coffre de clés](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/) - une application cloud en cours d’exécution dans une machine virtuelle sur Azure besoins un certificat. Comment obtenir ce certificat sur cette machine virtuelle dès aujourd’hui ?
- [Comment tooset configuration coffre de clés avec tooend de fin de clé de rotation et de l’audit](key-vault-key-rotation-log-monitoring.md) -cet exemple présente le tooset de rotation des clés et d’audit avec Azure Key Vault.
- [Déploiement d’Azure App Service Certificate via Key Vault]( https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/) fournit des instructions détaillées pour déployer les certificats stockés dans Key Vault dans le cadre l’offre [App Service Certificate](https://azure.microsoft.com/blog/internals-of-app-service-certificate/).
- [Accorder l’autorisation réduire applications tooaccess un coffre de clés](key-vault-group-permissions-for-apps.md) stratégie de contrôle d’accès le coffre de clés prend uniquement en charge les entrées de 16. Mais vous pouvez créer un groupe de sécurité Azure Active Directory. Ajouter hello tous les groupe de sécurité de service principaux toothis associé et accorder l’accès toothis sécurité groupe tooKey coffre.
- Pour obtenir des conseils plus spécifiques sur certaines tâches, en relation avec l’intégration et l’utilisation de coffres de clés avec Azure, voir les [exemples de modèles Azure Resource Manager de Ryan Jones pour Key Vault](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).
- [Comment toouse le coffre de clés soft-suppression avec l’interface CLI](key-vault-soft-delete-cli.md) vous guide à travers les hello utilisation et de cycle de vie d’un coffre de clés et les différents objets de coffre de clés avec soft-suppression est activée.
- [Comment toouse le coffre de clés soft-suppression avec PowerShell](key-vault-soft-delete-powershell.md) vous guide à travers les hello utilisation et de cycle de vie d’un coffre de clés et les différents objets de coffre de clés avec soft-suppression est activée.

## <a name="integrated-with-key-vault"></a>Intégration avec Key Vault

Ces articles concernent d’autres scénarios et services qui utilisent ou intègrent Key Vault.

- [Le chiffrement des disques Azure](../security/azure-security-disk-encryption.md) tire parti hello norme industrielle [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) la fonctionnalité de Windows et hello [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) fonctionnalité de chiffrement de volume tooprovide Linux pour hello du système d’exploitation et les données de salutation disques. solution de Hello est intégrée à Azure Key Vault toohelp contrôler et de gérer les clés de chiffrement de disque hello et des clés secrètes dans votre abonnement de coffre de clés, tout en garantissant que toutes les données de disques de machine virtuelle hello sont chiffrées au repos dans votre stockage Azure.
- [Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md) fournit l’option pour le chiffrement des données stockées dans le compte de hello. Gestion de clés, Data Lake Store propose deux modes de gestion de vos clés de chiffrement principale (MEKs), qui sont requis pour le déchiffrement des données qui sont stockées dans hello Data Lake Store. Vous pouvez laisser Data Lake Store gérer hello MEKs pour vous, ou choisissez tooretain approprier MEKs hello à l’aide de votre compte Azure Key Vault. Vous spécifiez le mode de gestion de clés hello lors de la création d’un compte Data Lake Store. 
- [Azure Information Protection](/information-protection/plan-design/plan-implement-tenant-key) vous permet de toomanager votre propre clé de locataire. Par exemple, au lieu de gérer votre clé de locataire (valeur par défaut de hello) de Microsoft, vous pouvez gérer vos propres toocomply clé de locataire à des réglementations spécifiques qui s’appliquent tooyour organisation. Gérer votre propre clé de locataire est également référencés tooas bring your own key, BYOK.

## <a name="key-vault-overviews-and-concepts"></a>Concepts et présentations des coffres de clés

- [Comportement de soft-suppression de coffre de clés](key-vault-ovw-soft-delete.md) décrit une fonctionnalité qui permet la récupération des objets supprimés, si la suppression de hello était accidentelle ou intentionnelle.
- [Client de coffre de clés de limitation](key-vault-ovw-throttling.md) vous oriente toohello les concepts de base de la limitation et propose une approche pour votre application.
- [Vue d’ensemble des clés de compte de stockage coffre de clés](key-vault-ovw-storage-keys.md) décrit les clés de comptes de stockage Azure integration hello coffre de clés.
- [Des mondes de sécurité le coffre de clés](key-vault-ovw-security-worlds.md) décrit hello des relations entre les régions et les zones de sécurité.

## <a name="social"></a>Réseaux sociaux

- [Blog de Key Vault](http://aka.ms/kvblog)
- [Forum de Key Vault](http://aka.ms/kvforum)

## <a name="supporting-libraries"></a>Bibliothèques connexes

- [Microsoft Azure Key Vault Core Library](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Core) fournit les interfaces **IKey** et **IKeyResolver** pour localiser des clés à partir d’identificateurs et effectuer des opérations avec des clés.
- [Microsoft Azure Key Vault Extensions](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Extensions) fournit des fonctionnalités étendues pour Azure Key Vault.


