---
title: "aaaHow tooconfigure un toouse d’application de Proxy d’Application la délégation contrainte Kerberos | Documents Microsoft"
description: "Comment tooconfigure la délégation contrainte Kerberos pour une application de Proxy d’Application Azure AD."
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
ms.openlocfilehash: 93dac264ff1d3b99dead1d9c759c37c59373cbd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-application-proxy-application-toouse-kerberos-constrained-delegation"></a>Comment tooconfigure un toouse d’application de Proxy d’Application la délégation contrainte Kerberos

Bonjour les méthodes disponibles pour atteindre une toopublished SSO applications peuvent varier quelque peu de tooapplication de l’application et une des options hello que le Proxy d’Application Azure offre dès la hello est la délégation Kerberos (KCD). C’est là un hôte de connecteur configuré tooperform contraint kerberos authentification toobackend applications, pour le compte d’utilisateurs.

procédure réel de Hello pour l’activation de KCD est relativement simple et ne nécessite généralement aucuns plus d’une compréhension générale de hello différents composants et flux d’authentification qui facilite l’authentification unique. Recherche de bonnes sources d’informations toohelp dépanner des scénarios où KCD SSO ne fonctionne pas comme prévu, peut être fragmenté.

Par conséquent, cet article tente tooprovide un seul point de référence qui peut aider à résoudre les problèmes et certains des problèmes les plus courants hello qu’il corrige automatiquement. À hello même offre des conseils supplémentaires de temps pour diagnostiquer hello plus complexe et gênés d’implémentation.

Notez que cet article rend hello suivant hypothèses :

-   Proxy d’Application Azure a été déployé en tant que par notre [documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable) et applications de KCD toonon accès général fonctionne comme prévu.

-   Hello application publiée cible est basée sur la mise en œuvre de IIS et de Microsoft du protocole kerberos.

