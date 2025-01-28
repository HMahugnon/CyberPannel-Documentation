# Documentation d'installation et de personnalisation de CyberPanel

Bienvenue dans la documentation officielle de **CyberPanel**. Ce guide vous accompagne dans l’installation de CyberPanel, son intégration avec WHMCS, la configuration des services, et la personnalisation de la page CyberPanel pour vos clients.

## Table des matières

1. [Installation de CyberPanel](#installation-de-cyberpanel)
2. [Intégration de CyberPanel avec WHMCS](#integration-de-cyberpanel-avec-whmcs)
3. [Configuration des services dans CyberPanel](#configuration-des-services-dans-cyberpanel)
4. [Personnalisation de la page CyberPanel pour les clients](#personnalisation-de-la-page-cyberpanel-pour-les-clients)
5. [Configuration des services de messagerie (MX, TXT, DKIM, MSPMX)](#configuration-des-services-de-messagerie-mx-txt-dkim-mspmx)

---

## Installation de CyberPanel

### Prérequis

Avant de commencer l'installation, assurez-vous de disposer de ce qui suit :

- Un serveur dédié ou VPS avec l’un des systèmes d’exploitation suivants :
  - CentOS 7.x/8.x
  - Ubuntu 20.04/22.04
- Accès root ou un utilisateur avec privilèges sudo.

### Étapes d'installation

1. **Téléchargez et exécutez le script d'installation :**
   ```bash
   wget -O installer.sh https://cyberpanel.net/install.sh
   chmod +x installer.sh
   sudo ./installer.sh
   ```

2. **Suivez les instructions d'installation :**
   - Vous serez invité à choisir les composants à installer (par exemple, OpenLiteSpeed ou LiteSpeed Enterprise).
   - Saisissez un mot de passe pour l’administrateur de CyberPanel.

3. **Accédez à l'interface Web de CyberPanel :**
   Une fois l'installation terminée, vous pouvez vous connecter à CyberPanel via votre navigateur en accédant à :
   ```
   http://<IP_DU_SERVEUR>:8090
   ```
   Utilisez le nom d'utilisateur et le mot de passe que vous avez définis pendant l'installation pour vous connecter.

---

## Intégration de CyberPanel avec WHMCS

### Prérequis

- Une instance de WHMCS fonctionnelle.
- Le module CyberPanel pour WHMCS que vous pouvez télécharger depuis [le site officiel de CyberPanel](https://cyberpanel.net/).

### Étapes d'intégration

1. **Installation du module CyberPanel dans WHMCS :**
   - Téléchargez le module CyberPanel pour WHMCS.
   - Décompressez le fichier et placez le dossier du module dans le répertoire suivant de WHMCS :
     ```
     /path/to/whmcs/modules/servers/
     ```

2. **Configurer WHMCS pour utiliser le module CyberPanel :**
   - Connectez-vous à votre tableau de bord WHMCS.
   - Allez dans **Setup > Products/Services > Servers** et cliquez sur **Add New Server**.
   - Remplissez les informations suivantes :
     - **Nom du serveur** : CyberPanel
     - **Type de serveur** : CyberPanel
     - **URL du serveur** : URL de votre serveur CyberPanel.
     - **Nom d'utilisateur** : Le nom d'utilisateur administrateur de CyberPanel.
     - **Mot de passe** : Le mot de passe administrateur de CyberPanel.
   - Cliquez sur **Save Changes** pour enregistrer.

3. **Créer un groupe de serveurs dans WHMCS :**
   - Allez dans **Setup > Products/Services > Server Groups**.
   - Cliquez sur **Create a New Server Group** et associez le serveur CyberPanel au groupe.

---

## Configuration des services dans CyberPanel

### Étapes de configuration

1. **Ajouter un produit WHMCS :**
   - Dans WHMCS, allez dans **Setup > Products/Services > Products/Services**.
   - Cliquez sur **Create a New Product** et configurez les options suivantes :
     - **Type de produit** : Shared Hosting.
     - **Groupe de produits** : Choisissez un groupe comme "CyberPanel Plans".
     - **Nom et description** du produit, ainsi que le prix.

2. **Associer le module CyberPanel au produit :**
   - Allez dans l'onglet **Module Settings** de votre produit dans WHMCS.
   - Sélectionnez **CyberPanel** comme module.
   - Configurez les options spécifiques du produit comme le plan d'hébergement, les limites de ressources, et d'autres paramètres.
   - Cliquez sur **Save Changes** pour enregistrer le produit.

3. **Tester la configuration :**
   - Créez un compte d'essai pour vérifier que le service est correctement provisionné sur CyberPanel.

---

## Personnalisation de la page CyberPanel pour les clients

CyberPanel permet de personnaliser l'interface pour mieux s'adapter à votre marque et améliorer l'expérience de vos clients.

### Étapes de personnalisation

1. **Accédez à l'outil de personnalisation de CyberPanel :**
   - Connectez-vous à l’interface d'administration de CyberPanel.
   - Allez dans **Customization > Branding**.

2. **Changer le logo et les couleurs :**
   - Téléversez un logo personnalisé pour l’interface de CyberPanel.
   - Modifiez les couleurs principales de l’interface (par exemple, la couleur de fond et des boutons) pour correspondre à votre charte graphique.

3. **Modifier les messages et options visibles :**
   - Si vous souhaitez personnaliser davantage l’apparence ou les messages de l’interface, vous pouvez modifier les fichiers CSS ou HTML :
     - Les fichiers sont situés sous :
       ```
       /usr/local/CyberCP/public/css
       ```
     - Vous pouvez ajuster les styles ou ajouter de nouvelles fonctionnalités via ces fichiers.

4. **Ajouter des liens utiles pour les clients :**
   - Vous pouvez ajouter des liens ou des tutoriels dans le tableau de bord de CyberPanel pour aider vos clients.
   - Vous devrez peut-être personnaliser les templates dans le répertoire d'administration de CyberPanel pour afficher ces liens dans des sections spécifiques.

---

## Configuration des services de messagerie (MX, TXT, DKIM, MSPMX)

Lors de la création d'un service de messagerie pour un client, CyberPanel vous permet de configurer les enregistrements DNS nécessaires pour garantir la livraison correcte des e-mails et la sécurité du domaine.

### Enregistrements à configurer

1. **Enregistrement MX (Mail Exchange)** :
   L'enregistrement MX indique le serveur responsable de la réception des e-mails pour un domaine.
   - Exemple de configuration MX :
     ```
     domaine.com.    IN    MX    10 mail.domaine.com.
     ```

2. **Enregistrement TXT** :
   L'enregistrement TXT est utilisé pour diverses vérifications de sécurité, comme le SPF (Sender Policy Framework) qui définit quels serveurs peuvent envoyer des e-mails pour ce domaine.
   - Exemple d'enregistrement TXT pour SPF :
     ```
     domaine.com.    IN    TXT    "v=spf1 mx ~all"
     ```

3. **Configuration DKIM (DomainKeys Identified Mail)** :
   DKIM permet de signer numériquement les e-mails pour vérifier leur authenticité.
   - Après avoir activé DKIM dans CyberPanel, un enregistrement TXT sera généré. Voici un exemple :
     ```
     default._domainkey.domaine.com.    IN    TXT    "v=DKIM1; k=rsa; p=MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA..."
     ```

4. **Enregistrement MSPMX** :
   Un enregistrement MSPMX est utilisé pour spécifier le serveur de messagerie primaire. CyberPanel le configure automatiquement lors de l'ajout d'un service de messagerie.
   - Exemple d'enregistrement MSPMX :
     ```
     domaine.com.    IN    MX    20 mail.domaine.com.
     ```

### Processus automatisé pour chaque service mail commandé

À chaque fois qu'un client commande un service de messagerie, les enregistrements suivants sont automatiquement configurés pour son domaine :
- **Enregistrement MX** : Configuration du serveur de messagerie principal.
- **Enregistrement TXT** : Pour le SPF et autres vérifications.
- **Enregistrement DKIM** : Génération d'une clé DKIM pour signer les e-mails.
- **Enregistrement MSPMX** : Associer un serveur MSPMX.

CyberPanel gère ces configurations de manière transparente, et vous pouvez visualiser ces paramètres dans le panneau de gestion DNS de CyberPanel.

---

## Ressources supplémentaires

- [Documentation officielle de CyberPanel](https://cyberpanel.net/documentation/)
- [Forum d’assistance CyberPanel](https://community.cyberpanel.net/)
- [Documentation WHMCS](https://docs.whmcs.com/)

---

Merci d'avoir consulté cette documentation. Si vous avez des questions ou avez besoin de plus de détails, n'hésitez pas à consulter les ressources supplémentaires ou à poser vos questions sur le forum !
