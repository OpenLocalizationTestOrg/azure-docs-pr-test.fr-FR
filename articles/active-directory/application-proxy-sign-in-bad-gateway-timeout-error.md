---
title: "AAA » ne peut pas accéder à cette erreur de l’Application d’entreprise lorsque vous utilisez une application de Proxy d’Application | Documents Microsoft »"
description: "Comment les accès commun tooresolve problèmes avec les applications du Proxy d’Application Azure AD."
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 490b106b7d774ee43fc076cc5d082997a1df85e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="cant-access-this-corporate-application-error-when-using-an-application-proxy-application"></a>Erreur « Impossible d’accéder à cette application d’entreprise » lors de l’utilisation d’une application Proxy d’application

Cet article vous a-t-il tootroubleshoot des problèmes courants rencontrés lorsque vous voyez une erreur « cette application d’entreprise n’est pas accessible » sur une application de Proxy d’Application Azure AD.

## <a name="overview"></a>Vue d'ensemble
Lorsque vous voyez cette erreur, page de hello partagent également un code d’état. Ce code est probablement de l’une des manières suivantes les hello :

-   **Délai d’attente de la passerelle**: hello service Proxy d’Application est le connecteur de hello tooreach impossible. En règle générale, cela indique un problème avec affectation de connecteur hello, connecteur proprement dit ou hello autour de connecteur de hello, les règles de mise en réseau.

-   **Passerelle incorrecte**: connecteur de hello est l’application principale ne peut pas tooreach hello. Cela peut indiquer une configuration incorrecte de l’application hello.

-   **Il est interdit**: utilisateur de hello n’est pas autorisé tooaccess hello application. Cela peut se produire lorsque l’utilisateur de hello ne possède pas d’application toohello dans Azure Active Directory, ou si sur hello principal utilisateur de hello n’a pas d’application de hello tooaccess autorisation.

code de hello toofind, examinez le texte hello en hello en bas à gauche de message d’erreur hello pour le champ de « Code d’état » hello. Recherchez également les notes à hello tout en bas du page hello avec des conseils supplémentaires.

   ![Erreur liée au dépassement du délai de la passerelle](./media/application-proxy/connection-problem.png)

Pour plus d’informations sur comment tootroubleshoot hello cause première de ces erreurs et plus de détails sur les suggestions de correction, voir hello correspondants ci-dessous.

## <a name="gateway-timeout-errors"></a>Erreurs liées au dépassement du délai de la passerelle

Un délai d’attente de la passerelle se produit lorsque le service de hello essaie de connecteur de hello tooreach et est la fenêtre de délai d’attente hello toowithin impossible. Cela est généralement dû à une application affectée tooa groupe de connecteurs avec aucun connecteur de travail, ou certains ports requis par hello connecteur ne sont pas ouverts.


## <a name="bad-gateway-errors"></a>Erreurs liées à une passerelle incorrecte

Une erreur de passerelle incorrecte indique que le connecteur hello est l’application principale ne peut pas tooreach hello. Assurez-vous que vous avez publié d’application correct hello. Erreurs courantes à l’origine de ce problème :

-   Une faute de frappe ou d’une erreur dans une URL interne hello

-   Ne pas de publication racine hello application hello. Par exemple, la publication <http://expenses/reimbursement> , mais la tentative de tooaccess <http://expenses>

-   Problèmes liés à la configuration de la délégation Kerberos (KCD) hello

-   Problèmes liés à l’application hello principale

## <a name="forbidden-errors"></a>Erreurs liées à une interdiction

Si vous voyez une erreur interdit, hello utilisateur n'a pas reçu toohello application. Cela peut être dans Azure Active Directory ou sur l’application hello principale.

