# Réponses du TP final Git

## Mission 5 : analyse de l'historique

1. L'identifiant du premier commit c'est fbe54c9. Je l'ai trouvé avec git log --oneline --reverse, le premier de la liste est le plus vieux.

2. Le commit qui ajoute la page Contact c'est cb4aaf7, c'est là que j'ai créé contact.html. Ensuite j'ai fait un deuxième commit (4af2978) pour les champs obligatoires, et le commit a3fa1e2 c'est la fusion dans main.

3. Pour l'instant il y a 11 commits. Je les ai comptés avec git rev-list --count HEAD. Les commits de fusion sont comptés aussi.

4. Pour voir l'historique en graphique j'ai utilisé : git log --oneline --graph --decorate --all

5. Pour regarder un commit de la fonctionnalité Contact en détail j'ai fait : git show cb4aaf7. Ça montre l'auteur, la date, le message et les lignes ajoutées.
