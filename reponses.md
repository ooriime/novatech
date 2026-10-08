# Réponses du TP final Git

## Mission 5 : analyse de l'historique

1. L'identifiant du premier commit c'est fbe54c9. Je l'ai trouvé avec git log --oneline --reverse, le premier de la liste est le plus vieux.

2. Le commit qui ajoute la page Contact c'est cb4aaf7, c'est là que j'ai créé contact.html. Ensuite j'ai fait un deuxième commit (4af2978) pour les champs obligatoires, et le commit a3fa1e2 c'est la fusion dans main.

3. Pour l'instant il y a 11 commits. Je les ai comptés avec git rev-list --count HEAD. Les commits de fusion sont comptés aussi.

4. Pour voir l'historique en graphique j'ai utilisé : git log --oneline --graph --decorate --all

5. Pour regarder un commit de la fonctionnalité Contact en détail j'ai fait : git show cb4aaf7. Ça montre l'auteur, la date, le message et les lignes ajoutées.

## Mission 8 : commit local incorrect

J'ai utilisé git reset --soft HEAD~1. Cette commande enlève le dernier commit (Test affichage) de l'historique, en gardant mes modifications. HEAD revient sur le commit d'avant, mais je n'ai pas touché au contenu du fichier ni à la zone de staging.

Les modifications sont toujours là parce que --soft ne change que le pointeur de la branche. Mon fichier style.css contenait toujours la règle body { display: none; } et elle était même déjà prête à être commitée (en staging).

Pour supprimer aussi les modifications du fichier, il aurait fallu faire git reset --hard HEAD~1. Là tout est effacé, le commit et les changements dans le fichier.

Après le reset, j'ai enlevé la règle incorrecte de style.css avec git restore.

## Mission 9 : commit partagé à annuler

Pour annuler le commit Ajout promotion j'ai utilisé git revert HEAD. Cette commande crée un nouveau commit qui fait l'inverse du commit d'avant. Le commit Ajout promotion reste dans l'historique, on voit juste qu'il a été annulé après.

La méthode est différente de la mission 8 parce que là le commit avait déjà été récupéré par les autres membres de l'équipe. Si j'avais fait un reset, j'aurais supprimé le commit de mon côté, mais les autres l'auraient toujours et leur historique ne correspondrait plus au mien, ça ferait des problèmes. Avec revert j'ajoute juste un commit en plus, donc personne n'est perdu. Le reset on peut l'utiliser seulement quand le commit n'a été partagé avec personne, comme à la mission 8.

## Mission 11 : récupérer un seul commit

J'ai utilisé la commande git cherry-pick 42844c1 depuis la branche main. Cette commande copie un seul commit d'une autre branche sur la branche où je suis.

L'identifiant du commit d'origine (sur la branche test) est 42844c1. Une fois copié sur main, il a un nouvel identifiant : 48d44d2, parce que c'est une copie, pas le même commit.

Une fusion classique (git merge test) n'était pas adaptée parce qu'elle aurait pris tous les commits de la branche test. Il y aurait eu aussi le test des couleurs et le texte de test dans le footer, et je ne voulais pas les mettre sur main. Je voulais juste la correction de la faute.

## Mission 12 : version stable

J'ai créé la version avec git tag -a v1.0.0 -m "Première version stable de NovaTech" sur le dernier commit de main, puis j'ai affiché les infos avec git show v1.0.0.

Les trois nombres de 1.0.0 :
- Le premier (1) c'est MAJOR : il change quand il y a un changement qui n'est plus compatible avec les anciennes versions.
- Le deuxième (0) c'est MINOR : il change quand on ajoute une nouvelle fonctionnalité compatible.
- Le troisième (0) c'est PATCH : il change quand on corrige un bug sans rien changer d'autre.

La version suivante pour :
- une correction de bug mineur : 1.0.1
- une nouvelle fonctionnalité compatible : 1.1.0
- une refonte majeure incompatible : 2.0.0

## Mission 13 : fichiers à ignorer

J'ai créé un fichier .gitignore avec les lignes debug.log, cache/ et .env. Ce fichier est commité pour que la règle soit dans le projet. J'ai vérifié avec git status (seul .gitignore apparaît) et avec git check-ignore -v.

## Questions finales

1. La zone de travail c'est mes fichiers sur mon disque, ceux que je modifie. La zone de staging c'est ce que je prépare pour le prochain commit avec git add. L'historique c'est l'ensemble des commits déjà enregistrés dans le dépôt.

2. C'est mieux de travailler sur une branche dédiée pour ne pas casser la branche principale pendant que la fonctionnalité n'est pas finie. On peut aussi travailler à plusieurs en même temps, et si la fonctionnalité est abandonnée on supprime juste la branche.

3. Avec git reset (mission 8) on supprime le commit de l'historique, donc ça doit se faire seulement sur un commit pas encore partagé. Avec git revert (mission 9) on ajoute un nouveau commit qui annule l'ancien, l'historique n'est pas modifié, donc c'est sûr pour un commit que les autres ont déjà.

4. C'est utile quand j'ai un travail pas fini et que je dois changer de branche ou faire une correction urgente, sans faire un commit à moitié fini. Je mets de côté avec git stash et je récupère ensuite avec git stash pop.

5. Parce qu'une fusion complète récupère tous les commits de la branche, y compris ceux qu'on ne veut pas (tests, travail pas fini). Avec cherry-pick on prend seulement le commit voulu.

6. HEAD c'est un pointeur qui indique où je suis dans le dépôt, en général le dernier commit de la branche sur laquelle je travaille.

7. HEAD~2 c'est le commit qui se trouve 2 commits avant le commit actuel (HEAD).

8. Un tag sert à mettre une étiquette sur un commit précis, par exemple pour marquer une version comme v1.0.0 et la retrouver facilement.

9. Des petits commits précis sont plus faciles à lire et à comprendre. Si il y a un bug on retrouve plus vite d'où il vient, et on peut annuler ou récupérer un seul changement sans toucher au reste.

10. Certains fichiers ne doivent pas être versionnés car ils contiennent des infos secrètes (comme .env avec des mots de passe) ou ils sont générés automatiquement (logs, cache). Ça alourdit le dépôt pour rien et ça peut créer des conflits ou des failles de sécurité.
