---
title: "aaaHow toodelegate d’inscription et de produit abonnement d’utilisateur"
description: "Découvrez comment tooa abonnement toodelegate utilisateur d’inscription et le produit tiers de gestion des API Azure."
services: api-management
documentationcenter: 
author: antonba
manager: erikre
editor: 
ms.assetid: 8b7ad5ee-a873-4966-a400-7e508bbbe158
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 406648db2d2f37c4dcda466294726d331cc0551b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodelegate-user-registration-and-product-subscription"></a>Comment les abonnement toodelegate utilisateur d’inscription et de produit
Délégation contrainte vous permet de toouse votre site Web existant pour la gestion des tooproducts signe-dans/connexion-haut et un abonnement de développeur en tant qu’et non pas les fonctionnalités intégrées de toousing hello dans le portail des développeurs hello. Cela permet à vos données d’utilisateur du site Web tooown hello et effectuer une validation de hello de ces étapes d’une manière personnalisée.

## <a name="delegate-signin-up"></a>Délégation de la connexion et de l’inscription des développeurs
toodelegate développeur tooyour de se connecter et d’abonnement à un site Web existant que vous devez toocreate un point de terminaison spécial de délégation sur votre site qui agit en tant que hello point d’entrée pour cette demande initiée à partir du portail des développeurs gestion des API hello.

flux de travail final Hello seront comme suit :

1. Développeur clique sur le lien de connexion ou d’inscription de hello en hello portail des développeurs gestion des API
2. Navigateur est redirigé toohello point de terminaison de délégation
3. Point de terminaison de délégation redirige en retour tooor présente l’interface utilisateur vous demande utilisateur dans toosign ou d’abonnement
4. En cas de réussite, utilisateur de hello est redirigé toohello arrière gestion des API développeur page du portail de qu'ils ont démarré à partir

toobegin, nous allons premier tooroute de gestion des API de configuration des demandes effectuées avec votre point de terminaison de délégation. Dans le portail de publication de gestion des API hello, cliquez sur **sécurité** puis cliquez sur hello **délégation** onglet. Cliquez sur tooenable de case à cocher hello 'Délégué connexion & d’abonnement'.

![Delegation page][api-management-delegation-signin-up]

* Décider de hello les URL de votre point de terminaison spécial délégation sera être et entrez-la dans hello **URL de point de terminaison de délégation** champ. 
* Au sein de hello **clé d’authentification de délégation** champ Entrez un mot de passe sera utilisé toocompute un tooyou signature fourni pour vérification tooensure qui hello demande provient effectivement gestion des API Azure. Vous pouvez cliquer sur hello **générer** bouton toohave API liste générer de façon aléatoire une clé pour vous.

Maintenant vous devez toocreate hello **point de terminaison de délégation**. Il a tooperform un certain nombre d’actions :

1. Reçoit une demande dans hello suivant du formulaire :
   
   > *http://www.yourwebsite.com/apimdelegation?operation=SignIn&amp;returnUrl={URL of source page}&amp;salt={string}&amp;sig={string}*
   > 
   > 
   
    Paramètres de requête pour les cas de connexion / inscription hello :
   
   * **operation** : identifie le type de demande de délégation. Il ne peut s’agir ici que de **SignIn**
   * **returnUrl**: hello URL de page hello si utilisateur de hello l'clique sur un lien de connexion ou d’abonnement
   * **salt**: chaîne salt spéciale utilisée pour calculer un code de hachage de sécurité.
   * **SIG**: un toobe de hachage calculée de sécurité utilisé pour tooyour de comparaison propre de hachage calculé
2. Vérifiez que demande hello provient de gestion des API Azure (facultatif, mais fortement recommandé pour la sécurité)
   
   * Calculer un hachage HMAC-SHA512 d’une chaîne en fonction de hello **returnUrl** et **salt** des paramètres de requête ([exemple de code ci-dessous]) :
     
     > HMAC(**salt** + ’\n’ + **returnUrl**)
     > 
     > 
   * Comparer la valeur toohello hello hello hachage calculé ci-dessus **sig** paramètre de requête. Si hello deux hachages correspondent, déplacer sur l’étape suivante de toohello, sinon refuser la demande de hello.
3. Vérifiez que vous recevez une demande de connexion dans/la connexion des : hello **opération** paramètre de requête est défini trop «**SignIn**».
4. Utilisateur hello actuel avec l’interface utilisateur dans toosign ou d’abonnement
5. Si l’utilisateur hello est inscription vous avez toocreate un compte correspondant pour eux dans Gestion des API. [Créer un utilisateur] avec hello API REST de gestion des API. Lorsque vous procédez ainsi, vous assurer que hello utilisateur ID toohello même qu'il se trouve dans votre magasin de l’utilisateur ou l’ID de tooan que vous pouvez effectuer le suivi de.
6. Lorsque l’utilisateur de hello est authentifié avec succès :
   
   * [demander un jeton de single-sign-on (SSO)] via l’API REST de gestion des API de hello
   * Ajouter un toohello de paramètre de requête returnUrl URL SSO que vous avez reçu de l’appel d’API de hello ci-dessus :
     
     > Par exemple, https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url 
     > 
     > 
   * redirection hello utilisateur toohello ci-dessus produit URL

En outre toohello **SignIn** opération, vous pouvez également effectuer la gestion des comptes en suivant les étapes précédentes hello et en utilisant l’une des hello opérations suivantes.

* **ChangePassword**
* **ChangeProfile**
* **CloseAccount**

Vous devez passer hello suivant les paramètres de requête pour les opérations de gestion de compte.

