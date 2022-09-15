# Git

# Partie 1

## Prise en main rapide
Github dispose d'un outil permettant la prise en main rapide de certaines commandes git [site](https://try.github.io/levels/1/challenges/1).
1. Explorer [visualizing-git](http://git-school.github.io/visualizing-git/) et [learn git branching](https://learngitbranching.js.org/)

# Partie 2

## Mise en place

2. Créez un compte sur GitHub pour chaque utilisateur.
3. Configurez votre client git pour utiliser cet identifiant

```bash
# Hints:
# https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token
# Cache for 1 week
git config --global credential.helper "cache --timeout=604800"
# or use token in remote url
git remote set-url origin https://[USERNAME]:[TOKEN]@github.com/[ORGANIZATION_OR_USERNAME]/[REPO].git
# or
git remote add origin https://[USERNAME]:[TOKEN]@github.com/[ORGANIZATION_OR_USERNAME]/[REPO].git
```

## Premiers pas
4. Dans github, créez un premier dépôt nommé 'TP-Git' et le cloner sur votre machine de travail
5. Ajoutez un fichier authors.html au dépôt de travail, contenant un titre et une liste avec votre prénom.
6. Verifiez l'état de votre dépôt (status). (il doit mentionner l'ajout d'un nouveau fichier dans votre copie de travail)
7. Indexez le fichier créé (le passer en staging). Vérifiez que les modifications ont été placées dans l'index. Puis observez les différences (git diff ...) entre l'index et la dernière version du dépôt.
8. Commitez votre modification. N'oubliez pas le message de commit.
9. Vérifiez l'état de votre dépôt.
10. Affichez la liste des changements effectués dans le dépôt (log). Notez le numéro (le sha1) du dernier commit.

### Le site de streaming
Vous allez maintenant créer votre site de streaming en utilisant le versionning Git durant le developpement.

11. Cherchez sur le web un template html et css gratuit, opensource, **simple, léger** et joli pour servir de base à votre site de streaming. Si vous êtes plus à l'aise avec, vous pouvez aussi utiliser un framework comme foundation ou bootstrap ...
12. Ajoutez votre template au dépôt. Puis modifier/supprimer/ajouter des fichiers jusqu'à obtenir une base de site présentant le nom et la miniature de deux films. Chaque commit doit maintenir le dépot dans un état cohérent, (ajouter un fichier, supprimer du contenu non utilisé, modifier un fichier) et vous devez effectuer au moins 5 modifications (5 commits).
  * profitez de chaque étape pour essayer les commandes:
    * git diff avant un add
    * git diff --cached après un add
13. Affichez la liste des changements. Essayez des paramètres d'affichage différents (--graph ou --oneline).
14. Quand vous êtes satisfait de votre base de travail, poussez les modifications sur le dépôt distant.

## Annuler une modification et retourner dans le passé.
15. Faites une modification sur un film, ajoutez la à l'index mais **ne la commitez pas**. Faites des diff pour regarder la modification. Vous changez maintenant d'avis et vous ne souhaitez pas commiter ces modifications. Faites un git reset sur le fichier puis vérifiez le résultat de la commande en regardant le statut du dépôt.
16. Votre modification n'est plus indexé, mais elles sont toujours présentes sur le/les fichier/s. Supprimer ces modifications avec la commande checkout sur le/les fichiers. Vérifiez avec git status qu'il n'y a plus de modifications à commiter.
17. Regardez l'historique de votre dépôt (log). Choisissez un commit dans la liste (sauf le dernier). Faites un `git checkout`sur le commit ID du commit que vous avez choisi. Vérifier que votre site est revenu dans l'état correspondant à ce commit. Observer ce qu'affiche la commande git status.
18. Affichez l'historique du dépôt. Git log n'affiche plus les commits plus récents. Ajoutez l'option --all.
19. Retournez à la version la plus récente de votre dépôt. (le commit le plus récent de la branche master, est toujours pointé par le label `master`. Une fois fait, vérifiez l'état de votre site, puis l'état de votre dépôt.

## Travailler à plusieurs.
20. Le propriétaire du dépôt sur GitHub doit ajouter un collaborateur pour qu'il puisse directement pousser ses modifications. Pour cela il suffit de se rendre sur l'interface web de github et dans les configurations du dépôt *TP-Git* ajouter un collaborateur. (Attention le nouveau collaborateur va recevoir un mail où il doit accepter d'être ajouté au projet).
21. Cloner une seconde fois le dépôt. Idéalement si vous avez deux machines sur une seconde machine sinon dans un autre répertoire (par exemple TP-Git-user2) à coté du premier répertoire de travail. Assurez-vous que cette copie de travail utilise bien les identifiants du deuxième collaborateur (user2 dans la suite de l'énoncé).
22. User2: ajoutez votre prénom à la liste des auteurs.
23. User1: récupérez les modifications de User2 avec un pull du dépôt distant.
24. Vous allez faire un conflit.
  * User2: Modifiez un titre de film et poussez les modifications.
  * User1: en même temps que user2 fait une modification, vous allez modifier tous les titres pour qu'ils s'affichent en italique. Puis vous allez pusher les modifications. Si un conflit apparaît lors du push vous devez résoudre le conflit avant de pouvoir pusher de nouveau.

## Branches
25. User1: vous allez créer une branche 'feature-mark' dans laquelle vous allez développer la fonctionnalité pour ajouter une note à chaque film. Vous pouvez pusher votre branche régulièrement (la première fois avec `git push -u origin feature-mark`)
26. User2: En même temps que user1, vous allez créer une autre branche 'feature-themes' pour développer la fonctionnalité, liste de thèmes du film. **Mais vous ne devez pas pusher votre branche sur le dépôt distant**.
27. Quand la feature de user1 est prête, il la merge dans master et push les modifications de master sur le dépôt distant.
28. La branche de User2 n'est plus à jour par rapport à l'avancement de master. Il peut la mettre à jour de manière automatique avec un commit de merge en effectuant un git pull sur sa branche de feature. Une fois la branche à jour, mergez la dans master et pousser les modifications de master sur le dépôt distant.
29. Refaire les 3 premières opérations de la section Branches avec des branches 'feature-social-header' pour ajouter des liens de réseaux sociaux dans le haut de page, et 'feature-login-header' pour ajouter un formulaire de login dans le haut de page. Cette fois ci, après que la première branche ait été mergé dans master, lors de la réintégration des modifications de master dans la deuxième branche (celle qui n'est pas à jour) vous allez rebaser la branche pour la mettre à jour avec `git pull --rebase=preserve`


## Revert

30. Sur master supprimez l'ensemble des films de votre site, commitez et pushez cette modification.
31. Cette modification était une erreur, vous allez effectuer la modification inverse du commit incriminé en utilisant la commande `git revert`. [doc git revert](https://git-scm.com/docs/git-revert)

## Rebase interractif

32. Faites une nouvelle branche de feature, contenant plusieurs commit (5 mini) dont des commit minim, ne pushez pas vos commits.
33. Faites un rebase interactif `git rebase -i` sur vos commits pour squasher les petits commits qui peuvent faire partie d'un plus gros commit.

# Partie 3

34. Faite un fork du repo github [lodelestra-edu/licence_2022_github](https://github.com/lodelestra-edu/licence_2022_github) et proposez une pull request pour ajouter un élément à la liste, ajouter une fonctionnalité ou une amélioration.
  * Liens utiles:
    * [working with forks](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/working-with-forks)
    * [creating a pull request from a fork](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/creating-a-pull-request-from-a-fork)
