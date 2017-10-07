---
title: "aaaAzure Active Directory groupe-licences basées sur des scénarios supplémentaires | Documents Microsoft"
description: "Plus de scénarios pour la licence basée sur le groupe Azure Active Directory"
services: active-directory
keywords: Gestion des licences Azure AD
documentationcenter: 
author: curtand
manager: femila
editor: piotrci
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/02/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 782b7c9aa1c062a55c1241d69af673466f7a849c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-limitations-and-known-issues-using-groups-toomanage-licensing-in-azure-active-directory"></a>Scénarios, limitations et problèmes connus liés à l’aide du Gestionnaire de licences toomanage groupes dans Azure Active Directory

Utilisez hello suivant des informations et des exemples toogain une plus grande maîtrise du contrat de licence basé sur un groupe Azure Active Directory (Azure AD).

## <a name="usage-location"></a>Emplacement d’utilisation

Certains services Microsoft ne sont pas disponibles dans tous les emplacements. Avant de tooa utilisateur peut être affectée à une licence, administrateur de hello a toospecify hello **l’emplacement d’utilisation** propriété sur l’utilisateur de hello. Dans [hello portail Azure](https://portal.azure.com), vous pouvez spécifier dans **utilisateur** &gt; **profil** &gt; **paramètres**.

Pour l’attribution de licence de groupe, tous les utilisateurs sans un emplacement d’utilisation spécifié héritera emplacement hello du répertoire de hello. Si vous avez des utilisateurs dans plusieurs emplacements, assurez-vous que tooreflect qui correctement dans vos objets de l’utilisateur avant d’ajouter toogroups les utilisateurs dont les licences.

> [!NOTE]
> L’affectation d’une licence de groupe n’a jamais pour effet de modifier une valeur d’emplacement d’utilisation existante sur un utilisateur. Nous vous recommandons de toujours activer l’emplacement d’utilisation dans le cadre de votre flux de création d’utilisateur dans Azure AD (par exemple, via la configuration AAD Connect) - qui garantira hello résultat de l’attribution de licence est toujours correct, et les utilisateurs ne reçoivent pas de services dans les emplacements qui ne sont pas autorisé.

## <a name="use-group-based-licensing-with-dynamic-groups"></a>Utilisation de la gestion des licences par groupe avec des groupes dynamiques

Vous pouvez utiliser la gestion des licences par groupe avec n’importe quel groupe de sécurité, ce qui signifie que vous pouvez la combiner avec des groupes dynamiques Azure AD. Groupes dynamiques exécuter les règles par rapport à l’utilisateur objet attributs tooautomatically ajoutent et supprimer des utilisateurs de groupes.

Par exemple, vous pouvez créer un groupe dynamique pour un jeu de produits vous souhaitez tooassign toousers. Chaque groupe est rempli par une règle d’ajout d’utilisateurs par leurs attributs, et chaque groupe est licences attribuées hello que vous voulez tooreceive. Vous pouvez affecter hello attribut locale et synchroniser avec Azure AD, ou vous pouvez gérer attribut hello directement dans le cloud de hello.

Licences sont attribuées toohello utilisateur peu de temps après que les avoir ajoutés toohello groupe. Lorsque l’attribut de hello est modifié, les groupes hello de départ de l’utilisateur hello et licences de hello sont supprimés.

### <a name="example"></a>Exemple

Considérez l’exemple hello d’une solution de gestion d’identité locale qui détermine quels utilisateurs doivent avoir accès tooMicrosoft web services. Il utilise **extensionAttribute1** toostore une valeur de chaîne qui représentent des licences hello hello utilisateur doit avoir. Azure AD Connect la synchronise avec Azure AD.

Des utilisateurs peuvent avoir besoin d’une licence mais pas d’une autre, ou avoir besoin des deux. Voici un exemple, dans lequel vous distribuez Office 365 entreprise E5 et Enterprise Mobility + Security (EMS) toousers dans des groupes de licences :

#### <a name="office-365-enterprise-e5-base-services"></a>Office 365 Enterprise E5 : services de base

![Capture d’écran des services de base Office 365 Enterprise E5](media/active-directory-licensing-group-advanced/o365-e5-base-services.png)

#### <a name="enterprise-mobility--security-licensed-users"></a>Enterprise Mobility + Security : utilisateurs sous licence

![Capture d’écran des utilisateurs sous licence Enterprise Mobility + Security](media/active-directory-licensing-group-advanced/o365-e5-licensed-users.png)

Pour cet exemple, un utilisateur de modifier et définir leur valeur toohello extensionAttribute1 `EMS;E5_baseservices;` si vous souhaitez hello utilisateur toohave les deux licences. Vous pouvez effectuer cette modification localement. Après avoir hello modifier se synchronise avec le cloud de hello, hello utilisateur est automatiquement ajouté tooboth groupes et licences sont attribuées.

![Capture d’écran montrant comment tooset hello extensionAttribute1 de l’utilisateur](media/active-directory-licensing-group-advanced/user-set-extensionAttribute1.png)

> [!WARNING]
> Faites preuve de vigilance lorsque vous modifiez la règle d’appartenance au groupe existante. Lorsqu’une règle est modifiée, appartenance hello du groupe de hello seront réévaluée et les utilisateurs qui ne correspondent plus hello nouvelle règle sera supprimée (utilisateurs toujours correspondre à la nouvelle règle de hello ne seront pas affectées au cours du processus). Ces utilisateurs auront leurs licences supprimées pendant hello qui peut entraîner une perte de service, ou dans certains cas, une perte de données.

> Si vous avez un grand groupe dynamique dépendent de l’attribution de licence, pensez à valider les changements importants sur un plus petit groupe de test avant de les appliquer groupe principal de toohello.

## <a name="multiple-groups-and-multiple-licenses"></a>Plusieurs groupes et plusieurs licences

Un utilisateur peut être membre de plusieurs groupes avec des licences. Voici certains tooconsider choses :

- Plusieurs licences pour aboutir hello même produit peut se chevaucher et ils toutes activées en cours toohello appliqué utilisateur des services. Hello suivant montre deux groupes de licences : *les services de base E3* contient hello foundation toodeploy tout d’abord, tooall les utilisateurs des services. Et *E3 services étendus* contient des services supplémentaires (balancement et Planner) toodeploy seuls toosome les utilisateurs. Dans cet exemple, utilisateur de hello a été ajouté tooboth groupes :

  ![Capture d’écran des services activés](media/active-directory-licensing-group-advanced/view-enabled-services.png)

  Par conséquent, utilisateur de hello a 7 des services de 12 hello produit hello activé, lors de l’utilisation qu’une licence pour ce produit.

- En sélectionnant hello *E3* licence affiche plus de détails, notamment des informations sur les groupes a provoqué le toobe services activée pour l’utilisateur de hello.

  ![Capture d’écran des services activés par groupe](media/active-directory-licensing-group-advanced/view-enabled-service-by-group.png)

## <a name="direct-licenses-coexist-with-group-licenses"></a>Coexistence de licences directes avec des licences de groupe

Lorsqu’un utilisateur hérite d’une licence à partir d’un groupe, vous ne peut pas directement supprimer ou modifier cette attribution de licence dans les propriétés de l’utilisateur hello. Modifications doivent être effectuées dans le groupe de hello et ensuite propagées tooall utilisateurs.

Il est possible, cependant, tooassign hello même licence produit directement toohello utilisateur, dans Ajout toohello héritée de licence. Vous pouvez activer des services supplémentaires à partir du produit hello uniquement pour un utilisateur, sans affecter d’autres utilisateurs.

Des licences attribuées directement peuvent être supprimées sans que cela affecte les licences héritées. Prenons l’utilisateur de hello qui hérite d’une licence Office 365 entreprise E3 à partir d’un groupe.

1. Au départ, utilisateur de hello hérite de licence de hello uniquement hello *les services de base E3* groupe, ce qui permet aux quatre plans de service, comme indiqué :

  ![Capture d’écran des services activés par groupe E3](media/active-directory-licensing-group-advanced/e3-group-enabled-services.png)

2. Vous pouvez sélectionner **affecter** toodirectly affecter un utilisateur toohello E3. Dans ce cas, vous allez toodisable service tous les plans à l’exception de Yammer l’entreprise :

  ![Capture d’écran de façon tooassign une licence directement tooa utilisateur](media/active-directory-licensing-group-advanced/assign-license-to-user.png)

3. Par conséquent, hello utilisateur continue à utiliser uniquement une licence de produit de E3 hello. Mais affectation directe de hello hello service Yammer une entreprise pour cet utilisateur uniquement. Vous pouvez voir quels services sont activés par l’appartenance au groupe de hello et affectation directe de hello :

  ![Capture d’écran de l’affectation héritée et directe](media/active-directory-licensing-group-advanced/direct-vs-inherited-assignment.png)

4. Lorsque vous utilisez une assignation directe, hello opérations suivantes est autorisée :

  - Yammer Qu'enterprise peut être désactivé sur l’objet utilisateur de hello directement. Hello **désactivez-les** bascule dans l’illustration de hello a été activée pour ce service, en opposition toohello autres bascules de service. Étant donné que le service de hello est activé directement sur l’utilisateur de hello, elle peut être modifiée.
  - Services supplémentaires peuvent être activées, dans le cadre de hello directement attribué des licences.
  - Hello **supprimer** bouton peut être utilisé tooremove hello direct licence utilisateur de hello. Vous pouvez voir que hello utilisateur uniquement a maintenant licence de groupe hérité hello et uniquement les services d’origine hello restent activés :

    ![Capture d’écran montrant comment tooremove directe affectation](media/active-directory-licensing-group-advanced/remove-direct-license.png)

## <a name="managing-new-services-added-tooproducts"></a>La gestion des services de nouveau ajouté tooproducts
Lorsque Microsoft ajoute un nouveau produit tooa de service, elle est activée par défaut dans tous les groupes toowhich que vous avez affectés licence hello. Utilisateurs sont abonnées toonotifications sur les modifications du produit dans votre client recevra des e-mails à l’avance pour les informer sur les compléments hello imminente du service.

En tant qu’administrateur, vous pouvez passer en revue tous les groupes affectés par la modification de hello et effectuer une action, par exemple la désactivation du nouveau service de hello dans chaque groupe. Par exemple, si vous avez créé des groupes ciblant uniquement des services spécifiques pour le déploiement, vous pouvez réexaminer ces groupes pour vous assurer que les nouveaux services ajoutés sont désactivés.

Voici un exemple de ce à quoi ce processus peut ressembler :

1. À l’origine, vous avez affecté hello *Office 365 entreprise E5* groupes tooseveral de produits. Un de ces groupes, appelés *O365 E5 - Exchange uniquement* a été conçue tooenable les hello uniquement *Exchange Online (Plan 2)* service pour ses membres.

2. Vous avez reçu une notification de Microsoft qui hello E5 produit sera étendu avec un nouveau service - *Microsoft Stream*. Lorsque le service de hello devient disponible dans votre client, vous pouvez effectuer les suivant hello :

3. Accédez toohello [ **Azure Active Directory > licences > tous les produits** ](https://portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Products) panneau et sélectionnez *Office 365 entreprise E5*, puis sélectionnez **concédé sous licence de groupes**  tooview une liste de tous les groupes avec le produit.

4. Cliquez sur le groupe de hello souhaité tooreview (dans ce cas, *O365 E5 - Exchange uniquement*). Cela ouvre hello **licences** onglet. Cliquez sur la licence de E5 hello pour ouvrir un panneau qui répertorie tous les services activés.
> [!NOTE]
> Hello *Microsoft Stream* service a été automatiquement ajouté et activé dans ce groupe, en plus toohello *Exchange Online* service :

  ![Capture d’écran du nouveau service ajouté la licence de groupe tooa](media/active-directory-licensing-group-advanced/manage-new-services.png)

5. Si vous souhaitez toodisable hello nouveau service de ce groupe, cliquez sur hello **désactivez-les** activer/désactiver le service toohello suivant et cliquez sur hello **enregistrer** bouton de modification de hello tooconfirm. Azure AD va maintenant traiter tous les utilisateurs de la modification de hello tooapply hello groupe ; tous les nouveaux utilisateurs ajoutés toohello groupe n’aura pas hello *Microsoft Stream* service est activé.

  > [!NOTE]
  > Les utilisateurs devront peut-être toujours service hello activée par le biais des autres attribution de licence (un autre groupe qu’ils sont membres ou à une attribution de licence direct).

6. Si nécessaire, effectuez hello affecté de la même procédure pour d’autres groupes avec ce produit.

## <a name="use-powershell-toosee-who-has-inherited-and-direct-licenses"></a>Utilisez toosee PowerShell qui a hérité et diriger les licences
Vous pouvez utiliser un toocheck de script PowerShell si les utilisateurs disposent d’une licence directement affectée ou héritée d’un groupe.

1. Exécutez hello `connect-msolservice` tooauthenticate de l’applet de commande et se connecter tooyour client.

2. `Get-MsolAccountSku`peut être utilisé toodiscover toutes les licences de produit approvisionnés dans le locataire de hello.

  ![Capture d’écran de l’applet de commande Get-Msolaccountsku de hello](media/active-directory-licensing-group-advanced/get-msolaccountsku-cmdlet.png)

3. Hello d’utilisation *AccountSkuId* valeur licence hello vous intéressez avec [ce script PowerShell](./active-directory-licensing-ps-examples.md#check-if-user-license-is-assigned-directly-or-inherited-from-a-group). Cela génère une liste d’utilisateurs qui ont cette licence avec hello plus d’informations sur la licence de hello est attribuée.

## <a name="use-audit-logs-toomonitor-group-based-licensing-activity"></a>Utilisez Audit journaux toomonitor basée sur le groupe gestion des licences activité

Vous pouvez utiliser [AD Azure des journaux d’audit](./active-directory-reporting-activity-audit-logs.md#audit-logs) toosee toutes les activités liées toogroup concession de licence, y compris :
- qui a modifié les licences attribuées aux groupes ;
- Lorsque le système de hello a démarré le traitement d’une modification de licence de groupe et, une fois terminée
- les modifications de licence ont été apportées utilisateur tooa à la suite d’une attribution de licence de groupe.

>[!NOTE]
> Journaux d’audit sont disponibles sur la plupart des panneaux Bonjour section Azure Active Directory du portail de hello. Selon l’endroit où vous y accédez, les filtres peuvent être tooonly applique afficher le contexte de toohello pertinentes activité du Panneau de hello. Si vous ne voyez pas les résultats hello attendus, examinez [hello des options de filtrage](./active-directory-reporting-activity-audit-logs.md#filtering-audit-logs) ou accéder aux journaux d’audit hello non filtré sous [ **Azure Active Directory > activité > journaux d’Audit** ](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Audit).

### <a name="find-out-who-modified-a-group-license"></a>Déterminer qui a modifié une licence de groupe

1. Ensemble hello **activité** trop de filtre*ensemble groupe licence* et cliquez sur **appliquer**.
2. les résultats de Hello incluent tous les cas de licences qui est définie ou modifiée sur les groupes.
>[!TIP]
> Vous pouvez également taper le nom hello du groupe de hello Bonjour *cible* filtrer les résultats de hello tooscope.

3. Cliquez sur un élément hello liste Afficher toosee hello les détails de ce qui a changé. Sous *les propriétés modifiées* anciennes et nouvelles valeurs pour l’attribution de licence hello sont répertoriées.

Voici un exemple de modifications récentes de licence groupe, avec des détails :

![Capture d’écran de modifications de licence de groupe](media/active-directory-licensing-group-advanced/audit-group-license-change.png)

### <a name="find-out-when-group-changes-started-and-finished-processing"></a>Déterminer quand le traitement de modifications de groupe a commencé et s’est terminé

Lorsqu’il modifie une licence sur un groupe, Azure AD démarre l’application hello modifications tooall utilisateurs.

1. toosee au démarrage de groupes de traitement, définissez hello **activité** trop de filtre*commencer à appliquer les toousers de licence de groupe en fonction*. Notez l’acteur hello pour hello opération est *Microsoft Azure AD basée sur le groupe de licences* -un système de compte qui est utilisé tooexecute toutes les modifications de licence de groupe.
>[!TIP]
> Cliquez sur un élément Bonjour de hello liste toosee *les propriétés modifiées* champ - il affiche les modifications de licence hello qui ont été sélectionnées pour le traitement. Cela est utile si le groupe de tooa plusieurs modifications et que vous vous n’êtes pas sûr de l’application a été traitée.

2. De même, toosee lorsque groupes terminé le traitement, utiliser des valeurs de filtre hello *finissez toousers de licence de groupe en fonction*.
>[!TIP]
> Dans ce cas, hello *les propriétés modifiées* champ contient un résumé des résultats de hello - cela est utile tooquickly vérification si le traitement a généré des erreurs. Exemple de sortie :
> ```
Modified Properties
...
Name : Result
Old Value : []
New Value : [Users successfully assigned licenses: 6, Users for whom license assignment failed: 0.];
> ```

3. toosee hello complet du journal de la façon dont un groupe a été traité, y compris toutes les modifications de l’utilisateur, définissez hello suivant filtres :
  - **Initié par (acteur)** : « Microsoft Azure AD Group-Based Licensing ».
  - **Plage de dates** (facultatif) : plage personnalisée indiquant quand, à votre connaissance, le traitement d’un groupe spécifique a commencé et s’est terminé.

Cet exemple de sortie montre début hello du traitement, résultant de toutes les modifications de l’utilisateur et hello de fin du traitement.

![Capture d’écran de modifications de licence de groupe](media/active-directory-licensing-group-advanced/audit-group-processing-log.png)

>[!TIP]
> En cliquant sur les éléments liés trop*licence d’utilisateur de modification* afficher les détails pour les modifications appliquées tooeach utilisateur individuels.

## <a name="limitations-and-known-issues"></a>Limitations et problèmes connus

Si vous utilisez basée sur le groupe de licences, c’est une bonne idée toofamiliarize vous-même avec hello suivant la liste des limitations et problèmes connus.

- Actuellement, la gestion des licences par groupe ne prend pas en charge les groupes contenant d’autres groupes. Si vous appliquez un groupe imbriqué tooa de licence, seuls les membres de premier niveau immédiate de l’utilisateur hello du groupe de hello posséder des licences hello appliquées.

- Hello fonctionnalité peut uniquement être utilisée avec des groupes de sécurité. Groupes d’Office ne sont actuellement pas pris en charge et vous ne serez pas en mesure de toouse dans le processus d’attribution de licence de hello.

- Hello [portail d’administration d’Office 365](https://portal.office.com ) ne prend pas en charge basée sur le groupe de licences. Si un utilisateur hérite d’une licence à partir d’un groupe, cette licence s’affiche dans le portail d’administration Office hello en tant qu’une licence d’utilisateur standard. Si vous essayez toomodify de licence ou essayez de licence de hello tooremove, portail de hello renvoie un message d’erreur. Les licences de groupe héritées ne peuvent pas être modifiées directement sur un utilisateur.

- Lorsqu’un utilisateur est supprimé d’un groupe et perd la licence de hello, plans de service hello à partir de cette licence (par exemple, SharePoint Online) sont définies tooa **Suspended** état. Hello plans de service ne sont pas définies tooa final, l’état désactivé. Cette précaution permet d’éviter une suppression accidentelle de données utilisateur si un administrateur commet une erreur dans la gestion de l’appartenance au groupe.

- Lorsque des licences sont attribuées ou modifiées pour un groupe de grande taille (par exemple, 100 000 utilisateurs), cela peut affecter les performances. Plus précisément, volume hello des modifications généré par l’automatisation d’Azure AD peut nuire aux performances hello votre synchronisation d’annuaires entre Azure AD et systèmes locaux.

- Automation de gestion de licence ne réagit pas automatiquement les types tooall des modifications dans un environnement de hello. Par exemple, vous pouvez exécuter plus de licences, à l’origine de certaines toobe d’utilisateurs dans un état d’erreur. toofree de nombre de sièges disponibles de hello, vous pouvez supprimer certaines licences attribuées directement à partir d’autres utilisateurs. Toutefois, système de hello ne pas réagir toothis modifier et résoudre automatiquement les utilisateurs dans cet état d’erreur.

  Comme un contournement toothese les types de limites, vous pouvez accéder toohello **groupe** panneau dans Azure AD, puis cliquez sur **retraiter**. Cette commande traite tous les utilisateurs de ce groupe et résout les États d’erreur hello, si possible.

- Basé sur le groupe de licences n’enregistre pas les erreurs lors d’une licence ne peut pas être attribuée utilisateur tooa en raison de la configuration de l’adresse proxy en double tooa dans Exchange Online ; ces utilisateurs sont ignorés au cours de l’attribution de licence. Pour plus d’informations sur la façon tooidentify et résoudre ce problème, consultez [cette section](./active-directory-licensing-group-problem-resolution-azure-portal.md#license-assignment-fails-silently-for-a-user-due-to-duplicate-proxy-addresses-in-exchange-online).

## <a name="next-steps"></a>Étapes suivantes

toolearn en savoir plus sur les autres scénarios de gestion des licences via le groupe de licences, consultez :

* [What is group-based licensing in Azure Active Directory? (Présentation des licences basées sur le groupe dans Azure Active Directory)](active-directory-licensing-whatis-azure-portal.md)
* [Affectation d’un groupe de tooa de licences dans Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md)
* [Identification et résolution des problèmes de licence pour un groupe dans Azure Active Directory](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Comment toomigrate individuels titulaires d’une licence dans Azure Active Directory en fonction des toogroup](active-directory-licensing-group-migration-azure-portal.md)