* **operation**: identifie le type de demande de délégation dont il s’agit (ChangePassword, ChangeProfile ou CloseAccount)
* **userId**: id d’utilisateur hello de hello compte toomanage
* **salt**: chaîne salt spéciale utilisée pour calculer un code de hachage de sécurité.
* **SIG**: un toobe de hachage calculée de sécurité utilisé pour tooyour de comparaison propre de hachage calculé

## <a name="delegate-product-subscription"></a>Délégation de l’abonnement aux produits
Délégation de l’abonnement du produit fonctionne de façon similaire toodelegating utilisateur connectez-vous/à distance. flux de travail final Hello devrait se présenter comme suit :

1. Développeur sélectionne un produit dans le portail des développeurs gestion des API hello et clique sur le bouton d’abonnement hello
2. Navigateur est redirigé toohello point de terminaison de délégation
3. Point de terminaison de délégation effectue les étapes d’abonnement de produit requis - il s’agit des tooyou et peut entraîner de redirection tooanother page toorequest, informations de facturation, poser des questions supplémentaires, ou simplement le stockage d’informations de hello et ne pas nécessitant une action de l’utilisateur

fonctionnalités de hello tooenable, sur hello **délégation** page, cliquez sur **déléguer abonnement**.

Puis vérifiez le point de terminaison de délégation hello effectue hello suivant des actions :

1. Reçoit une demande dans hello suivant du formulaire :
   
   > *http://www.yourwebsite.com/apimdelegation?Operation= {opération} & productId = {toosubscribe produit à} & userId = {user demande} & salt = {string} & sig = {string}*
   > 
   > 
   
    Paramètres de requête pour les cas d’abonnement hello produit :
   
   * **operation**: identifie le type de demande de délégation. Pour un abonnement demandes hello les options valides sont :
     * « S’abonner » : un toosubscribe de demande hello tooa utilisateur donnée produit avec fourni d’ID (voir ci-dessous)
     * « Vous désabonner » : un toounsubscribe demande un utilisateur à partir d’un produit
     * « Renouveler » : un toorenew demande un abonnement (par exemple, qui peut être expirer)
   * **productId**: hello des ID d’utilisateur de hello hello produit demandé toosubscribe à
   * **userId**: hello ID d’utilisateur hello pour lequel hello est demandé
   * **salt**: chaîne salt spéciale utilisée pour calculer un code de hachage de sécurité.
   * **SIG**: un toobe de hachage calculée de sécurité utilisé pour tooyour de comparaison propre de hachage calculé
2. Vérifiez que demande hello provient de gestion des API Azure (facultatif, mais fortement recommandé pour la sécurité)
   
   * Calcul d’un code HMAC-SHA512 d’une chaîne en fonction de hello **productId**, **userId** et **salt** des paramètres de requête :
     
     > HMAC(**salt** + ’\n’ + **productId** + ’\n’ + **userId**)
     > 
     > 
   * Comparer la valeur toohello hello hello hachage calculé ci-dessus **sig** paramètre de requête. Si hello deux hachages correspondent, déplacer sur l’étape suivante de toohello, sinon refuser la demande de hello.
3. Exécuter tout traitement d’abonnement de produit en fonction de type hello de l’opération demandée dans **opération** -par exemple, la facturation, d’autres questions, etc..
4. Sur l’abonnement avec succès les produits de toohello hello utilisateur de votre côté, abonnez-vous au produit de gestion des API hello utilisateurs toohello par [hello appel API REST pour l’abonnement].

## <a name="delegate-example-code"></a> Exemple de Code
Ces afficher des exemples de code comment tootake hello *clé de validation de délégation*toocreate un code HMAC qui est ensuite utilisé toovalidate hello signature, ce qui prouve validité hello Hello, qui est défini dans l’écran de délégation hello du portail de publication hello returnUrl passé. Hello même code fonctionne pour hello productId et userId légères modifications.

**Hachage toogenerate code c# de returnUrl**

```c#
using System.Security.Cryptography;

string key = "delegation validation key";
string returnUrl = "returnUrl query parameter";
string salt = "salt query parameter";
string signature;
using (var encoder = new HMACSHA512(Convert.FromBase64String(key)))
{
    signature = Convert.ToBase64String(encoder.ComputeHash(Encoding.UTF8.GetBytes(salt + "\n" + returnUrl)));
    // change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
    // compare signature toosig query parameter
}
```

**Hachage toogenerate NodeJS code returnUrl**

```
var crypto = require('crypto');

var key = 'delegation validation key'; 
var returnUrl = 'returnUrl query parameter';
var salt = 'salt query parameter';

var hmac = crypto.createHmac('sha512', new Buffer(key, 'base64'));
var digest = hmac.update(salt + '\n' + returnUrl).digest();
// change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
// compare signature toosig query parameter

var signature = digest.toString('base64');
```

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur la délégation, consultez hello suivant vidéo.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Delegating-User-Authentication-and-Product-Subscription-to-a-3rd-Party-Site/player]
> 
> 

[Delegating developer sign-in and sign-up]: #delegate-signin-up
[Delegating product subscription]: #delegate-product-subscription
[demander un jeton de single-sign-on (SSO)]: http://go.microsoft.com/fwlink/?LinkId=507409
[create a user]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser
[hello appel API REST pour l’abonnement]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO
[Next steps]: #next-steps
[exemple de code ci-dessous]: #delegate-example-code

[api-management-delegation-signin-up]: ./media/api-management-howto-setup-delegation/api-management-delegation-signin-up.png 
