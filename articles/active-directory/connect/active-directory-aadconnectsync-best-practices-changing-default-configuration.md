---
title: "Synchronisation Azure AD Connect : modification de la configuration par défaut de hello | Documents Microsoft"
description: "Fournit les meilleures pratiques pour la modification de configuration par défaut de hello de synchronisation Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 7638a031-1635-4942-94c3-fce8f09eed5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: aa05e935edd02c49c3c3fdc198b854f50327847c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-best-practices-for-changing-hello-default-configuration"></a>Synchronisation Azure AD Connect : meilleures pratiques pour la modification de configuration par défaut de hello
Hello de cette rubrique vise toodescribe pris en charge et non pris en charge de synchronisation de modifications tooAzure AD Connect.

configuration de Hello créés par Azure AD Connect fonctionne « tel quel » pour la plupart des environnements qui synchroniser Active Directory local avec Azure AD. Toutefois, dans certains cas, il est nécessaire tooapply besoin de certaines toosatisfy de configuration tooa modifications un particulier ou exigence.

## <a name="changes-toohello-service-account"></a>Compte de service de toohello de modifications
Synchronisation Azure AD Connect s’exécute sous un compte de service créé par l’Assistant installation hello. Ce compte de service conserve hello chiffrement clés toohello base de données utilisée par la synchronisation. Il est créé avec un mot de passe de 127 caractères de long et mot de passe hello est toonot expirer.

* Il s’agit de **non pris en charge** toochange ou réinitialisation du mot de passe hello hello du compte de service. Cela supprime les clés de chiffrement hello et service de hello n’est pas en mesure de tooaccess hello et n’est pas en mesure de toostart.

## <a name="changes-toohello-scheduler"></a>Planificateur de toohello de modifications
En commençant par les versions hello à partir de la version 1.1 (février 2016), vous pouvez configurer hello [planificateur](active-directory-aadconnectsync-feature-scheduler.md) toohave une autre synchronisation cycle par défaut de hello 30 minutes.

## <a name="changes-toosynchronization-rules"></a>Règles de tooSynchronization de modifications
l’Assistant installation Hello propose une configuration qui est supposée toowork pour les scénarios les plus courants hello. En cas de besoin de la configuration de toohello toomake modifications, vous devez suivre ces règles toostill ont une configuration prise en charge.

* Vous pouvez [modifier le flux d’attributs](active-directory-aadconnectsync-change-the-configuration.md#other-common-attribute-flow-changes) si le flux d’attribut directe hello par défaut ne conviennent pas pour votre organisation.
* Si vous souhaitez trop[ne passent pas un attribut](active-directory-aadconnectsync-change-the-configuration.md#do-not-flow-an-attribute) et suppression de valeurs de l’attribut existant dans Azure AD, vous devez toocreate une règle pour ce scénario.
* [Désactiver une règle de synchronisation indésirable](#disable-an-unwanted-sync-rule) plutôt que la supprimer. Une règle supprimée est recréée pendant la mise à niveau.
* trop[modifier une règle d’out-of-box](#change-an-out-of-box-rule), vous devez effectuer une copie de hello d’origine de règle et désactive la règle d’out-of-box hello. Hello Éditeur des règles de synchronisation vous invite à entrer et vous aide à vous.
* Exportez vos règles de synchronisation personnalisées à l’aide de hello Éditeur des règles de synchronisation. Hello éditeur vous fournit un script PowerShell que vous pouvez utiliser tooeasily les recréer dans un scénario de récupération d’urgence.

> [!WARNING]
> règles de synchronisation d’out-of-box Hello ont une empreinte numérique. Si vous apportez une modification des règles de toothese, l’empreinte numérique hello est n’est plus mise en correspondance. Lorsque vous essayez de tooapply une nouvelle version d’Azure AD Connect, vous pouvez avoir des problèmes Bonjour futures. Seulement faire modifications hello qu'il est décrit dans cet article.

### <a name="disable-an-unwanted-sync-rule"></a>Désactiver une règle de synchronisation indésirable
Ne supprimez pas une règle de synchronisation out-of-box. Elle est recréée au cours de la mise à niveau suivante.

Dans certains cas, l’Assistant installation hello a généré une configuration qui ne fonctionne pas pour votre topologie. Par exemple, si vous disposez d’une topologie de forêt compte-ressource mais vous les schéma étendu hello dans la forêt de comptes hello avec schéma de Exchange hello, des règles pour Exchange sont créés pour la forêt de comptes hello et la forêt de ressources hello. Dans ce cas, vous devez toodisable hello la règle de synchronisation pour Exchange.

![Règle de synchronisation désactivée](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/exchangedisabledrule.png)

Dans l’image hello ci-dessus, l’Assistant installation hello a trouvé un ancien schéma Exchange 2003 dans la forêt de comptes hello. Cette extension de schéma a été ajoutée avant de la forêt de ressources hello a été introduit dans l’environnement de Fabrikam. tooensure aucuns attributs à partir de la mise en œuvre de Exchange ancien hello ne sont synchronisées, la règle de synchronisation hello doit être désactivée comme indiqué.

### <a name="change-an-out-of-box-rule"></a>effectuer des modifications sur une règle out-of-box
Hello que vous devez modifier une règle d’out-of-box étant uniquement lorsque vous avez besoin de règle de jointure toochange hello. Si vous avez besoin de toochange un flux d’attribut, vous devez créer une règle de synchronisation avec une priorité plus élevée que les règles d’out-of-box hello. Hello uniquement de la règle, vous devez pratiquement tooclone est hello **dans depuis AD - jointure utilisateur**. Vous pouvez remplacer toutes les autres règles avec une règle de priorité plus élevée.

Si vous avez besoin de règle d’out-of-box tooan toomake modifications, vous devez faire une copie de la règle d’out-of-box hello et désactive la règle d’origine de hello. Apportez la règle de hello modifications toohello cloné. Hello Éditeur des règles de synchronisation vous aide à ces étapes. Lorsque vous ouvrez une règle out-of-box, cette boîte de dialogue s'affiche :   
![Règle d'avertissement out-of-the box](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/warningoutofboxrule.png)

Sélectionnez **Oui** toocreate une copie de la règle de hello. règle de cloné Hello est ensuite ouvert.  
![Règle clonée](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/clonedrule.png)

Dans cette règle clonée, effectuez toutes les modifications nécessaires tooscope, jointure et des transformations.

## <a name="next-steps"></a>Étapes suivantes
**Rubriques de présentation**

* [Azure AD Connect Sync - Présentation et personnalisation des options de synchronisation](active-directory-aadconnectsync-whatis.md)
* [Intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md)
