
<br>

> [!NOTE]
> Si un administrateur vous a donné un nom d’utilisateur et un mot de passe, il est probable que vous disposiez déjà d’un ID professionnel ou scolaire (parfois appelé *ID d’organisation*). Dans ce cas, vous pouvez commencer immédiatement toouse votre tooaccess compte Azure des ressources Azure qui en ont besoin. Si vous trouvez que vous ne pouvez pas utiliser ces ressources, vous devrez peut-être tooreturn toothis article d’aide. Pour plus d’informations, consultez [les comptes que vous pouvez utiliser pour se connecter](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) et [abonnement de la manière dont un Azure est connexe tooAzure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).
> 
> 

étapes de Hello sont simples. Vous devez toolocate votre signé identité Bonjour portail Azure classic, découvrir votre domaine d’Azure Active Directory par défaut et ajouter un nouveau tooit d’utilisateur en tant qu’un coadministrateur Azure.

## <a name="locate-your-default-directory-in-hello-azure-classic-portal"></a>Recherchez le répertoire par défaut Bonjour portail Azure classic
Commencez par la journalisation dans toohello [portail Azure classic](https://manage.windowsazure.com) avec votre identité de compte Microsoft personnelle. Après vous être connecté, faites défiler panneau hello bleu sur hello côté gauche vers le bas et cliquez sur **ACTIVE DIRECTORY**.

![Azure Active Directory](./media/virtual-machines-common-create-aad-work-id/azureactivedirectorywidget.png)

Commençons par rechercher des informations sur votre identité dans Azure. Vous devez voir quelque chose comme hello suivant dans le volet principal de hello, indiquant que vous disposez d’un répertoire par défaut.

![](./media/virtual-machines-common-create-aad-work-id/defaultaadlisting.png)

Recherchons quelques informations supplémentaires. Cliquez sur ligne hello par défaut active, ce qui vous permet de propriétés du répertoire par défaut hello.  

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectorypage.png)

nom de domaine par défaut tooview hello, cliquez sur **domaines**.

![](./media/virtual-machines-common-create-aad-work-id/domainclicktoseeyourdefaultdomain.png)

Ici, vous devez être en mesure de toosee lors de la création de hello compte Azure, Azure Active Directory créé un domaine personnel par défaut qui est une valeur de hachage (un nombre généré à partir d’une chaîne de texte) de votre ID personnel utilisé comme un sous-domaine de onmicrosoft.com. Qui est toowhich de domaine hello vous allez maintenant ajouter un nouvel utilisateur.

## <a name="creating-a-new-user-in-hello-default-domain"></a>Création d’un utilisateur dans le domaine par défaut de hello
Cliquez sur **UTILISATEURS** et recherchez votre compte personnel unique. Vous devez voir Bonjour **provenance** colonne qu’il est un **compte Microsoft**. Nous souhaitons toocreate un utilisateur dans la valeur par défaut. domaine Azure Active Directory de onmicrosoft.com.

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryuserslisting.png)

Nous allons toofollow [ces instructions](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) dans hello lors des étapes suivantes, mais utiliser un exemple spécifique.

Au bas de hello de page de hello, cliquez sur **+ ajouter un utilisateur**. Dans la page hello qui s’affiche, tapez le nouveau nom d’utilisateur hello et rendre hello **Type d’utilisateur** un **nouvel utilisateur dans votre organisation**. Dans cet exemple, le nouveau nom d’utilisateur hello est `ahmet`. Sélectionnez le domaine par défaut hello que vous avez découvert précédemment en tant que domaine hello pour l’adresse de messagerie du ahmet. Cliquez sur hello la flèche suivante une fois.

![](./media/virtual-machines-common-create-aad-work-id/addingauserwithdirectorydropdown.png)

