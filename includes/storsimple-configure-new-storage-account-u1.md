<!--author=alkohli last changed: 9/17/15-->

#### <a name="tooadd-a-storage-account-in-storsimple-8000-series-update-10"></a>tooadd un compte de stockage StorSimple 8000 Series Update 1.0
1. Sur le service StorSimple Manager hello page d’accueil, sélectionnez votre service et double-cliquez dessus. Cette opération prendra toohello **Quick Start** page. Sélectionnez hello **configurer** page.
2. Cliquez sur **Ajouter/modifier un compte de stockage**.
3. Bonjour **Ajouter/modifier un compte de stockage** boîte de dialogue, cliquez sur **ajouter un nouveau**.
4. Bonjour **fournisseur** fournisseur de services de cloud approprié, sélectionnez hello. les fournisseurs de Hello pris en charge sont Azure, Amazon S3, S3 Amazon avec les enregistrements de ressources, HP et OpenStack. Spécifiez les informations d’identification hello et l’emplacement de hello associé au compte de stockage hello de vos fournisseurs de services cloud. champs Hello présentées pour les informations d’identification seront différentes selon de fournisseur de services de cloud hello que vous avez spécifié. 
   
   * Si vous avez sélectionné Azure en tant que votre fournisseur de services de cloud computing, fournissez hello **nom** et hello principal **clé d’accès** pour votre compte de stockage Microsoft Azure. Pour un compte Azure, emplacement de hello est rempli automatiquement.
     
        ![Ajout d’un compte Stockage Azure](./media/storsimple-configure-new-storage-account-u1/AddAzureStorageaccount-include.png)
   * Si vous avez sélectionné Amazon S3 ou Amazon S3 avec RRS, indiquez un **Nom de compte de stockage** convivial, une **Clé d’accès** et une **Clé secrète**. Amazon S3 et S3 Amazon avec les enregistrements de ressources, hello emplacements suivants est prises en charge :
     
     * Standard États-Unis
     * Ouest des États-Unis (Oregon)
     * Ouest des États-Unis (Californie du Nord)
     * UE (Irlande)
     * Asie-Pacifique (Singapour)
     * Asie-Pacifique (Sydney)
     * Asie-Pacifique (Tokyo)
     * Amérique du Sud (Sao Paulo)
       
       ![Ajout d’un compte de stockage Amazon](./media/storsimple-configure-new-storage-account-u1/AddAmazonStorageaccount-include.png)
   * Si vous avez sélectionné HP comme fournisseur de services cloud, indiquez un **Nom de compte de stockage** convivial, un **ID de locataire**, un **Nom d’utilisateur** et un **Mot de passe**. Pour HP, hello emplacements suivants est pris en charge :
     
     * Est des États-Unis
     * Ouest des États-Unis
       
       ![Ajout d’un compte de stockage HP](./media/storsimple-configure-new-storage-account-u1/AddHPStorageaccount-include.png)
   * Si vous avez sélectionné **Openstack** comme fournisseur de services cloud, indiquez un **Nom d’hôte**, une **Clé d’accès** et une **Clé secrète**.
     
     > [!NOTE]
     > Pour tous les fournisseurs de services de cloud hello, à l’exclusion de Azure, un nom convivial est autorisé. Vous pouvez utiliser des noms conviviaux différents et créer plusieurs comptes de stockage avec le même jeu d’informations d’identification de hello.
     > 
     > 
     
        ![Ajout du compte de stockage Openstack](./media/storsimple-configure-new-storage-account-u1/AddOpenstackStorageaccount-include.png)
5. Sélectionnez **activer le Mode SSL** toocreate un canal sécurisé pour la communication réseau entre votre cloud hello et des appareils. Désactivez hello **activer le Mode SSL** case à cocher uniquement si vous opérez dans un cloud privé.
   
   > [!NOTE]
   > Si vous utilisez HP comme fournisseur, SSL est toujours activé.
   > 
   > 
6. Cliquez sur une icône de coche hello ![icône en forme de coche](./media/storsimple-configure-new-storage-account/HCS_CheckIcon-include.png). Vous serez averti une fois le compte de stockage hello est créé avec succès.
7. Hello compte de stockage nouvellement créé s’affichera sur hello **configurer** page sous **comptes de stockage**. Cliquez sur **enregistrer** toosave hello nouveau compte de stockage. Cliquez sur **OK** lorsque vous êtes invité à confirmer l’opération.

