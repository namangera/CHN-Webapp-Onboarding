[_English follows_](#description-starting-guide)

# Description - Guide de démarrage

Ce guide à pour but d'expliquer les différents morceaux qui doivent être mis en place avant de commencer les activités de développement pour l'équipe du Réseau Hydrospatial Canadien.

Sujets couvert par ce guide :

1. [Configuration GitLab](#1-configuration-gitlab)
2. [Configuration Conda](#2-configuration-conda)
3. [Configuration VScode](#3-configuration-vscode)

## 1. Configuration Gitlab

**N.B.** : Cette section est largement inspirée de la méthode de travail git disponible sur le wiki du CCCOT, mais contient quelques détails additionnels qui sont important pour utiliser git dans la nouvelle instance de GitLab.

### Prérequis

Vous aurez besoin de l'application [Git Bash](https://git-scm.com/downloads). Assurez-vous qu'elle est bel et bien installée avant de commencer. Assurez-vous également d'être membre du sous groupe du [Canadian Hydro Network](https://git.geoproc.geogc.ca/canadian-hydrospatial-network) qui contient le projet sur lequel vous travaillez.

### Message d'erreur fréquent

À n'importe quel point dans le processus Git, si vous rencontrez ce message d'erreur :

![error_01](uploads/ee86f1d9cc6a4d3e14c1d3dfa8516c37/error_01.jpg)

Il suffit de rajouter l'argument `http.sslVerify=False` dans votre commande. ex.: 

```
git http.sslVerify=False fetch --all
```

Il est également possible d'enrayer le problème de façon définitive si c'est quelque chose qui revient fréquemment. Dans **Git Bash**, positionnez-vous dans le répertoire de:

```
git config --global http.sslVerify false
```

### **a)** Créer un token d'accès personnel.

1. Cliquer sur votre photo de profil pour ouvrir le menu déroulant
2. Cliquer sur **edit profile**

![01_token](uploads/bb9a733e5c71e722c4050a6eda7aeb90/01_token.jpg)

Dans le menu **Access Token** :

3. Donner un nom à votre token
4. Vous pouvez spécifier une date d'expiration au besoin. Cependant, s'il s'agit d'un token dédié à vos activités de développement, il est recommandé de supprimer la date d'expiration en cliquant sur le **x**. Cela vous évitera de devoir créer plusieurs token.
5. Choisir **write_repository** pour permettre la lecture et l'écriture sur les répertoires des projets de l'équipe.
6. Cliquer sur le bouton **Create personnal access token**.

![02_token](uploads/c4de3200d75d96d3452c6672ead95c2d/02_token.jpg)

7. Sauvegarder votre token dans un fichier texte dans un endroit sûr. Ce token vous servira de mot de passe et vous sera demandé lorsque vous clonerez un projet.

![03_token](uploads/6c5a19990ce812a6f6d0cc8f0b231985/03_token.PNG)

### **b)** Créer une divergence (fork)
1. Retourner sur la page principale du projet officiel distant que vous voulez clonez et cliquer sur le bouton **fork** pour faire une copie du projet qui sera votre version de travail.

![01_git](uploads/7eea63fab78600efebede0a0412c3801/01_git.jpg)

> **Note**: On appelle aussi le projet officiel distant, le **Upstream**.

1. Dans le menu déroulant **Select a namespace** de l'option **Project URL**, sélectionner votre nom d'utilisateur.
2. Mettre le **Visibility level** à **Internal**.
3. Cliquer sur le bouton **Fork project**.

![02_git](uploads/752877d77c0fc63b0c6d12c35d20e9bc/02_git.jpg)

Une fois que la fork du projet est faites, vous pouvez maintenant accéder #a votre projet personnel distant en cliquant sur le chiffre qui se trouve à la droite du bouton **fork** de la page du Upstream ou bien directement à partir de votre compte.

> **Note**: On appelle aussi le projet personnel, le **Origin**.

### **c)** Cloner un projet

1. Ouvrez un fenêtre de commande Git Bash.
2. Assurez-vous d'être sur la page de votre projet personnel distant. Vous pouvez facilement confirmer si vous êtes sur la bonne page en regardant l'addresse URL de la page. Si celle-ci contient votre username, vous êtes au bon endroit.

![03_git](uploads/63de7ee59b7668038fde1b992d54d804/03_git.jpg)

Par contre, si vous voyez plutôt **canadian-hydrospatial-network**, vous êtes sur la page du upstream.

3. Cliquer sur le bouton **Clone**.
4. Copier le lien https.

![04_git](uploads/84080373ac86dc59d19b3eb92d1779b4/04_git.jpg)

5. Dans **Git Bash**, positionnez-vous dans le répertoire de votre choix et cloner le répertoire de votre projet en utilisant les lignes de commande suivantes :

```
cd <chemin vers votre répertoire>
git clone <lien https copié>
```

> **Note**: Si c'est le premier projet du groupe que vous clonez, une fenêtre d'authentification apparaîtra. Utiliser votre nom d'utilisateur Gitlab et le token que vous avez enregistré plus tôt comme mot de passe.

6. Positionner vous dans le répertoire du projet que vous venez de cloner :

```
cd <nom du projet cloné>
```

### **d)** Ajouter la référence au projet officiel distant

1. Aller sur la page du projet officiel distant.

![05_git](uploads/cf7d4bf62e450bc85600122d29592bf1/05_git.jpg)

2. Cliquer sur le bouton **Clone**.
3. Copier le lien https.

![06_git](uploads/f796ca7a70ede910c3fe197a7ec1fd51/06_git.jpg)

4. Dans **Git Bash**:

```
git remote add upstream <lien https copié>
```

Pour vérifier que les références au projet personnel distant et au projet officiel distant ont bien été configurées, utiliser la commande suivante dans **Git Bash**:

```
git remote -v
```

![07_git](uploads/0493924e731e0e9c08f3c097b012961d/07_git.jpg)

Vous devriez retrouver les url contenant votre username Gitlab dans les lignes **origin** et le nom du groupe canadian-hydro-spatial dans les lignes **upstream**.

### **e)** Créer une branche de travail

1. Se positionner dans le répertoire du projet.
2. Charger les fichiers à jour du projet officiel

```
git fetch upstream
```

3. Se positionner sur la branche **main** du projet

```
git checkout main
```

4. Baser notre projet local sur la branche **main** du projet officiel distant

```
git rebase upstream/main
```

5. Créer une nouvelle branche

```
git checkout -b <nom de votre nouvelle branche> upstream/main
```

6. Pousser la branche sur votre projet personnel distant

```
git push origin <nom de votre nouvelle branche>
```

> **Note**: À partir de ce moment, tout les éléments sont en place pour le développement et commencer à modifier le code du projet.

### **f)** Enregistrer les modifications

1. Afficher les fichiers qui ont été modifiés, mais qui n'ont pas encore été enregistrées :

```
git status
```

![08_git](uploads/eb124900396e2a7cb15b67b5d72399e3/08_git.jpg)

2. Ajouter les fichiers au staging.

```
git add <nom du fichier à ajouter>
```

ou si vous désirez ajouter tous les fichiers

```
git add *
```

3. Vérifier que les fichiers ont bel et bien été ajouté au staging.

```
git status
```

![09_git](uploads/c6e7720236e01997b04bfba5ae5a9b36/09_git.jpg)

Les fichiers prêts à être enregistrer devraient maintenant apparaître en vert.


4. Enregistrer les modifications

```
git commit -m "<message qui décrit les modifications>"
```

![10_git](uploads/31fe3c42a6e6db64449a15bf31ecf59d/10_git.jpg)

Vous pouvez retrouver plus d'informations à propos de la structure et du contenu des messages de commit [ici](https://gccode.ssc-spc.gc.ca/geobase/geosys/api-rest/-/blob/master/CONTRIBUTING.md). L'important est d'inclure un message court et évocateur afin de bien communiquer les modifications apportées.

### **g)** Enregistrer les modifications dans le projet personnel distant (origin)

1. Assurez-vous d'être synchronisé avec le projet officiel distant (upstream)

```
git fetch --all
```

![11_git](uploads/713d290a625fdf0531b276ae50be1939/11_git.jpg)

2. Baser votre projet local sur la branche **main** du projet officiel distant

```
git rebase upstream/main
```

![12_git](uploads/b3e14954076182acb75efa37af9f0d2f/12_git.jpg)


3. Pousser les modifications dans le projet personnel distant.

```
git push -f origin <nom de votre branche>
```

![13_git](uploads/b1269e3c2969c6773e4c5b05a4ddedcb/13_git.jpg)



#### Ressources

> Git Cheat Sheet : https://www.atlassian.com/git/tutorials/atlassian-git-cheatsheet
>
> Méthode de travail git : https://wiki.cits.rncan.gc.ca/M%C3%A9thode_de_travail_GeoSys_dans_GGCode

## 2. Configuration Conda

_Section à venir_

## 3. Configuration VScode

_Section à venir_

---

## Description - Starting guide

The purpose of this guide is to explain the various components that need to be in place before starting development for the Canadian Hydrospatial Network team.

Topics covered by this guide :

1. [Gitlab setup](#1-gitlab-setup)
2. [Conda setup](#2-conda-setup)
3. [VScode setup](#3-vscode-setup)

## 1. Gitlab setup

**N.B.** : This section is largely inspired by the git workflow available on the CCMEO wiki, but contains some additional details that are important for using git with the new GitLab instance.

### Prerequisites

You will need the [Git Bash](https://git-scm.com/downloads) application. Make sure it is installed before you start. Also make sure you are a member of the [Canadian Hydro Network](https://git.geoproc.geogc.ca/canadian-hydrospatial-network) subgroup that contains the project you are working on.

### Common error message

At any point in the Git process, if you encounter this error message :

![error_01](uploads/ee86f1d9cc6a4d3e14c1d3dfa8516c37/error_01.jpg)

Just add the argument `http.sslVerify=False` in your command. eg : 

```
git http.sslVerify=False fetch --all
```

It is also possible to fix the problem permanently if it is something that happens frequently. In **Git Bash**, while in the working directory:

```
git config --global http.sslVerify false
```

### **a)** Create a personal access token.

1. Click on your profile picture to open the drop-down menu
2. Click on **edit profile**

![01_token](uploads/bb9a733e5c71e722c4050a6eda7aeb90/01_token.jpg)

In the **Access Token** menu :

3. Name your token
4. You can specify an expiration date if needed. However, if it is a token dedicated to your development activities, it is recommended to remove the expiration date by clicking on the **x**. That way, you avoid having to create multiple tokens.
5. Select **write_repository** to allow read and write on the team's project directories.
6. Click on the **Create personnal access token** button.

![02_token](uploads/c4de3200d75d96d3452c6672ead95c2d/02_token.jpg)

7. Save your token in a text file in a safe place. This token will act as your password and will be requested when you clone a project for the first time.

![03_token](uploads/6c5a19990ce812a6f6d0cc8f0b231985/03_token.PNG)

### **b)** Create a fork
1. Go back to the page of the project you want to clone and click on the **fork** button to make a copy of the project that will become your working version.

![01_git](uploads/7eea63fab78600efebede0a0412c3801/01_git.jpg)

> **Note**: **Upstream** also refers to the official version of the project.

1. In the **Select a namespace** drop-down menu of the **Project URL** option, select your username.
2. Select the **Internal** option in the **Visibility level** section.
3. Click on the **Fork project** button.

![02_git](uploads/752877d77c0fc63b0c6d12c35d20e9bc/02_git.jpg)

Once your fork is done, you can access it by clicking on the number to the right of the **fork** button on the Upstream page or directly from your account.

> **Note**: **Origin** also refers to your personnal version of the project.

### **c)** Clone a project

1. Open a Git Bash command window.
2. Make sure you are on your remote personal project's page. You can easily confirm if you are on the right page by looking at the URL of the page. If it contains your username, you are in the right place.

![03_git](uploads/63de7ee59b7668038fde1b992d54d804/03_git.jpg)

However, if you see **canadian-hydrospatial-network**, you are on the upstream's page.

3. Click on the **Clone** button.
4. Copy the https link.

![04_git](uploads/84080373ac86dc59d19b3eb92d1779b4/04_git.jpg)

5. In a **Git Bash** command window, go to the directory of your choice and clone the directory of your project using the following command lines :

```
cd <path to your working directory>
git clone <copied https link>
```

> **Note**: If this is the first project in the group you are cloning, an authentication window will appear. Use your Gitlab username and the token you registered earlier as your password.

6. Go in the directory of the project you just cloned :

```
cd <name of the cloned project>
```

### **d)** Add the reference to the official project (Upstream)

1. Go to the official project's page.

![05_git](uploads/cf7d4bf62e450bc85600122d29592bf1/05_git.jpg)

2. Click on the **Clone** button.
3. Copy the https link.

![06_git](uploads/f796ca7a70ede910c3fe197a7ec1fd51/06_git.jpg)

4. In a **Git Bash** command window:

```
git remote add upstream <copied https link>
```

To check if the references to the remote personal project (origin) and the remote official project (upstream) have been set correctly, use the following command in **Git Bash**:

```
git remote -v
```

![07_git](uploads/0493924e731e0e9c08f3c097b012961d/07_git.jpg)

You should find the url containing your Gitlab username in the **origin** lines and the name of the canadian-hydro-spatial group in the **upstream** lines.

### **e)** Create a work branch

1. Move to the project directory.
2. Download updated official project files

```
git fetch upstream
```

3. Move to the **main** branch of the project

```
git checkout main
```

4. Base your local project on the **main** branch of the official remote project

```
git rebase upstream/main
```

5. Create a new branch

```
git checkout -b <name of your new branch> upstream/main
```

6. Push the new branch on your remote personal project

```
git push origin <name of your new branch>
```

> **Note**: From this point on, all the elements are in place for development.

### **f)** Commit changes

1. Show files that have been modified but not yet saved :

```
git status
```

![08_git](uploads/eb124900396e2a7cb15b67b5d72399e3/08_git.jpg)

2. Add files to the staging.

```
git add <name of the file you want to add>
```

or if you want to add all the files

```
git add *
```

3. Check that the files have been added to the staging.

```
git status
```

![09_git](uploads/c6e7720236e01997b04bfba5ae5a9b36/09_git.jpg)

Files ready to be saved should now appear in green.

4. Save changes

```
git commit -m "<short message describing the changes made>"
```

![10_git](uploads/31fe3c42a6e6db64449a15bf31ecf59d/10_git.jpg)

You can find more information about the structure and content of commit messages [here](https://gccode.ssc-spc.gc.ca/geobase/geosys/api-rest/-/blob/master/CONTRIBUTING.md). The important thing is to include a short, evocative message to communicate the changes made.

### **g)** Save changes in the remote personal project (origin)

1. Make sure you are synchronized with the official remote project (upstream)

```
git fetch --all
```

![11_git](uploads/713d290a625fdf0531b276ae50be1939/11_git.jpg)

2. Base your local project on the **main** branch of the official remote project

```
git rebase upstream/main
```

![12_git](uploads/b3e14954076182acb75efa37af9f0d2f/12_git.jpg)


3. Push the changes into the remote personal project.

```
git push -f origin <name of your branch>
```

![13_git](uploads/b1269e3c2969c6773e4c5b05a4ddedcb/13_git.jpg)



#### Resources

> Git Cheat Sheet : https://www.atlassian.com/git/tutorials/atlassian-git-cheatsheet
>
> Git Workflow : https://wiki.cits.rncan.gc.ca/M%C3%A9thode_de_travail_GeoSys_dans_GGCode