Ajoutez plus de détails pour Ahmet, mais assurez-vous que tooselect hello approprié **rôle** valeur. Il est facile toouse **administrateur Global** toomake que cela fonctionne, mais si vous pouvez utiliser un rôle plus petit, qui est une bonne idée. Cet exemple utilise hello **utilisateur** rôle. (Pour plus d’informations, consultez la section relative aux [autorisations des administrateurs par rôle](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) N’activez pas l’authentification multifacteur, sauf si vous souhaitez que l’authentification multifacteur toouse pour chaque journal dans l’opération. Lorsque vous avez terminé, cliquez sur flèche suivant de hello.

![](./media/virtual-machines-common-create-aad-work-id/userprofileuseradmin.png)

Cliquez sur hello **créer** bouton toogenerate et afficher un mot de passe temporaire pour Ahmet.

![](./media/virtual-machines-common-create-aad-work-id/gettemporarypasswordforuser.png)

Copier l’adresse de messagerie hello user name, ou utiliser **envoyer un message électronique de mot de passe**. Vous devez hello informations toolog sur peu de temps.

![](./media/virtual-machines-common-create-aad-work-id/receivedtemporarypassworddialog.png)

Maintenant vous devriez voir hello nouvel utilisateur **Ahmet hello développeur**, Corée d’Azure Active Directory. Vous avez créé le nouveau travail de hello ou l’identité de l’établissement scolaire avec Azure Active Directory. Toutefois, cette identité n’a pas encore autorisations toouse Azure ressources.

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryusersaftercreate.png)

Si vous utilisez **envoyer un message électronique de mot de passe**, hello suivant le type de courrier électronique est envoyé.

![](./media/virtual-machines-common-create-aad-work-id/emailreceivedfromnewusercreation.png)

## <a name="adding-azure-co-administrator-rights-for-subscriptions"></a>Ajout de droits de co-administrateur Azure pour les abonnements
Vous devez maintenant utilisateur tooadd hello en tant que coadministrateur de votre abonnement pour la connexion utilisateur hello dans toohello portail de gestion. toodo, dans le panneau inférieur gauche de hello cliquez sur **paramètres**.

![](./media/virtual-machines-common-create-aad-work-id/thesettingswidget.png)

Dans la zone de paramètres principaux hello, cliquez sur **administrateurs** à hello haut et que vous devez voir seulement votre identité du compte Microsoft personnelle. Au bas de hello de page de hello, cliquez sur **+ ajouter** toospecify un coadministrateur. Saisir une adresse de messagerie hello du hello nouvel utilisateur que vous avez créé, y compris votre domaine par défaut. Comme indiqué dans la capture d’écran suivante de hello, une coche verte apparaît utilisateur toohello suivant hello répertoire par défaut. N’oubliez pas de tooselect tous les abonnements hello que vous souhaitez que cette tooadminister en mesure de toobe utilisateur.

![](./media/virtual-machines-common-create-aad-work-id/addingnewuserascoadmin.png)

Lorsque vous avez terminé, vous devriez voir deux utilisateurs, y compris la nouvelle identité de votre co-administrateur. Déconnectez-vous de portail de hello.

![](./media/virtual-machines-common-create-aad-work-id/newuseraddedascoadministrator.png)

## <a name="logging-in-and-changing-hello-new-users-password"></a>Connexion et la modification de mot de passe hello du nouvel utilisateur
Ouvrez une session en tant qu’utilisateur de nouvelle hello que vous avez créé.

![](./media/virtual-machines-common-create-aad-work-id/signinginwithnewuser.png)

Vous verrez alors immédiatement toocreate invité à un nouveau mot de passe.

![](./media/virtual-machines-common-create-aad-work-id/mustupdateyourpassword.png)

Vous devez être récompensé avec succès qui ressemble à hello suivant.

![](./media/virtual-machines-common-create-aad-work-id/successtourdialog.png)

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez maintenant utiliser votre nouveau toouse d’identité Azure Active Directory [modèles de groupe de ressources Azure](../articles/xplat-cli-azure-resource-manager.md).

    azure login
    info:    Executing command login
    warn:    Please note that currently you can login only via Microsoft organizational account or service principal. For instructions on how tooset them up, please read http://aka.ms/Dhf67j.
    Username: ahmet@aztrainpassxxxxxoutlook.onmicrosoft.com
    Password: *********
    /info:    Added subscription Azure Pass
    info:    Setting subscription Azure Pass as default
    +
    info:    login command OK
    ralph@local:~$ azure config mode arm
    info:    New mode is arm
    ralph@local:~$ azure group list
    info:    Executing command group list
    + Listing resource groups
    info:    No matched resource groups were found
    info:    group list command OK
    ralph@local:~$ azure group create newgroup westus
    info:    Executing command group create
    + Getting resource group newgroup
    + Creating resource group newgroup
    info:    Created resource group newgroup
    data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/newgroup
    data:    Name:                newgroup
    data:    Location:            westus
    data:    Provisioning State:  Succeeded
    data:    Tags:
    data:
    info:    group create command OK
