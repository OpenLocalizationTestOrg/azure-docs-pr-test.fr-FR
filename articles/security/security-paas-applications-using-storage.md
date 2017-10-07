---
title: "les applications PaaS aaaSecuring à l’aide du stockage Azure | Documents Microsoft"
description: " Découvrez les bonnes pratiques de sécurité du stockage Azure pour protéger vos applications mobiles et web PaaS. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: TomShinder
ms.openlocfilehash: 3fed75cb121e7f32eb8b948ee12ca35fb25eca7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-web-and-mobile-applications-using-azure-storage"></a>Sécurisation des applications mobiles et web PaaS à l’aide du stockage Azure
Dans cet article, nous abordons un ensemble de bonnes pratiques de sécurité du stockage Azure pour protéger vos applications mobiles et web PaaS. Ces recommandations sont dérivées de notre expérience avec Azure et les expériences hello de clients comme vous-même.

Hello [guide de sécurité de stockage Azure](../storage/common/storage-security-guide.md) constitue une source précieuse pour plus d’informations sur le stockage Azure et la sécurité.  Cet article traite à un niveau élevé des concepts hello trouvés dans le guide de sécurité hello et guide de sécurité toohello de liens, ainsi que d’autres sources, pour plus d’informations.

## <a name="azure-storage"></a>Azure Storage
Azure rend possible toodeploy et utilisez le stockage de façons pas facilement réalisable sur site. Grâce au stockage Azure, vous pouvez atteindre des niveaux élevés de scalabilité et de disponibilité avec relativement peu d’effort. Non seulement est foundation hello de stockage Azure pour Windows et Linux des Machines virtuelles Azure, il peut également gérer les grandes applications distribuées.

Le stockage Azure fournit hello suivant quatre services : stockage, le stockage de Table, stockage de file d’attente et le stockage de fichiers d’objets Blob. toolearn, voir [Introduction tooMicrosoft Azure Storage](../storage/storage-introduction.md).

## <a name="best-practices"></a>Meilleures pratiques
Cet article traite hello suivant les meilleures pratiques :

- Protection de l’accès :
   - Signatures d’accès partagé (SAP)
   - Disque managé
   - Contrôle d’accès en fonction du rôle

- Chiffrement du stockage :
   - Chiffrement côté client pour les données de valeur élevée
   - Azure Disk Encryption pour les machines virtuelles
   - Storage Service Encryption

## <a name="access-protection"></a>Protection de l’accès
### <a name="use-shared-access-signature-instead-of-a-storage-account-key"></a>Utiliser la signature d’accès partagé au lieu d’une clé de compte de stockage

