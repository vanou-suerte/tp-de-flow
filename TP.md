# Utilisation de GitHub

## Créer un compte GitHub

1. **Rendez-vous sur le site web [GitHub](https://github.com). Rentrez votre adresse e-mail ensg puis cliquez sur le bouton "inscrivez-vous sur GitHub".**

   ![git_hub_home_page](prez/img/git_hub_home_page.png)

2. **Remplissez le formulaire avec les informations requises puis finalisez l'inscription. **

   ![formulaire_inscription](img/formulaire_inscription)

3. **Connectez vous ensuite sur votre nouveau compte.** Vous arrivez sur une page d'accueil ressemblant à l'image ci-dessous.

   ![page_accueil_1](prez/img/page_accueil.png)

4. **Allez dans le menu utilisateur, sélectionnez les paramètres, puis allez dans la section "Credentials". **Vous arrivez sur un menu permettant de gérer les options d'identifications.

   ![options_identification](prez/img/options_identification.png)

   Pour pouvoir cloner, ou pousser des modifications sur GitHub, il faut parfois s'authentifier, et GitHub ne permet pas l'authentification par mot de passe dans ces cas là. Il faut donc utiliser une des options suivantes :
   - Utiliser un token : un mot de passe généré aléatoirement, avec des accès potentiellement restreint. Un même compte GitHub peut avoir plusieurs token, avec des rôles différents.
   - Certaines applications peuvent être directement autorisées à accéder à votre GitHub, via l'authentification par mot de passe. Une fois cette autorisation donnée, plus besoin de s'authentifier.
   - Utiliser le protocole de communication `ssh` pour communiquer avec GitHub. Ce protocole sécurise la communication entre deux ordinateurs via l'utilisation de paires de clé publique/privée. GitHub peut donc utiliser une clé publique `ssh` que vous lui fournissez pour déchiffrer vos communications via ce protocole.

5. **Sélectionnez l'option "personnal access token (classic)", puis choisissez "generate new token (classic)". Donnez un nom au token, et sélectionnez les acions que ce token doit permettre d'effectuer.** Dans notre cas, on se contentera des actions liées aux repositories (option "repo"). **Ensuite validez en cliquant sur "generate token".**

   ![setup_token](prez/img/setup_token.png)

   **Copiez ensuite le token et collez le dans un nouveau fichier texte. **

   ![github_token](prez/img/github_token.png)

## Création d'un nouveau dépôt sur GitHub

4. On va créer un dépôt git, mais contrairement au cours 2, on va le faire directement sur GitHub. **Cliquez sur le bouton "Create project"**. Une nouvelle fenêtre s'ouvre pour paramétrer votre nouveau dépôt. **Créez un dépôt <u>privé</u> avec un <u>README généré automatiquement</u>.**

   ![create_repo](prez/img/create_repo.png)

5. **Récupérez le projet sur votre ordinateur grâce à la commande `git clone`.**

## Communication entre GitHub et un dépôt local

6. **En local sur votre ordinateur, créez une nouvelle branche _develop_ et placez vous sur cette branche.**

7. **Écrivez une description du projet dans le README.** Le projet consistera en une bibliothèque de calcul géométrique.

8. **Faites un commit avec ce changement, puis poussez ces changements avec la commande `git push`.** Vous obtenez un message d'erreur : `fatal: The current branch develop has no upstream branch`. Cette erreur se produit car on essaie de pousser une branche qui n'existe pas encore sur le dépôt GitHub.

   Pour régler ce problème, il faut indiquer à git de créer une nouvelle branche équivalente sur le dépôt GitHub. On fait ça en rajoutant l'options `--set-upstream origin develop` à la commande `push`. Le terme `origin` désigne le serveur à partir duquel on a cloné notre dépôt, ici il s'agit de GitHub. **Lancez la commande , puis retournez sur la page d'accueil de votre projet sur github et rechargez la.** Le README affiché sur cette page d'accueil a-t-il changé ? Si non, que faire pour afficher la nouvelle version ?

9. **Créez une nouvelle branche _calcul_de_distances_ sur votre projet dans github.** Attention à bien prendre la branche _develop_ comme source de cette nouvelle branche.

   ![github_project_page_2](prez/img/github_project_page_2.png)

10. **Toujours sur GitHub, assurez-vous que vous êtes bien sur la nouvelle branche, puis modifiez le README pour ajouter une section "fonctionnalités" contenant une liste à puces avec un item "calcul des distances".** L'enregistrement crée un nouveau commit.

    ![modif_fichier_github_1](prez/img/modif_fichier_github_1.png)

    ![modif_fichier_github_2](prez/img/modif_fichier_github_2.png)

    ![modif_fichier_github_3](prez/img/modif_fichier_github_3.png)

11. **Sur votre dépôt local, récupérez les modifications avec la commande `git pull`, puis placez vous dans la branche _calcul_des_distances_.**

12. **Créez un dossier `src`, puis créez un fichier `calcul_distances.py` dans le dossier `src`. Dans ce fichier, créez une fonction calculant la distance entre deux points 3D** (vous pourrez vous aider de la bibliothèque `math` pour calculer le calcul de la racine carrée). La signature de la fonction est :

    ```python
    def distance_pt_pt(coords1, coords2):
    ```

13. **Faites un commit, puis poussez vos modifications sur GitHub.**

14. **Retournez sur github. Créez une `pull request` pour fusionner la branche _calcul_de_distances_ dans la branche _develop_.**

    ![pull_request_1](prez/img/pull_request_1.png)

    ***

    ![pull_request_2](prez/img/pull_request_2.png)

    ***

    ![pull_request_3](prez/img/pull_request_3.png)

15. **Retournez sur votre dépôt local.** <u>Ne faites PAS de `git pull` pour l'instant !</u> **Déplacez vous sur la branche _develop_, puis créez une nouvelle branche _calcul_perimetre_. Recréez le dossier `src`, puis créez dedans un fichier `calcul_perimetre.py`, et copiez le code suivant dedans :**

    ```python
    def perimetre_polygone(coords):
        pass
    ```

16. **Faites un commit, puis replacez vous dans la branche _develop_.**

17. **Faites une fusion de _calcul_perimetre_ dans _develop_.**

18. **Poussez vos modifications.** Vous obtenez une erreur car vous ne pouvez pas pousser des modifications sur un dépôt distant si votre dépôt n'est pas à jour avec ce dépôt.

    **Pour régler ce problème, faites un `git pull`, puis retentez le `git push`.**

    Si vous obtenez un message d'erreur lors du `git pull` vous demandant de réconcilier des branches divergentes, tapez la commande `git config pull.rebase false`, puis retentez le `git pull` et le `git push`.

19. **Retournez sur GitHub, et placez vous dans la branche _develop_. Modifiez le fichier `calcul_perimetre.py` en codant le corps de la fonction `perimetre_polygone`.** Pour cela, il faudra faire appel à la fonction `distance_pt_pt` définie dans le fichier `calcul_distances.py`.

20. **Sur votre git local, écrivez le code suivant dans le corps de la fonction `perimetre_polygone`.** Assurez-vous que vous êtes bien sur la branche `develop` avant de coder.

    ```python
    # On modifie le corps de cette fonction de manière à créer un conflit lors de l'execution de la commande git pull.
    	return -1
    ```

21. **Faites un commit avec vos changements, puis mettez votre dépôt à jour avec un pull.** Git essaie de fusionner les modifications, mais obtient un conflit. Il vous faut donc résoudre le conflit.

    **Résolvez le conflit (en gardant la version venant de GitHub) puis validez la fusion avec la commande `git merge --continue`.**

22. **Pour finir, supprimez votre projet sur votre gitHub .**

    ![suppression_1](prez/img/suppression_1.png)

    ![suppression_2](prez/img/suppression_2.png)
