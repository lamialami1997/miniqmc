# Optimisation MiniQMC

Dans ce dossier, il y a :   
- rapport au format PDF intitulé "rapport.pdf";
- un dossier "sequential" comprenant les mêmes dossiers envoyés pour la version séquentielle uniquement et le code source pour la version séquentielle;
- un dossier "parallel" comprenant les sorties Oneview en parallèle et le code source pour la version parallèle.

L'exécution de ce code requiert la librairie MKL de OneAPI et la librairie OpenMP.  
Les commandes pour appliquer `cmake`, compiler et exécuter le code en séquentiel (1 processus MPI et 1 thread OpenMP) sont :  
```
cd sequential/build
cmake -DCMAKE_CXX_COMPILER=mpicxx -DCMAKE_BUILD_TYPE=RelWithDebInfo  ..
sed -i 's/-O2/-O3/g' CMakeCache.txt
make -j 8
OMP_NUM_THREADS=1 ./bin/miniqmc -g "2 2 2"
```
Pour la version parallèle du code de base, par exemple 12 threads OpenMP et 4 processus MPI, ce sont les commandes suivantes :
```
cd parallel/build
cmake -DCMAKE_CXX_COMPILER=mpicxx -DCMAKE_BUILD_TYPE=RelWithDebInfo -DQMC_MPI=1 ..
sed -i 's/-O2/-O3/g' CMakeCache.txt 
make -j 8
OMP_NUM_THREADS=12 mpirun -n 4 ./bin/miniqmc -g "2 2 2"
```
À noter, pour permettre un niveau d'optimisation O3, il faut lancer entre le `cmake` et le `make` la commande `sed` comme montrer.

Pour nettoyer le dossier `build`, il y a `clean.sh` pour cela à l'intérieur : `bash clean.sh`
