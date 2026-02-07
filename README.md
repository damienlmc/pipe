# Pipe - Gestion simplifiée des librairies Python

`pipe` est un script shell qui permet d’installer, désinstaller ou lister rapidement des librairies Python à partir d’un fichier `.txt`. Il est conçu pour faciliter la gestion des dépendances Python sans avoir à taper des commandes `pip` complexes à chaque fois.

---

## Installation

Pour utiliser `pipe`, il suffit de définir l’alias dans votre terminal (par exemple dans votre `~/.bashrc` ou `~/.zshrc`) :



```
function pipe() { if [ "$1" = "-h" ]; then 
	echo "-i sert à installer des libs python avec un fichier txt exemple : pipe -i monfichier.txt" 
	echo "-u sert à désinstaller des libs python avec un fichier txt exemple : pipe -u monfichier.txt" 
	echo "-l sert à lister des libs python dans un fichier txt" 
elif [ "$1" = "-l" ]; then 
	pip list --format=freeze | cut -d= -f1 | grep -Ev '^(pip|setuptools|wheel)$' >> ./listPython.txt 
elif [ "$1" = "-u" ]; then 
	pip uninstall -r ./listPython.txt -y 
elif [ "$1" = "-i" ]; then 
	pip install -r ./listPython.txt 
else 
	echo "👉 pip permet d’installer et désinstaller des librairies Python rapidement et proprement, surtout via des fichiers .txt." 
fi 
} 
alias pipe=pipe
