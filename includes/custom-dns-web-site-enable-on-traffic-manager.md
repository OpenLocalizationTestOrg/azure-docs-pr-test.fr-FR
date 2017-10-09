Une fois la propagation des enregistrements hello pour votre nom de domaine, vous devez être en mesure de toouse tooverify votre navigateur que votre nom de domaine personnalisé peut être utilisé tooaccess votre application web dans Azure App Service.

> [!NOTE]
> Il peut prendre un certain temps pour votre toopropagate CNAME via hello système DNS. Vous pouvez utiliser un service, tel que <a href="http://www.digwebinterface.com/">http://www.digwebinterface.com/</a> tooverify qui hello CNAME est disponible.
> 
> 

Si vous n’avez pas encore ajouté de votre application web en tant qu’un point de terminaison Traffic Manager, vous devez le faire avant que la résolution de noms fonctionnent, en tant que tooTraffic d’itinéraires de nom de domaine personnalisé hello Manager. Traffic Manager achemine ensuite l’application web tooyour. Utilisez les informations de hello dans [ajouter ou supprimer les points de terminaison](../articles/traffic-manager/traffic-manager-endpoints.md) tooadd votre application web en tant qu’un point de terminaison dans votre profil Traffic Manager.

> [!NOTE]
> Si votre application web n’est pas répertoriée lors de l’ajout d’un point de terminaison, vérifiez qu’elle est configurée pour le mode de plan App Service **Standard** . Vous devez utiliser **Standard** mode pour votre application web dans l’ordre toowork avec Traffic Manager.
> 
> 

1. Dans votre navigateur, ouvrez hello [Azure Portal](https://portal.azure.com).
2. Bonjour **Web Apps** , cliquez sur le nom hello de votre application web, sélectionnez **paramètres**, puis sélectionnez **les domaines personnalisés**
   
    ![](./media/custom-dns-web-site/dncmntask-cname-6.png)
3. Bonjour **les domaines personnalisés** panneau, cliquez sur **ajouter le nom d’hôte**.
4. Hello d’utilisation **nom d’hôte** texte zones tooenter hello Traffic Manager domaine nom tooassociate avec cette application web.
   
    ![](./media/custom-dns-web-site/dncmntask-cname-8.png)
5. Cliquez sur **Validate** configuration de nom de domaine toosave hello.
6. Lorsque vous cliquez sur **Valider** , Azure lance le flux de travail de vérification du domaine. Cela vérifie pour la propriété de domaine ainsi que d’une réussite de disponibilité et de rapport du nom d’hôte ou d’erreur détaillée avec guidence normative sur la façon dont toofix hello erreur.    
7. Si la validation réussit **ajouter le nom d’hôte** bouton devient actif et vous serez en mesure de toohello affecter hostname. Maintenant accédez tooyour nom de domaine personnalisé dans un navigateur. Vous devriez voir votre application s’exécuter sous votre nom de domaine personnalisé. 
   
   Une fois la configuration terminée, nom de domaine personnalisé hello s’afficheront dans hello **les noms de domaine** section de votre application web.

À ce stade, vous devez être le nom du nom de domaine en mesure de tooenter hello Traffic Manager dans votre navigateur et consultez correctement nécessaire tooyour l’application web.

