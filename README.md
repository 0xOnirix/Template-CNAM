# Template CNAM Latex

Il s'agit d'un template Latex pour les rendus de mémoire et rapport du CNAM.

Il prend en compte les exigences de mise en forme du CNAM décrites dans le "Guide pour la rédaction du mémoire d'ingénieur CNAM", disponible ici : https://ecole-ingenieur.cnam.fr/medias/fichier/guide-redaction-memoire-vf-2023_1695841357339-pdf

Soit: 
- Police : Times New Roman
- Taille police : 12
- Interligne : 1.5

Le template utilise des variables (dans la section "Variables") pour la page de garde et pieds de page.

Il utilise également bibtex pour la bibliographie avec le fichier `biblio.tex`

## Configuration de LaTeX Workshop (VSCode)

Par défaut le plugin LaTeX Workshop de VSCode compile avec `pdflatex` et n'inclut pas la bibliographie et le glossaire.

`pdflatex` pose des problèmes d'encodage et de police, il vaut mieux lui préférer `xelatex`.

Pour changer tout ça, il faut :
- Ourvir `settings.json` dans VSCode (Ctrl+Maj+P -> Preferences: Open User Setting (JSON))
- Dans la partie `"latex-workshop.latex.tools":` ajouter:
```json
{
 "name": "makeglossaries",
 "command": "makeglossaries",
 "args": [
  "%DOCFILE%"
 ],
 "env": {}
}
```

- Dans la partie `"latex-workshop.latex.recipes":` ajouter:
```json
{
 "name": "makeglossaries",
 "tools": [
  "makeglossaries"
 ]
},
{
 "name": "xelatex ➞ makeglossaries ➞ bibtex ➞ xelatex x2",
 "tools": [
  "xelatex",
  "makeglossaries",
  "bibtex",
  "xelatex",
  "xelatex"
 ]
}
```
- Rajouter après la partie `"latex-workshop.latex.recipes":`: `"latex-workshop.latex.recipe.default": "xelatex ➞ makeglossaries ➞ bibtex ➞ xelatex x2",`

Cela va compiler en `xelatex` et prendre en charge le glossaire ainsi que la bibliographie