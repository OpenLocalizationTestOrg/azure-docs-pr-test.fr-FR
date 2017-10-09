---
title: aaaCreate Azure BizTalk Services Bonjour portail Azure | Documents Microsoft
description: "Découvrez comment tooprovision ou créer des Services BizTalk Azure Bonjour portail Azure ; MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 3ad18876-a649-40d6-9aa0-1509c1d62c43
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 6781cadada8ac9c84e1fe045d2b0f995811f75b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-biztalk-services-using-hello-azure-portal"></a>Créer des Services BizTalk à l’aide de hello portail Azure

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]


> [!TIP]
> toosign dans toohello portail Azure, vous devez un compte Azure et un abonnement Azure. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Consultez [Version d'évaluation gratuite d'Azure](http://go.microsoft.com/fwlink/p/?LinkID=239738).


## <a name="CreateService"></a>Créer un service BizTalk
Selon l’édition que vous choisissez de hello, pas tous les paramètres de BizTalk Service peuvent être disponibles.

1. Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Dans le volet de navigation inférieur hello, sélectionnez **nouveau**:  
   ![Sélectionnez le bouton de nouveau hello][NEWButton]
3. Sélectionnez **APP SERVICES** > **SERVICE BIZTALK** > **CRÉATION PERSONNALISÉE** :  
   ![Sélectionner BizTalk Services, puis Custom Create][NewBizTalkService]
4. Entrez les paramètres de Service BizTalk hello :
   
    <table border="1">
    <tr>
    <td><strong>Nom du service BizTalk</strong></td>
    <td>Vous pouvez entrer n'importe quel nom, mais soyez spécifique. Voici quelques exemples :<br/><br/>
    <em>masociété</em>.biztalk.windows.net<br/>
    <em>masociétémonapplication</em>.biztalk.windows.net<br/>
    <em>monapplication</em>.biztalk.windows.net<br/><br/>«. biztalk.windows.net » est automatiquement ajouté toohello nom que vous entrez. Cette opération crée une URL qui est utilisé tooaccess votre BizTalk Service, tel que <strong>https://<em>myapplication</em>. biztalk.windows.net</strong>.
    </td>
    </tr>
    <tr>
    <td><strong>Édition</strong></td>
    <td>Si vous êtes dans la phase de test/développement hello, choisissez <strong>développeur</strong>. Si vous êtes dans la phase de production hello, utilisez hello <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">Services BizTalk : tableau comparatif des éditions</a> toodetermine si <strong>Premium</strong>, <strong>Standard</strong>, ou <strong>Basic</strong>est hello bon choix pour votre scénario d’entreprise.
    </td>
    </tr>
    <tr>
    <td><strong>Région</strong></td>
    <td>Sélectionnez hello région géographique toohost votre BizTalk Service.</td>
    </tr>
    <tr>
    <td><strong>URL du domaine</strong></td>
    <td><strong>Facultatif</strong>. Par défaut, les URL de domaine hello est <em>Nom_de_votre_service_biztalk</em>. biztalk.windows.net. Un domaine personnalisé peut également être entré. Par exemple, si votre domaine est <em>contoso</em>, vous pouvez entrer : <br/><br/>
    <em>MaSociété</em>.contoso.com<br/>
    <em>MaSociétéMonApplication</em>.contoso.com<br/>
    <em>MonApplication</em>.contoso.com<br/>
    <em>NomServiceBizTalk</em>.contoso.com<br/>
    </td>
    </tr>
    </table>
Sélectionnez la flèche suivant de hello.
5. Entrez hello stockage et les paramètres de la base de données :  <table border="1">
    <tr>
    <td><strong>Compte de stockage de surveillance/archivage</strong></td>
    <td>Sélectionnez un compte de stockage existant ou créez un nouveau compte de stockage. <br/><br/>Si vous créez un compte de stockage, entrez hello <strong>nom de compte de stockage</strong>.</td>
    </tr>
    <tr>
    <td><strong>Base de données de suivi</strong></td>
    <td>Si vous utilisez une base de données SQL Azure existante, celle-ci ne peut pas être utilisée par un autre service BizTalk. Vous devez le nom de connexion hello et le mot de passe entré lors de la création de ce serveur de base de données SQL Azure.<br/><br/><strong>Conseil</strong> base de données de suivi créer hello et compte de stockage surveillance/archivage hello même région que hello BizTalk Service.</td>
    </tr>
    </table>
Sélectionnez la flèche suivant de hello.
6. Entrez les paramètres de base de données hello :  <table border="1">
    <tr>
    <td><strong>Name</strong></td>
    <td>Disponible lorsque <strong>créer une nouvelle instance de la base de données SQL</strong> est sélectionné dans l’écran précédent hello.
    <br/><br/>
Entrez un toobe de nom de base de données SQL utilisée par votre BizTalk Service.</td>
    </tr>
    <tr>
    <td><strong>Serveur</strong></td>
    <td>Disponible lorsque <strong>créer une nouvelle instance de la base de données SQL</strong> est sélectionné dans l’écran précédent hello.
    <br/><br/>
Sélectionnez un serveur SQL Database existant ou créez-en un.</td>
    </tr>
    <tr>
    <td><strong>Nom de connexion du serveur</strong></td>
    <td>Entrez le nom d’utilisateur hello.</td>
    </tr>
    <tr>
    <td><strong>Mot de passe de connexion du serveur</strong></td>
    <td>Entrez le mot de passe de connexion hello.</td>
    </tr>
    <tr>
    <td><strong>Région</strong></td>
    <td>Disponible lorsque l’option <strong>Créer une instance de base de données SQL</strong> est sélectionnée. Sélectionnez hello région géographique toohost votre base de données SQL.</td>
    </tr>
    </table>

Sélectionnez hello coche toocomplete hello Assistant. icône de progression Hello s’affiche :  
![Icône d'avancement affichée à la fin de l'opération][ProgressComplete]

Lorsque vous avez terminé, hello Azure BizTalk Service est créé et prêt pour vos applications. paramètres par défaut de Hello sont suffisants. Si vous souhaitez que les paramètres par défaut de hello toochange, sélectionnez **BIZTALK SERVICES** dans hello du volet de navigation gauche, puis sélectionnez votre BizTalk Service. Paramètres supplémentaires sont affichés dans hello [onglets tableau de bord, analyse et mise à l’échelle](biztalk-dashboard-monitor-scale-tabs.md) haut hello.

En fonction de l’état de hello Hello BizTalk Service, il existe certaines opérations qui ne peut pas être terminées. Pour obtenir la liste de ces opérations, consultez trop[BizTalk Services état graphique](biztalk-service-state-chart.md).

## <a name="post-provisioning-steps"></a>Étapes postérieures à l’approvisionnement
* [Installer le certificat de hello sur un ordinateur local](#InstallCert)
* [Ajouter un certificat prêt pour la production](#AddCert)
* [Obtenir l’espace de noms de contrôle d’accès hello](#ACS)

#### <a name="InstallCert"></a>Installer le certificat de hello sur un ordinateur local
Dans le cadre de l'approvisionnement du service BizTalk, un certificat auto-signé est créé et associé à votre abonnement au service BizTalk. Vous devez télécharger ce certificat et l’installer sur des ordinateurs de l’emplacement où vous déployez des applications de BizTalk Service ou envoyez des messages tooa point de terminaison de BizTalk Service.

1. Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Sélectionnez **BIZTALK SERVICES** dans hello du volet de navigation gauche, puis sélectionnez votre abonnement au Service de BizTalk.
3. Sélectionnez hello **tableau de bord** onglet.
4. Sélectionnez **Télécharger le certificat SSL** :  
   ![Modifier le certificat SSL][QuickGlance]
5. Double-cliquez sur le certificat de hello et exécuter via un certificat de hello Assistant tooinstall hello. Assurez-vous que vous installez le certificat hello sous hello **autorités de certification racine de confiance** stocker.

#### <a name="AddCert"></a>Ajouter un certificat prêt pour la production
Hello un certificat auto-signé créé automatiquement lors de la création de Services de BizTalk est prévu pour une utilisation dans les environnements de développement uniquement. Dans les scénarios de production, remplacez-le par un certificat prêt pour la production.

1. Sur hello **tableau de bord** onglet, sélectionnez **certificat SSL de mise à jour**.
2. Parcourir les certificats SSL privé tooyour (*CertificateName*.pfx) qui inclut le nom de votre BizTalk Service, hello mot de passe, puis cliquez sur la case à cocher hello.

#### <a name="ACS"></a>Obtenir l’espace de noms de contrôle d’accès hello
1. Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Sélectionnez **BIZTALK SERVICES** dans hello du volet de navigation gauche, puis sélectionnez votre BizTalk Service.
3. Dans la barre des tâches hello, sélectionnez **les informations de connexion**:  
   ![Sélectionner les informations de connexion][ACSConnectInfo]
4. Copiez les valeurs de contrôle d’accès hello.

Lorsque vous déployez un projet BizTalk Services à partir de Visual Studio, vous entrez cet espace de noms de contrôle d'accès. espace de noms de contrôle d’accès Hello est automatiquement créé pour votre BizTalk Service.

valeurs de contrôle d’accès de Hello peuvent être utilisées avec n’importe quelle application. En cas d’Azure BizTalk Services est créé, cet espace de noms de contrôle d’accès contrôle authentification hello avec votre déploiement de BizTalk Service. Si vous souhaitez toochange hello abonnement ou gérez l’espace de noms hello, sélectionnez **ACTIVE DIRECTORY** dans hello du volet de navigation gauche et sélectionnez votre espace de noms. barre des tâches Hello répertorie les options disponibles.

En cliquant sur **gérer** ouvre hello portail de gestion Access Control. Dans le portail de gestion Access Control de hello, hello BizTalk Service utilise **identités de Service**:  
![Identités de Service ACS Bonjour portail de gestion Access Control][ACSServiceIdentities]

Hello identité de service de contrôle d’accès est un ensemble d’informations d’identification qui permettent aux applications ou tooauthenticate clients directement avec le contrôle d’accès et de recevoir un jeton.

> [!IMPORTANT]
> Hello BizTalk Service utilise **propriétaire** pour l’identité de service par défaut hello et hello **mot de passe** valeur. Si vous utilisez la valeur de clé symétrique hello au lieu de la valeur de mot de passe de hello, hello erreur suivante peut se produire.<br/><br/>*Pas pu se connecter compte de Service de gestion Access Control toohello hello spécifié avec les informations d’identification*
> 
> 

[Gestion de votre espace de noms ACS](https://msdn.microsoft.com/library/azure/hh674478.aspx) répertorie quelques instructions et recommandations.

## <a name="requirements-explained"></a>Explication des exigences
Ces exigences ne s’appliquent pas toohello édition gratuite.

<table border="1">
<tr bgcolor="FAF9F9">
        <td><strong>Ce dont vous avez besoin</strong></td>
        <td><strong>Raison</strong></td>
</tr>
<tr>
<td>Abonnement Azure</td>
<td>abonnement de Hello détermine qui peut se connecter toohello portail Azure. détenteur du compte de Hello crée l’abonnement hello sur <a HREF="https://account.windowsazure.com/Subscriptions"> abonnements Azure</a>.
<br/><br/>
Bonjour compte Azure peut avoir plusieurs abonnements et peut être géré par toute personne qui est autorisée. Par exemple, le détenteur du compte Azure crée un abonnement nommé <em>BizTalkServiceSubscription</em> et donne hello administrateurs BizTalk au sein de votre société (par exemple, ContosoBTSAdmins@live.com) à toothis abonnement. Dans ce scénario, les administrateurs de BizTalk hello connectez-vous toohello portail Azure et ont des services de hello hébergé tooall de droits administrateur complets dans l’abonnement hello, y compris les Services BizTalk Azure. les administrateurs de BizTalk Hello ne sont pas des détenteurs de compte Azure hello et par conséquent, n’avez pas accès aux informations de facturation tooany.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577">Gérer les abonnements et les comptes de stockage Bonjour Azure portal</a> fournit plus d’informations.
</td>
</tr>
<tr>
<td>Base de données SQL Azure</td>
<td>Stocke les tables de hello, vues et procédures stockées utilisées par hello BizTalk Service, y compris les données de suivi hello.
<br/><br/>
Lorsque vous créez un service BizTalk, vous pouvez utiliser un serveur SQL Azure existant, une base de données SQL Azure existante ou créer automatiquement un serveur ou une base de données.
<br/><br/>
Hello montée en puissance de la base de données SQL est configuré automatiquement. En règle générale, la mise à l’échelle par défaut de hello est suffisant pour un BizTalk Service. Modifier l’échelle de hello a un impact sur la tarification. Voir <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930">Comptes et facturation dans la base de données SQL Azure</a>
<br/><br/>
<strong>Remarques</strong>
<br/>
<ul>
<li> Lorsque vous créez un serveur et une base de données SQL Azure, les services Azure sont automatiquement activés. Hello BizTalk Service nécessite des Services Azure est activée.</li>
<li>Si vous créez une nouvelle base de données SQL Azure sur un serveur SQL Azure, hello des règles de pare-feu de hello serveur ne sont pas modifiés. Par conséquent, il est possible d’autres Services Azure ne sont pas autorisés de bases de données du serveur d’accès toohello.</li>
</ul>
</td>
</tr>
<tr>
<td>Espace de noms de contrôle d'accès Azure</td>
<td>Permet de s'authentifier auprès d'Azure BizTalk Services. Lorsque vous déployez un projet BizTalk Services à partir de Visual Studio, vous entrez cet espace de noms de contrôle d'accès. Lorsque vous créez un BizTalk Service, espace de noms de contrôle d’accès hello est automatiquement créé.</td>
</tr>

<tr>
<td>Compte de Stockage Azure</td>
<td>Offrent un accès tootables, objets BLOB et files d’attente utilisées par votre suivant de hello toosave BizTalk Service :

<ul>
<li>Les fichiers journaux qui hello moniteur BizTalk Service. Hello analyse la sortie s’affiche également dans hello **analyse** onglet Bonjour portail Azure.</li>
<li>Lorsque vous créez un X12 ou accord AS2 entre partenaires, vous pouvez activer les propriétés de message hello d’archivage fonctionnalité toostore. Ces données sont enregistrées dans le compte de stockage de hello.</li>
</ul>
<br/>
Lorsque vous créez un service BizTalk, vous pouvez utiliser un compte de stockage existant ou en créer un automatiquement.
<br/><br/>
paramètres de stockage Hello par défaut sont suffisantes pour un BizTalk Service.
<br/><br/>
Lorsque vous créez un compte de stockage, une clé primaire et une clé secondaire sont automatiquement créées. Ces clés contrôlent l’accès tooyour compte de stockage. Hello BizTalk Service utilise automatiquement hello clé primaire.
<br/><br/>
Pour plus d’informations, consultez <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671">Stockage</a>.
</td>
</tr>

<tr>
<td>Certificat privé SSL</td>
<td>
Quand un service Azure BizTalk est créé, une URL HTTPS qui inclut le nom de votre service BizTalk est également créée. Cette URL est automatiquement configuré toouse un certificat auto-signé de développement uniquement. Pour la production, vous avez besoin d'un certificat SSL privé.
<br/><br/>
<strong>Informations importantes sur le certificat SSL</strong>

<ul>
<li>date d’expiration de certificat Hello doit être inférieure à 5 ans.</li>
<li>Tous les certificats privés exigent un mot de passe. Retenez ce mot de passe. Il est également recommandé de communiquer ce mot de passe à vos administrateurs.</li>
<li>Les certificats auto-signés sont utilisés dans des environnements de test/développement. Lors de l’utilisation des certificats auto-signés, importez le magasin de certificats personnel hello certificat tooyour et hello du magasin de certificats Autorités de Certification racines de confiance.</li>
</ul>
<br/>Lors de l’envoi d’autorité de certification du certificat demande tooyour hello production, donnez à hello certificat propriétés suivantes :
<br/>

<ul>
<li><strong>Utilisation avancée de la clé</strong> : au minimum, Azure BizTalk Services exige l’authentification du serveur.</li>
<li><strong>Nom commun</strong>: entrez le nom de domaine complet (FQDN) hello de votre URL de Service Azure BizTalk. Voir <a HREF="#CreateService">Création d’un service BizTalk</a> dans cet article.</li>
</ul>
<br/>
Un certificat nouveau ou différent peut être ajouté après que hello BizTalk Service est créé.
</td>
</tr>
</table>
<!---Loc Comment: Please, check link [Create a BizTalk Service] since it is not redirecting tooany location.--->



## <a name="hybrid-connections"></a>les connexions hybrides
Lorsque vous créez un BizTalk Service de Azure, hello **connexions hybrides** onglet est disponible :

![Onglet Connexions hybrides][HybridConnectionTab]

Connexions hybrides sont utilisé tooconnect Azure site Web ou service mobile Azure tooany localement les ressources qui utilise un port TCP statique, telles que SQL Server, MySQL, HTTP Web API, les Services mobiles et la plupart des Services Web personnalisés.  Connexions hybrides et hello Service d’adaptateur BizTalk sont différents. Hello Service d’adaptateur BizTalk est le système métier (LOB) local utilisé tooconnect Azure BizTalk Services tooan.

 Consultez [connexions hybrides](integration-hybrid-connection-overview.md) toolearn plus, notamment la création et la gestion des connexions hybrides.

## <a name="next-steps"></a>Étapes suivantes
Maintenant que la création d’un BizTalk Service, familiarisez-vous avec hello différents [BizTalk Services : onglets tableau de bord, analyse et mise à l’échelle](biztalk-dashboard-monitor-scale-tabs.md). Votre service BizTalk est prêt pour vos applications. toostart création d’applications, accédez trop[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).

## <a name="see-also"></a>Voir aussi
* [Tableau comparatif des éditions de BizTalk Services](biztalk-editions-feature-chart.md)<br/>
* [Tableau comparatif des états du service BizTalk](biztalk-service-state-chart.md)<br/>
* [Sauvegarde et restauration de BizTalk Services](biztalk-backup-restore.md)<br/>
* [Limitation dans BizTalk Services](biztalk-throttling-thresholds.md)<br/>
* [Nom et clé de l'émetteur dans BizTalk Services](biztalk-issuer-name-issuer-key.md)<br/>
* [Comment puis-je démarrer à l’aide de hello SDK des Services BizTalk Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [Connexions hybrides](integration-hybrid-connection-overview.md)

[NewBizTalkService]: ./media/biztalk-provision-services/WABS_NewBizTalkService.png
[NEWButton]: ./media/biztalk-provision-services/WABS_New.png
[ProgressComplete]: ./media/biztalk-provision-services/WABS_ProgressComplete.png
[ACSConnectInfo]: ./media/biztalk-provision-services/WABS_ACSConnectInformation.png
[QuickGlance]: ./media/biztalk-provision-services/WABS_QuickGlance.png
[ACSServiceIdentities]: ./media/biztalk-provision-services/WABS_ACSServiceIdentities.png
[HybridConnectionTab]: ./media/biztalk-provision-services/WABS_HybridConnectionTab.png