toolearn tooassign utilisateurs toohello application dans Azure, voir hello [documentation de configuration](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal#add-a-test-user).

Si vous confirmez les utilisateur hello sont attribué application toohello dans Azure, vérifiez la configuration de l’utilisateur dans l’application principale hello hello. Si vous utilisez la délégation Kerberos contrainte ou l’authentification Windows intégrée, consultez notre page de dépannage consacrée à la délégation Kerberos contrainte pour obtenir des instructions.

## <a name="check-hello-applications-internal-url"></a>Vérifier l’URL interne de l’application hello

Une première étape rapide, vérifiez vérifier et corriger les URL interne de hello en ouvrant l’application hello via **des Applications d’entreprise**, puis en sélectionnant hello **le Proxy d’Application** menu. Vérifiez qu’est bonne URL interne hello hello celui utilisé à partir de l’application hello tooaccess de votre réseau local.

## <a name="check-hello-application-is-assigned-tooa-working-connector-group"></a>Vérifier l’application hello est attribuée tooa connecteur de groupe de travail

application de hello tooverify est attribuée tooa connecteur de groupe de travail :

1.  Ouvrez l’application hello dans le portail de hello en accédant trop**Azure Active Directory**, en cliquant sur **des Applications d’entreprise**, puis **toutes les Applications.** Ouvrez l’application hello, puis sélectionnez **le Proxy d’Application** à partir du menu de gauche hello.

2.  Examinez le champ de groupe de connecteurs hello. S’il n’y a aucun connecteur active dans le groupe de hello, vous voyez un avertissement. Si vous ne voyez pas tous les avertissements, passez trop « vérifier tous les ports requis sont dans la liste approuvée ».

3.  S’il s’agit hello mauvais groupe de connecteur, hello déroulante groupe approprié de tooselect hello et Confirmez vous ne voyez plus les avertissements. S’il s’agit hello destinée groupe de connecteurs, cliquez sur la page hello avertissement message tooopen hello avec la gestion du connecteur.

4.  À ce stade, il existe quelques toodrill manières dans supplémentaire :

  * Déplacez un connecteur actif dans hello : Si vous avez un connecteur actif qui doit appartenir toothis groupe et qui possède l’application de ligne de vue toohello cible principale, vous pouvez déplacer hello connecteur dans le groupe de hello attribué. toodo, cliquez sur hello connecteur. Dans le champ de « Groupe de connecteurs » hello, utilisez groupe approprié du hello hello tooselect de liste déroulante, cliquez sur Enregistrer.

  * Télécharger un nouveau connecteur pour ce groupe : à partir de cette page, vous pouvez obtenir le lien de hello trop[télécharger un nouveau connecteur](https://download.msappproxy.net/Subscription/d3c8b69d-6bf7-42be-a529-3fe9c2e70c90/Connector/Download). besoins du connecteur Hello toobe installé sur un ordinateur avec l’application de ligne de vue directe toohello principale et se trouve généralement sur hello même serveur que l’application hello. Hello d’utilisation télécharger toodownload de lien de connecteur un connecteur sur l’ordinateur cible hello. Ensuite, cliquez sur hello connecteur et utiliser hello « Groupe de connecteurs » liste déroulante toomake qu’il appartient toohello des groupes appropriés.

  * Examiner un connecteur inactif : si un connecteur apparaît comme étant inactif, elle est service de hello tooreach impossible. C’est généralement en raison de ports toosome requis bloqués. toosolve ce problème, le déplacement de trop « vérifier tous les ports requis sont dans la liste approuvée ».

Une fois ces étapes application hello de tooensure est groupe tooa attribué avec l’utilisation de connecteurs, application hello test. Si elle ne fonctionne toujours pas, continuer toohello la prochaine section.

## <a name="check-all-required-ports-are-whitelisted"></a>Vérifier que tous les ports nécessaires figurent dans la liste verte

tooverify que tous les requis ports sont ouverts, consultez notre documentation sur l’ouverture des ports. Si tous les ports hello nécessaires sont ouverts, déplacez toohello la prochaine section.

## <a name="check-for-other-connector-errors"></a>Rechercher d’autres erreurs liées aux connecteurs

Si aucun des hello ci-dessus résoudre hello, hello prochaine étape consiste toolook des problèmes ou des erreurs avec hello connecteur proprement dit. Vous pouvez voir des erreurs courantes Bonjour [dépannage document](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot#connector-errors). 

Vous pouvez également consulter directement hello connecteur journaux tooidentify toutes les erreurs. Un grand nombre des messages d’erreur être en mesure de tooshare recommandations plus spécifiques pour les correctifs. toolearn Voir journaux hello tooview [notre documentation connecteurs](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors#under-the-hood).

## <a name="additional-resolutions"></a>Résolutions supplémentaires

Si hello ci-dessus n’a pas de résoudre hello, il existe quelques différentes causes possibles. problème de hello tooidentify :

Si votre application est configurée toouse Windows authentification intégrée, application hello de test sans l’authentification unique. Si ce n’est pas le cas, déplacez le paragraphe suivant toohello. application de hello toocheck sans l’authentification unique, ouvrez votre application via **des Applications d’entreprise,** et toohello **Single Sign-On** menu. Hello de modification liste déroulante à partir de le « authentification Windows intégrée » trop « Azure AD single sign-on disabled ». 

Ouvrez un navigateur et essayez l’application hello tooaccess. Vous devez être invité à s’authentifier et accéder à l’application hello. Si cela fonctionne, problème de hello est avec la configuration de la délégation Kerberos (KCD) hello permettant hello l’authentification unique. Voir page de résoudre les problèmes de KCD hello.

Si vous continuez d’erreur de hello toosee, accédez à toohello machine où hello connecteur est installé, ouvrez un navigateur et la tentative de tooreach hello URL interne utilisée pour l’application hello. Hello connecteur agit comme un autre client de hello même ordinateur. Si vous ne pouvez atteindre l’application hello, cherchez à savoir pourquoi cet ordinateur est application hello de tooreach impossible, ou utiliser un connecteur sur un serveur qui est en mesure de tooaccess hello application.

Si vous pouvez accéder à application hello sur cet ordinateur, toolook des problèmes ou des erreurs avec hello connecteur proprement dit. Vous pouvez voir des erreurs courantes Bonjour [dépannage document](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot#connector-errors). Vous pouvez également consulter directement hello connecteur journaux tooidentify toutes les erreurs. Un grand nombre des messages d’erreur être en mesure de tooshare recommandations plus spécifiques pour les correctifs. toolearn Voir journaux hello tooview [notre documentation connecteurs](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors#under-the-hood).

## <a name="next-steps"></a>Étapes suivantes
[Présentation des connecteurs de proxy d’application Azure AD](application-proxy-understand-connectors.md)
