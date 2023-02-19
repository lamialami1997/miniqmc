# Base 
##pour la compilation séquentiel sans MPI :
dans build/src/config.h
désctiver OpenMP
mettre en commentaire 
```c
/* Enable OpenMP parallelization. */
//#define ENABLE_OPENMP 1
```
```bash
cd build
cmake -DCMAKE_CXX_COMPILER=g++ ..
make -j 4
```
##MAQAO séquentiel sans MPI ni OpenMP
dans build/src/config.h
désctiver OpenMP
mettre en commentaire 
```c
/* Enable OpenMP parallelization. */
//#define ENABLE_OPENMP 1
```
l'execution du code : 
```bash
 taskset -c 3 /home/lamiadendani/maqao.intel64.2.16.0/maqao.intel64 oneview -R1 -- ./miniqmc -g " 2 2 2"
```
#Optimisation 
## ajout de flags de compilation séquentiel
```bash
	cd build
	cmake -DCMAKE_CXX_COMPILER=g++ CMAKE_CXX_FLAGS="-Ofast -march=native -finline-functions -funroll-loops -ftree-loop-vectorize -ftree-vectorize" ..  
    make -j 4
```
Expliquer les flags
