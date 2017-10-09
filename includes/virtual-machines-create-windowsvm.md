1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).

2. Désormais, dans le coin supérieur gauche de hello, cliquez sur **Nouveau > calcul > Windows Server 2016 Datacenter**.

    ![Accédez toohello des images de machine virtuelle Azure dans le portail de hello](./media/virtual-machines-common-portal-create-fqdn/marketplace-new.png)

3. Sur hello Datacenter de Windows Server 2016, sélectionnez le modèle de déploiement classique hello. Cliquez sur Créer.

    ![Capture d’écran qui affiche les images de machine virtuelle Azure hello disponibles dans le portail de hello](./media/virtual-machines-common-portal-create-fqdn/deployment-classic-model.png)

## <a name="1-basics-blade"></a>1. Panneau Informations de base

Panneau de principes de base Hello demande des informations d’administration pour l’ordinateur virtuel de hello.

1. Entrez un **nom** pour la machine virtuelle de hello. Dans l’exemple de hello, _HeroVM_ est le nom hello de machine virtuelle de hello. nom de Hello doit être de 1 à 15 caractères et il ne peut pas contenir les caractères spéciaux.

2. Entrez un **nom d’utilisateur** et un nom fort **mot de passe** qui sont toocreate utilisé un compte local sur hello machine virtuelle. Hello compte local est utilisé toosign dans tooand gérer hello machine virtuelle. Dans l’exemple de hello, _azureuser_ est le nom d’utilisateur hello.

 Hello doit comporter 8-123 caractères et répondre aux trois des exigences de complexité suivant quatre hello : une lettre minuscule, une lettre majuscule, un chiffre et un caractère spécial. En savoir plus sur les [conditions requises pour les noms d’utilisateur et les mots de passe](../articles/virtual-machines/windows/faq.md).

3. Hello **abonnement** est facultatif. Le paramètre le plus courant est « Paiement à l’utilisation ».

4. Sélectionnez un existant **groupe de ressources** ou nom du type hello pour un nouveau. Dans l’exemple de hello, _HeroVMRG_ est le nom hello hello du groupe de ressources.

5. Sélectionnez un centre de données Azure **emplacement** où vous souhaitez hello VM toorun. Dans l’exemple de hello, **États-Unis** est l’emplacement de hello.

6. Lorsque vous avez terminé, cliquez sur **suivant** Panneau de toocontinue toohello suivant.

    ![Capture d’écran qui affiche les paramètres de hello sur le panneau des principes de base hello pour la configuration d’une machine virtuelle Azure](./media/virtual-machines-common-portal-create-fqdn/basics-blade-classic.png)

## <a name="2-size-blade"></a>2. Panneau Taille

Panneau de taille Hello identifie les détails de la configuration de machine virtuelle de hello hello et répertorie les différentes options qui incluent le système d’exploitation, le nombre de processeurs, type de stockage de disque et des coûts d’utilisation mensuelle estimée.  

Choisissez une taille de machine virtuelle, puis cliquez sur **sélectionnez** toocontinue. Dans cet exemple, _DS1_\__V2 Standard_ est la taille de machine virtuelle hello.

  ![Capture d’écran du Panneau de taille hello qui montre les tailles de machine virtuelle Azure hello que vous pouvez sélectionner](./media/virtual-machines-common-portal-create-fqdn/vm-size-classic.png)


## <a name="3-settings-blade"></a>3. Panneau Paramètres

Panneau de paramètres Hello demande des options de stockage et réseau. Vous pouvez accepter les paramètres par défaut de hello. Azure crée les entrées appropriées si nécessaire.

Si vous avez sélectionné une taille de machine virtuelle qui le prend en charge, vous pouvez essayer le Stockage Premium Azure en sélectionnant Premium (SSD) sous Type de disque.

Une fois les modifications terminées, cliquez sur **OK**.

## <a name="4-summary-blade"></a>4. Panneau Résumé

Panneau de résumé Hello répertorie les paramètres de hello spécifiés dans les panneaux précédente hello. Cliquez sur **OK** lorsque vous êtes l’image de hello toomake prêt.

 ![Rapport de synthèse panneau donnant des paramètres spécifiés de la machine virtuelle de hello](./media/virtual-machines-common-portal-create-fqdn/summary-blade-classic.png)

Après la création de la machine virtuelle de hello, portail de hello répertorie hello machine virtuelle sous **toutes les ressources**et affiche une vignette de l’ordinateur virtuel de hello sur le tableau de bord hello. Hello correspondant cloud service compte de stockage et sont également créées et répertoriées. Machine virtuelle de hello et le service cloud sont démarrées automatiquement et leur état est répertorié en tant que **en cours d’exécution**.

 ![Configurer l’Agent de machine virtuelle et hello des points de terminaison de machine virtuelle de hello](./media/virtual-machines-common-portal-create-fqdn/portal-with-new-vm.png)