Dans une solution IaaS, qui exécute généralement des machines virtuelles Windows Server ou Linux, les fichiers sont protégés contre la divulgation d’informations et les menaces de falsification à l’aide de mécanismes de contrôle d’accès. Sur Windows, vous utiliseriez des [listes de contrôle d’accès (ACL)](../virtual-network/virtual-networks-acl.md), tandis que sur Linux, vous utiliseriez sans doute [chmod](https://en.wikipedia.org/wiki/Chmod). Pour l’essentiel, c’est exactement ce que vous feriez pour protéger des fichiers sur un serveur dans votre propre centre de données aujourd’hui.

PaaS est différent. Un des fichiers de toostore de façons courantes hello dans Microsoft Azure est toouse [le stockage Blob Azure](../storage/storage-dotnet-how-to-use-blobs.md). Une différence entre le stockage d’objets Blob et d’autres systèmes de stockage de fichier est e/s de fichier hello et les méthodes de protection hello qui accompagnent d’e/s de fichier.

Le contrôle d’accès est critique. toohelp vous contrôlez l’accès tooAzure stockage, hello système génère deux clés de compte de stockage de 512 bits (SAKs) lorsque vous [créer un compte de stockage](../storage/common/storage-create-storage-account.md). niveau Hello de redondance de clé rend possible pour l’interruption service tooavoid lors de la rotation des clés routine.

Clés d’accès de stockage sont des secrets de priorité élevée et ne doivent être accessible toothose responsable de contrôle d’accès de stockage. Si les personnes non autorisées hello obtenir l’accès des clés de toothese, ils seront ont un contrôle total de stockage et pourrait remplacer, supprimez ou ajoutez toostorage de fichiers. Cela inclut les logiciels malveillants et autres types de contenu qui peuvent nuire à vos clients ou à votre organisation.

Vous devez toujours un tooobjects d’accès tooprovide moyen dans le stockage. accès tooprovide plus précis que vous pouvez tirer parti de [Signature d’accès partagé](../storage/common/storage-dotnet-shared-access-signature-part-1.md) (SAS). Hello SAS rend possible pour vous tooshare des objets spécifiques dans le stockage pour un intervalle de temps prédéfini et avec des autorisations spécifiques. Une Signature d’accès partagé vous permet de toodefine :

- intervalle de salutation sur quel hello SAS est valide, y compris l’heure de début hello et l’heure d’expiration de hello.
- autorisations de Hello accordées par hello SAS. Par exemple, une SAP sur un objet blob peut accorder une lecture de l’utilisateur et écrire des objets blob de toothat autorisations, mais pas supprimer des autorisations.
- Une adresse IP facultative ou plage d’adresses IP à partir de laquelle le stockage Azure accepte hello SAS. Par exemple, vous pouvez spécifier une plage d’adresses IP appartenant tooyour organisation. Cela fournit une autre mesure de sécurité à votre SAP.
- protocole Hello sur lequel le stockage Azure accepte hello SAS. Vous pouvez utiliser cette tooclients d’accès toorestrict paramètre facultatif à l’aide de HTTPS.

Associations de sécurité vous permet de tooshare contenu hello librement tooshare sans donner vos clés de compte de stockage. Toujours à l’aide de SAP dans votre application est un tooshare de manière sécurisée à vos ressources de stockage sans compromettre vos clés de compte de stockage.

toolearn, voir [à l’aide de Signatures d’accès partagé](../storage/common/storage-dotnet-shared-access-signature-part-1.md) (SAS). reportez-vous à ces risques, toolearn plus toomitigate potentielle de risques et les recommandations [meilleures pratiques lors de l’utilisation de SAP](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

### <a name="use-managed-disks-for-vms"></a>Utiliser des disques managés pour les machines virtuelles

Lorsque vous choisissez [disques gérés d’Azure](../storage/storage-managed-disks-overview.md), Azure gère les comptes de stockage hello que vous utilisez pour vos disques de machine virtuelle. Vous devez toodo est choisissez type hello de disque (Premium ou Standard) et la taille du disque hello ; Le stockage Azure effectuera hello rest. Vous n’avez pas tooworry sur les limites d’extensibilité qui auraient sinon nécessité des comptes de stockage tooyou toomultiple.

toolearn, voir [Forum aux Questions sur managées et les disques premium](../storage/storage-faq-for-disks.md).

### <a name="use-role-based-access-control"></a>Utiliser le contrôle d’accès en fonction du rôle

Précédemment, nous avons abordé à l’aide de Signature d’accès partagé (SAS) toogrant limitée accès tooobjects dans vos clients tooother de compte de stockage, sans exposer votre clé de compte de stockage de compte. Parfois, les risques de hello associés à une opération particulière par rapport à votre compte de stockage dépassent les avantages de hello de SAP. Il est parfois plus simple accès toomanage par d’autres moyens.

Une autre façon toomanage l’accès est toouse [du contrôle d’accès](../active-directory/role-based-access-control-what-is.md) (RBAC). RBAC, vous vous concentrez sur fournir aux employés les autorisations exactes hello que dont ils ont besoin, basée sur hello besoin tooknow et les principes de sécurité de privilège minimum. Trop d’autorisations peuvent exposer un tooattackers de compte. Si le nombre d’autorisations est trop faible, les employés ne peuvent pas effectuer leur travail efficacement. RBAC permet de résoudre ce problème en offrant une gestion précise de l’accès pour Azure. Il est impératif pour les organisations qui souhaitent utiliser les stratégies de sécurité tooenforce pour accéder aux données.

Vous pouvez tirer parti des rôles RBAC intégrés dans Azure tooassign privilèges toousers. Envisagez d’utiliser un collaborateur de compte de stockage pour les opérateurs cloud qui doivent toomanage les comptes de stockage et les comptes de stockage classiques de toomanage rôle Collaborateur de compte de stockage classique. Pour les opérateurs cloud qui doivent toomanage machines virtuelles, mais pas hello virtual network ou toowhich de compte de stockage qu’ils sont connectés, envisagez de les ajouter toohello collaborateur d’ordinateur virtuel.

Les organisations qui n’appliquent aucun contrôle d’accès aux données via des fonctionnalités telles que RBAC risquent d’octroyer plus de privilèges que nécessaire à leurs utilisateurs. Cela peut entraîner la compromission de toodata en autorisant certaines toodata d’accès aux utilisateurs qu’ils ne devraient pas avoir en place de première hello.

toolearn d’informations sur RBAC, consultez :

- [Contrôle d’accès en fonction du rôle Azure](../active-directory/role-based-access-control-configure.md)
- [Rôles intégrés pour le contrôle d’accès en fonction du rôle Azure](../active-directory/role-based-access-built-in-roles.md)
- [Guide de sécurité de stockage Azure](../storage/common/storage-security-guide.md) pour plus de détails sur la façon dont toosecure votre compte de stockage avec RBAC

## <a name="storage-encryption"></a>Chiffrement du stockage
### <a name="use-client-side-encryption-for-high-value-data"></a>Utiliser le chiffrement côté client pour les données de valeur élevée

Permet de chiffrement côté client vous tooprogrammatically chiffrer les données en transit avant de le télécharger tooAzure stockage et déchiffrer les données par programme lors de leur récupération à partir du stockage.  Ce dispositif fournit le chiffrement des données en transit, mais également le chiffrement des données au repos.  Le chiffrement côté client est la méthode la plus sûre de hello du chiffrement de vos données, mais il vous nécessitent l’application de tooyour toomake les modifications par programme et mettre le processus de gestion de clés en place.

Le chiffrement côté client vous permet également contrôle seul toohave vos clés de chiffrement.  Vous pouvez créer et gérer vos propres clés de chiffrement.  Le chiffrement côté client utilise une technique d’enveloppe où hello bibliothèque cliente de stockage Azure génère une contenu clé de chiffrement (CEK) qui est ensuite encapsulée (chiffrée) à l’aide de la clé de chiffrement à clé hello (KEK). Hello veillent est identifié par un identificateur de clé et peut être une paire de clés asymétriques ou une clé symétrique et peut être géré localement ou de [Azure Key Vault](../key-vault/key-vault-whatis.md).

Le chiffrement côté client est intégré à hello Java et les bibliothèques clientes de stockage de .NET hello.  Pour plus d’informations sur le chiffrement de données dans les applications clientes et sur la génération et la gestion de vos propres clés de chiffrement, consultez [Chiffrement côté client et Azure Key Vault pour Stockage Microsoft Azure](../storage/storage-client-side-encryption.md).

### <a name="azure-disk-encryption-for-vms"></a>Azure Disk Encryption pour les machines virtuelles
Azure Disk Encryption est une fonctionnalité qui vous permet de chiffrer vos disques de machine virtuelle IaaS Windows et Linux. Le chiffrement des disques Azure s’appuie sur la fonctionnalité standard BitLocker hello industrie de Windows et fonctionnalité d’exploration de données-Crypt hello du chiffrement de volume tooprovide Linux pour hello du système d’exploitation et des disques de données hello. solution de Hello est intégrée à Azure Key Vault toohelp contrôler et de gérer les clés de chiffrement de disque hello et les secrets dans votre abonnement de coffre de clés. solution de Hello garantit également que toutes les données sur les disques de machine virtuelle hello sont chiffrées au repos dans votre stockage Azure.

Consultez [Azure Disk Encryption pour des machines virtuelles Windows et Linux IaaS](azure-security-disk-encryption.md).

### <a name="storage-service-encryption"></a>Storage Service Encryption
Lorsque [chiffrement de Service de stockage](../storage/storage-service-encryption.md) de stockage de fichiers est activé, les données de salutation sont chiffrées automatiquement à l’aide du chiffrement AES-256. Microsoft gère tous les hello chiffrement, le déchiffrement et la gestion de clés. Cette fonctionnalité est disponible pour les types de redondance LRS et GRS.

## <a name="next-steps"></a>Étapes suivantes
Cet article introduit collection tooa de stockage Azure meilleures pratiques de sécurité pour sécuriser votre PaaS applications web et mobiles. toolearn savoir plus sur la sécurisation de vos déploiements PaaS, consultez :

- [Sécurisation des déploiements PaaS](security-paas-deployments.md)
- [Sécurisation des applications mobiles et web PaaS à l’aide d’Azure App Services](security-paas-applications-using-app-services.md)
- [Sécurisation des bases de données PaaS dans Azure](security-paas-applications-using-sql.md)
