Une fois la propagation des enregistrements hello pour votre nom de domaine, vous devez les associer avec votre application Web. Utilisez hello suivant des noms de domaine hello tooenable étapes à l’aide de votre navigateur web.

> [!NOTE]
> Il peut prendre un certain temps pour les enregistrements TXT créé dans hello précédentes étapes toopropagate via hello système DNS. Impossible d’ajouter le nom de domaine hello de l’application web tooyour jusqu'à ce que l’enregistrement TXT de hello a propagé. Si vous utilisez un enregistrement A, vous ne pouvez pas ajouter hello une application web de domaine enregistrement nom tooyour jusqu'à ce que l’enregistrement TXT de hello créé à l’étape précédente de hello a propagé.
> 
> Vous pouvez utiliser un service, tel que <a href="http://www.digwebinterface.com/">http://www.digwebinterface.com/</a> tooverify qui hello enregistrement TXT est disponible.
> 
> 

1. Dans votre navigateur, ouvrez hello [Azure Portal](https://portal.azure.com).
2. Bonjour **Web Apps** onglet, cliquez sur nom hello de votre application web, puis sélectionnez **les domaines personnalisés**
   
    ![](./media/custom-dns-web-site/dncmntask-cname-6.png)
3. Bonjour **les domaines personnalisés** panneau, cliquez sur **ajouter le nom d’hôte**.
4. Hello d’utilisation **nom d’hôte** texte zones tooenter hello domaine noms tooassociate avec cette application web.
   
    ![](./media/custom-dns-web-site/add-custom-domain.png)
5. Cliquez sur **Valider**.
6. Lorsque vous cliquez sur **Valider** , Azure lance le flux de travail de vérification du domaine. Cela vérifie pour la propriété de domaine ainsi que d’une réussite de disponibilité et de rapport du nom d’hôte ou d’erreur détaillée avec guidence normative sur la façon dont toofix hello erreur.    

À ce stade, vous devez être un nom de domaine personnalisé en mesure de tooenter hello dans votre navigateur et consultez correctement nécessaire tooyour l’application web.