-   hôtes de serveur et l’application Hello résident dans un seul domaine Active Directory. Vous trouverez des informations détaillées sur les scénarios inter-domaines et inter-forêts dans notre [livre blanc sur KCD](http://aka.ms/KCDPaper).

-   Hello objet application est publiée dans Azure locataire avec l’authentification préalable activée et les utilisateurs sont censés tooAzure tooauthenticate via des formulaires en fonction de l’authentification. Scénarios d’authentification client riche ne sont pas couverts par cet article, mais être ajoutés à un moment donné dans hello futures.

## <a name="prerequisites"></a>Composants requis

Proxy d’Application Azure peut être déployé dans presque n’importe quel type d’infrastructure ou architectures environnement et hello diffèrent sans aucun doute tooorganization d’organisation. Une des causes les plus courantes de KCD hello liées problèmes ne sont pas hello environnements eux-mêmes, mais plutôt simple en matière de configuration ou supervision générale.

Pour cette raison, notre Conseil est toujours toostart en vous assurant que vous avez rempli tous les logiciels prérequis hello disposés dans notre principal [KCD à l’aide de l’authentification unique avec l’article de Proxy d’Application hello](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) avant de démarrer résolution des problèmes.

En particulier les section de hello sur la configuration de KCD sur 2012 R2, car il utilise un tooconfiguring approche fondamentalement différente KCD sur les versions antérieures de Windows, mais également tout en étant penser plusieurs autres considérations :

-   Il n’est pas rare qu’un tooopen de serveur de membre de domaine une boîte de dialogue canal sécurisé avec un contrôleur de domaine spécifique. Puis déplacez tooanother la boîte de dialogue à un moment donné, les hôtes de connecteur doit donc généralement pas être toocommunicate en mesure de toobeing restreint avec les contrôleurs de domaine spécifiques uniquement de site local.

-   Toohello similaires au-dessus du point, les scénarios entre domaines reposent sur les références qui dirigent une tooDCs hôte connecteur situés en dehors du périmètre du réseau local hello. Dans ce scénario, il est tout aussi important toomake que vous sont également autorisant le trafic d’et les versions ultérieures tooDCs qui représentent des autres domaines respectifs, ou bien la délégation d’échouer.

-   Dans la mesure du possible, vous devez éviter de placer des appareils IPS/IDS actifs entre les hôtes de connecteur et les contrôleurs de domaine. En effet, ceux-ci sont parfois trop intrusifs et interfèrent avec le trafic RPC de base.

Que nous souhaitons tooresolve problèmes rapidement et efficacement, peut prendre du temps, par conséquent, lorsque cela est possible doit essayer de délégation de test dans les scénarios les plus simples de hello. Hello plus vous introduisez de variables, hello plus avoir toocontend avec. Par exemple, limiter votre test tooa seul connecteur permettre gagner un temps précieux et connecteurs supplémentaires peuvent être ajoutées une fois les problèmes de hello a été résolu.

Certains facteurs environnementaux peuvent également être contribue tooan problème, et si possible, essayez et réduire hello architecture tooa minimum pour test. Par exemple, le pare-feu interne mal configuré ACL ne sont pas rares, donc si possible avoir tout le trafic à partir d’un connecteur autorisé directement par le biais de contrôleurs de domaine toohello et de l’application principale. 

Hello absolu meilleures place tooposition les connecteurs est en fait des cibles tootheir aussi près que peut être. La mise en place d’un pare-feu en ligne lors des tests ne fait qu’ajouter une complexité inutile et peut prolonger vos recherches.

Alors quels aspects caractérisent effectivement un problème avec KCD ? Ainsi, il plusieurs indications classiques de SSO KCD défectueux et hello premiers signes d’un problème généralement manifestent hello navigateur.

   ![Erreur de configuration incorrecte de KCD](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic1.png)

   ![Autorisation a échoué en raison d’autorisations de toomissing](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic2.png)

tous les qui portent hello même symptôme de l’échec de tooperform SSO et, par conséquent, le refus hello application toohello de l’accès utilisateur.

## <a name="troubleshooting"></a>Résolution des problèmes

Comment vous puis résolvez le problème dépendent de problème de hello et symptômes observés. Avant d’aller plus nous suggère hello suivant liens, car ils contiennent des informations utiles que vous pas encore avoir rencontriez :

-   [Résoudre les problèmes de proxy d’application et les messages d’erreur](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot)

-   [Erreurs Kerberos](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot#kerberos-errors)

-   [Utilisation de l’authentification unique quand des identités locales et sur le cloud ne sont pas identiques](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd#working-with-sso-when-on-premises-and-cloud-identities-are-not-identical)

Si vous avez cette mesure, puis hello principal problème existe définitivement. Vous devez toodig plus profond, donc démarrer en séparant les flux de hello en trois étapes distinctes que vous pouvez résoudre les problèmes.

**Authentification préalable du client** -utilisateur externe de hello authentification tooAzure via un navigateur.

Qui est en mesure de toopre-authentifier tooAzure est impérative pour KCD SSO toofunction. Cette possibilité doit être testée et tout problème doit être résolu en premier lieu. Notez que l’étape de l’authentification préalable hello n’a aucune relation tooKCD ou le hello publié l’application. Il doit être assez simple toocorrect les éventuelles incohérences par les tests de vérification du compte de sujet hello existe dans Azure, et qu’il n’est pas désactivéent/bloqués. réponse d’erreur Hello dans le navigateur de hello s’agit généralement suffisamment descriptif toounderstand hello. Vous pouvez également vérifier nos autres tooverify de documents de dépannage si vous n’êtes pas sûr.

**Service de délégation** -hello connecteur Azure Proxy d’obtenir un kerberos ticket de service à partir d’un KDC (centre de Distribution Kerberos), pour le compte d’utilisateurs.

les communications externes de Hello entre le client de hello et de hello frontal Azure ne doit avoir aucune incidence sur KCD que ce soit, autre que vous être assuré qu’il fonctionne. Il s’agit donc hello service Proxy de Azure peut être fournie avec un ID d’utilisateur valide qui est utilisé tooobtain un ticket kerberos. Sans cela, la délégation KCD n’est pas possible et échouera.

Comme mentionné précédemment, messages d’erreur hello navigateur fournissent généralement des indices corrects sur la raison de l’échec choses. Assurez-vous que toonote hello ID d’activité et timestamp dans la réponse de hello car cela vous permettre des événements toocorrelate hello comportement tooactual dans le journal des événements Azure Proxy hello.

   ![Erreur de configuration incorrecte de KCD](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic3.png)

Et hello hello vu journal des événements peut être vu comme événements 13019 ou 12027 les entrées correspondantes. Vous pouvez trouver hello journaux des événements de connecteur dans **journaux des Applications et Services** &gt; **Microsoft** &gt; **AadApplicationProxy** &gt; **Connecteur**&gt;**Admin**.

   ![Événement 13019 du journal des événements du proxy d’application](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic4.png)

   ![Événement 12027 du journal des événements du proxy d’application](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic5.png)

-   Utiliser un enregistrement de votre serveur DNS interne pour l’adresse de l’application hello et pas un enregistrement CName

-   Reconfirmer hello droits toodelegate toohello désigné les SPN du compte cible et qui a été accordé à cet hôte de connecteur hello **utiliser tout protocole d’authentification** est sélectionnée. Cet aspect est abordé dans notre [article principal sur la configuration de l’authentification SSO](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd).

-   Vérifiez qu’il existe une seule instance de hello SPN existe dans Active Directory en émettant un **setspn - x** à partir d’une invite de commandes sur un hôte membre de domaine

-   Vérifiez si une stratégie de domaine est en cours de toosee appliquée toolimit hello [taille maximale de jetons kerberos émis](https://blogs.technet.microsoft.com/askds/2012/09/12/maxtokensize-and-windows-8-and-windows-server-2012/), comme ce connecteur de hello empêcher d’obtenir un jeton si trouvé toobe excessive

Une trace réseau capture échanges hello entre l’hôte du connecteur hello et un domaine KDC serait alors hello suivante meilleures étape permettant d’obtenir plus d’informations au niveau faible sur les problèmes de hello. Pour cela, reportez-vous au [document sur la résolution approfondie des problèmes](https://aka.ms/proxytshootpaper).

Si la création de tickets semble correcte, vous devez voir un événement dans les journaux hello indiquant que l’authentification a échoué en raison de l’application qui toohello renvoie une erreur 401. Cela indique généralement l’application cible hello rejet votre ticket, par conséquent, poursuivre hello suivant l’étape suivante.

**L’application cible** -consommateur hello du ticket kerberos de hello fourni par le connecteur de hello

À ce connecteur hello de phase est toohave attendu envoyé un backend toohello du ticket de service kerberos, comme un en-tête au sein de la première demande d’application hello.

-   URL interne définie dans le portail hello, à l’aide de l’application hello pour valider que l’application hello est accessible directement à partir de navigateur hello sur l’hôte du connecteur hello. Vous pouvez alors vous connecter. Vous trouverez des détails sur cette opération sur la page de résolution des problèmes du connecteur hello.

-   Toujours sur l’hôte du connecteur hello, vérifiez que l’authentification entre le navigateur de hello hello et application hello est à l’aide de kerberos, en effectuant l’une des manières suivantes les hello :

1.  Exécuter les outils de développement (**F12**) dans Internet Explorer, ou utilisez [Fiddler](https://blogs.msdn.microsoft.com/crminthefield/2012/10/10/using-fiddler-to-check-for-kerberos-auth/) à partir de l’hôte du connecteur hello. Accédez application toohello à l’aide d’une URL interne hello et inspecter hello proposé d’en-têtes d’autorisation WWW retournés en réponse hello à partir de l’application hello, tooensure soit negotiate ou kerberos est présent. Un objet blob suivantes kerberos retourné dans la réponse de hello de hello navigateur toohello application commencent généralement par **YÎ**, c’est une bonne indication de kerberos en cours de lecture. NTLM sur hello autre part commencent toujours par **TlRMTVNTUAAB**, qui lit NTLMSSP lorsque décodées à partir de Base64. Si vous voyez **TlRMTVNTUAAB** au début de hello d’objet blob de hello, cela signifie que Kerberos est **pas** disponibles. Dans le cas contraire, Kerberos est probablement disponible.

  * Notez que si vous utilisez Fiddler, cette méthode nécessiterait de désactiver temporairement la protection étendue sur la configuration de l’application hello dans IIS.

     ![Fenêtre de contrôle de réseau du navigateur](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic6.png)

    *Illustration :* dans cet exemple, comme le blob ne commence pas par TIRMTVNTUAAB, Kerberos est disponible. Cet exemple montre un blob Kerberos qui ne commence pas par YII.

2.  Supprimer temporairement NTLM à partir de la liste des fournisseurs hello sur site et accès application IIS directement à partir d’Internet Explorer sur l’ordinateur hôte du connecteur. Avec NTLM n’est plus dans la liste des fournisseurs hello, vous devez être en mesure de tooaccess application de hello uniquement à l’aide de Kerberos. En cas d’échec, qui suggère qu’il existe un problème avec la configuration de l’application hello et l’authentification Kerberos ne fonctionne pas.

Si Kerberos n’est pas disponible, l’authentification de l’application de vérification hello négocient des paramètres dans toomake IIS que figure au premier plan, avec NTLM situé sous celui-ci. (Vous ne devez pas voir Negotiate:kerberos ou Negotiate:PKU2U). Continuez uniquement si Kerberos est fonctionnel.

   ![Fournisseurs d’authentification Windows](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic7.png)
   
-   Avec Kerberos et NTLM en place, vous permet maintenant désactiver temporairement l’authentification préalable pour une application hello dans le portail de hello. Voir si vous pouvez y accéder à partir de hello internet à l’aide des URL externe de hello. Vous doit être invité à tooauthenticate et doit être en mesure de toodo donc avec hello même compte hello utilisé dans une étape précédente. Si ce n’est pas le cas, cela indique un problème avec l’application principale hello et KCD pas du tout.

-   Maintenant, réactivez l’authentification préalable dans le portail de hello et authentifier via Azure en tentant d’application de toohello tooconnect via son URL externe. Si l’authentification unique a échoué, vous devez voir un message d’erreur interdit dans le navigateur de hello, ainsi que des événements 13022 dans le journal de hello :

    *Microsoft AAD Application Proxy Connector ne peut pas authentifier l’utilisateur de hello, car le serveur principal de hello répond tooKerberos les tentatives d’authentification avec une erreur HTTP 401.*

    ![Message d’interdiction HTTP 401](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic8.png)

-   Vérifiez hello IIS application tooensure hello configuré pool d’applications est hello toouse configuré même compte que hello SPN a été configuré sur dans Active Directory, en naviguant dans IIS, comme illustré ci-dessous

    ![Fenêtre de configuration d’application IIS](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic9.png)

    Une fois que vous connaissez les identités hello, émettre suivant hello à partir d’un toomake invite cmd que ce compte est configuré sans aucun doute par hello nom principal de service en question. Par exemple, **setspn – q http/spn.wacketywack.com**

    ![Fenêtre de commandes SetSPN](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic10.png)

-   Vérifiez que hello SPN défini par rapport aux paramètres de l’application hello dans le portail de hello est hello même SPN qui est configuré sur hello cible AD compte utilisé par le pool d’applications de l’application hello

   ![Configuration du SPN dans le Portail Azure](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic11.png)
   
-   Accédez à IIS et sélectionnez hello **l’éditeur de Configuration** option pour une application hello et accédez trop**system.webServer/security/authentication/windowsAuthentication** toomake que ce **UseAppPoolCredentials** a la valeur tootrue

   ![Option de configuration IIS - informations d’identification des pools d’applications](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic12.png)

Tout en étant utiles pour améliorer les performances de hello des opérations Kerberos, en laissant en mode noyau provoque également ticket hello pour hello demandé toobe service déchiffrée à l’aide du compte d’ordinateur. Également appelé système Local hello, donc avoir ce saut de tootrue ensemble KCD lors de l’application hello est hébergée sur plusieurs serveurs dans une batterie de serveurs.

-   En tant qu’une vérification supplémentaire, vous pouvez également toodisable hello **étendue** protection trop. Ont été rencontrés scénarios où cela s’est avéré toobreak KCD quand activée dans des configurations très spécifiques, où une application est publiée en tant qu’un sous-dossier du site Web par défaut de hello. Cette lui-même est configuré pour l’authentification anonyme uniquement, en laissant les boîtes de dialogue ensemble hello grisées suggérer des objets enfants ne seraient pas hériter de tous les paramètres actives. Mais où possible, nous vous recommandons de serait toujours ayant cette option est activée, par conséquent, par tous les moyens de test, mais n’oubliez pas ce tooenabled toorestore.

Doivent avoir ces vérifications supplémentaires vous mettre dans toostart de suivi à l’aide de votre application publiée. Vous pouvez commencer et vitesse de rotation des connecteurs supplémentaires qui sont également configurés toodelegate, mais si aucune autres les choses sont puis nous suggère une lecture de notre procédure pas à pas techniques plus approfondies [guide complet de hello pour résoudre les problèmes de Azure AD Application Proxy](https://aka.ms/proxytshootpaper)

Si vous êtes toujours tooprogress ne peut pas votre problème, prise en charge est supérieure à tooassist heureux et continuer à partir d’ici. Créer un ticket de support directement dans le portail de hello et nos ingénieurs tooyou va joindre.

## <a name="other-scenarios"></a>Autres scénarios

-   Proxy d’Application Azure demande un ticket Kerberos avant d’envoyer son application tooan de demande. Certaines applications de tiers 3e comme serveur de Tableau ne convient pas cette méthode d’authentification et plutôt attend hello plus classique négociations tootake place,. Hello première demande est anonyme, ce qui permet de hello application toorespond avec les types d’authentification hello pris en charge via une erreur 401.

-   Authentification à deux tronçons : couramment utilisée dans les scénarios où une application est hiérarchisée, avec un serveur principal et un serveur frontal requérant tous deux une authentification comme les services SQL Reporting.

## <a name="next-steps"></a>Étapes suivantes
[Configurer la délégation Kerberos contrainte (KCD) sur un domaine géré](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-enable-kcd)
