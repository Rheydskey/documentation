# 0 - Introduction
Ici nous ne ferons pas de programmation, juste des bonnes définitions pour être préparé.

## Préface (aka gate keeping)
Ce tutoriel vous expliquera comment créer les __bases__ d'un kernel.

Il faut savoir que c'est très dur et long. Beaucoup de kernel sont abandonnés... 

Il faut être déterminé et savoir coder, il faut bien connaitre le c ou c++ (le rust ne sera pas abordé dans ces tutoriels).
Il faut aussi comprendre l'assembleur, cependant, l'architecture de l'assembleur dépend de vos envies. Et il ne sera pas énormément présent.

Il ne faut pas commencer un kernel en parallèle d'apprendre un language, ce sera beaucoup plus dur.

Il ne faut pas croire que toutes vos application vont supporter windows, 
    
Vous ne pouvez pas coder un kernel en javascript.

Il est __très très très__ recommandé d'utiliser GNU/Linux, Windows complique la vie et wsl est très lent.

Il faut lire et ne pas juste faire de bêtes copier/coller.

## Introduction

### Qu'est ce qu'un kernel (ou noyau) ?

Un noyau est l'une des plus grosse partie d'un système d'exploitation. Il permet aux applications utilisateur d'accèder aux composants et périphériques. Il gère la mémoire, les fichiers, les processus, les drivers, les processeurs, une partie de la sécurité etc...

Un noyau est l'étape après le bootloader, ou le chargeur de boot.

### Qu'est ce qu'un bootloader ?

Un bootloader est généralement ce qui permet de faire passer de la machine qui démarre à une machine prête pour faire booter/démarrer le noyau 

Il est très important et très compliqué, il est recommandé de ne pas écrire son propre bootloader quand on débute, cela va vite vous décourager...

Un bootloader peut aussi charger des éléments important pour le kernel, comme des modules chargés dans le disques, l'A20, etc...
### L'architecture 

L'architecture c'est comment un processeur est structuré, comment il fonctionne, quel est son language d'assemblage. 
Il y a plusieurs architectures et un kernel peut en supporter plusieurs en même temps: 

- x86 
- riscV
- arm
- powerpc
- et bien d'autres...

L'architecture est importante, ici nous prenons le x86 car c'est l'architecture la plus utilisée.

Le x86 est divisé en *modes* : 


| nom anglais   |nom français   |taille de registre
|------------   |-------------  |-
|real mode      |mode réel      |16/20 bit
|protected mode |mode protégé   |32bit
|long mode      |mode long      |64bit

Nous utiliserons ici le mode long, car il est le plus récent, même si il a moins de documentation que le mode protégé.


### Comment ?
Comment coder un kernel ? 

Il faut prendre la route que l'on veut, mais il y a des éléments importants qu'il faut faire dans un ordre assez précis.

Vous pouvez dans certains cas le faire dans l'ordre que vous voulez mais il faut quand même une route... car parfois on se pose la question : quoi faire après ? 

Donc cette route ici est recommandé mais vous pouvez le faire de la manière dont vous l'entendez: 

- démarrage
- com // pour le debugging 
- gdt
- idt
- interruption  // pour le debugging d'erreur
- pit 
- gestion de mémoire physique
- pagination 
- multitache 

À partir d'ici, tout devient très subjectif vous pouvez enchainer sur le smp, le système de fichiers, les tâches utilisatrices, etc...
