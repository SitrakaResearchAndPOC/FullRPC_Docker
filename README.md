# FullRPC_Docker
# Installing Docker engine over ubuntu
## Add Docker's official GPG key:
```  
apt update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```  

```  
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
# INSTALLATION OF DEBIAN ON DOCKER
```  
docker pull debian:bullseye
```  
```  
docker run -tid --privileged -v /dev/bus/usb:/dev/bus/usb -v /tmp/.X11-unix:/tmp/.X11-unix:ro -v $XAUTHORITY:/home/user/.Xauthority:ro --net=host --env="DISPLAY=$DISPLAY" --env="LC_ALL=C.UTF-8" --env="LANG=C.UTF-8" --name fullrpc debian:bullseye
```  
```  
xhost +
```  
```  
docker exec -ti fullrpc /bin/bash
```  
```  
apt update
```  
```  
apt install build-essential
```  
```  
apt install libc6-dev
```  
```  
apt install libc-dev-bin
```  
```  
apt install manpages-dev
```  
```  
apt install git zip gcc zsh
```  
```  
apt install nano gedit mousepad
```  
```  
apt install rpcbind
```
```  
apt install zip
```  
```  
apt install git
```  
```  
apt install nano mousepad
```  
```  
apt install make 
```  

# EXERCICE 1 : SOCKET
```  
mkdir SOCKET
```  
```  
cd SOCKET/
```  
```  
git clone https://github.com/ImsicatcherBastienbaranoff/tpsocket
```  
```  
cd tpsocket
```  
```  
unzip client-server.zip
```  
```  
gcc -o tcpclient tcpclient.c
```  
```  
chmod +x tcpclient
```  
```  
gcc -o tcpserver tcpserver.c
```  
```  
chmod +x tcpserver
```  
```  
exit
```  
```  
sudo docker exec -ti fullrpc SOCKET/tpsocket/tcpserver
```  
```  
sudo docker exec -ti fullrpc SOCKET/tpsocket/tcpclient
```  
Dans l’autre terminal :  </br>
Tapez hey :  </br>
Dans l’autre terminal : </br>
Tapez : ok </br>
Dans l’autre terminal : </br>
Quittez </br>
```
exit
```

# Exercice 2 :  TP RPC
Installation des dependances  </br>
Essai de RPC pour hello world code predefine : [RPC_Helloworld](https://github.com/riyazathali/RPC-HelloWorld) 
```
sudo docker exec -ti fullrpc bash
```
```
sudo apt install rpcbind
```
```
/etc/init.d/rpcbind start
```
```
git clone https://github.com/riyazathali/RPC-HelloWorld
```
```
cd RPC-HelloWorld/
```
```
rpcgen -a -C hw.x
```
```
make -f Makefile.hw
```
```
chmod +x hw_server
```
```
./hw_server 
```
ctrl + shift+ t
```
sudo docker exec -ti fullrpc bash
```
```
cd RPC-HelloWorld/
```
```
chmod +x hw_client
```
```
./hw_client localhost
```



# Exercice 3 : Entrainnement C, 
3.1 -> Affichage Hello world </br>
3.2 -> Affichage d’un variable ayant comme contenu 10 </br>
3.3 -> Afffichage de texte entrée comme paramètre en ligne de commande </br>
3.4 -> Affichage de texte avec plusieurs arguments en ligne de commande </br>
3.5 -> Déclaration d’un variable, saisie d’un nombre et affichage de ce nombre </br>
3.6 -> Creation de fonction somme (entier) </br>
3.7 -> Creation d’une fonction somme avec verification overflow </br>
3.8 -> Creation de fonction somme de deux structures points en utilisant une passage par copie </br>
3.9 -> passage par pointeur de la function somme </br>
3.10 ->  Création d’une de la function somme C en utilisant une passage par pointeur </br>

# Reponse 3.1
3.1 -> Affichage Hello world
INSTALLER : apt install mousepad
```
sudo docker exec -ti fullrpc bash
```
```
mkdir TPC
```
```
cd TPC/
```
```
nano helloworld.c
```
Copier le code suivant puis tapez ctrl+x et Y et enter pour enregistrer
```
#include <stdio.h>
#include <stdlib.h>

void main(){
	printf("hello world\n");
}
```
```
gcc -c helloworld.c
```
```
gcc -o helloworld helloworld.o
```
```
chmod +x helloworld
```
```
./helloworld
 ```
```
exit
```

# Reponse 3.2 
3.2 -> Affichage d’un variable ayant comme contenu 10
```
sudo docker exec -ti fullrpc bash
```
```
nano affichageVar.c
```
Copier le code suivant puis tapez ctrl+x et Y et enter pour enregistrer
```
#include <stdio.h> 
#include <stdlib.h> 

void main(){
	int var = 10;
	printf("le variable est donc %d \n", var);
}
```
```
gcc -c affichageVar.c
```
```
gcc -o affichageVar affichageVar.o
```
```
chmod +x affichageVar
```
```
./affichageVar
```
```
exit
```

# Reponse 3.3
3.3 -> Afffichage de texte entrée comme paramètre en ligne de commande </br>
La declaration de main deviant c.f [argc](https://stackoverflow.com/questions/3024197/what-does-int-argc-char-argv-mean) :  </br>
int main (int argc, char *argv[]); //first declaration </br>
int main (int argc, char **argv);  //RE-DECLARATION. Equivalent to the above declaration </br>
```
sudo docker exec -ti fullrpc bash
```
```
nano affichage.c
```
Copier le code suivant puis tapez ctrl+x et Y et enter pour enregistrer
```
#include <stdio.h>
#include <stdlib.h>
int main (int argc, char *argv[]){
	if(argc == 1){
		printf("pas de paramètre\n");
        }
	else if(argc == 2){
		printf("le paramètre est %s \n", argv[1]);
	} else {
		printf("le nombre de paramètre est invalide \n");	
	}
}
```
```
gcc -c affichage.c 
```
```
gcc -o affichage affichage.o 
```
```
chmod +x affichage
```
Test après : 
```
./affichage
```
```
./affichage test
```
```
./affichage "test is ok"
```
```
./affichage test is ok
```
```
exit
```
 

# Reponse 3.4
3.4 -> Affichage de texte avec plusieurs arguments en ligne de commande
```
sudo docker exec -ti fullrpc bash
```
```
nano affichageMultiple.c
```
Copier le code suivant puis tapez ctrl+x et Y et enter pour enregistrer
```
#include <stdio.h>
#include <stdlib.h>
int main (int argc, char *argv[]){
	int i = 0;
	if(argc == 1){
		printf("pas de paramè?tre\n");
        }
	else if(argc >= 2){
		for(i = 1; i < argc ; i++){
			printf("le paramè?tre numero %d est %s \n", i, argv[i]);
		}
	} else {
		printf("le nombre de paramè?tre est invalide \n");	
	}
}
```
```
gcc -c affichageMultiple.c
```
```
gcc -o affichageMultiple affichageMultiple.o
```
```
chmod +x affichageMultiple
```
```
./affichageMultiple
```
``` 
./affichageMultiple test
```
``` 
./affichageMultiple "test is ok"
```
``` 
./affichageMultiple test is ok
```
```
exit
```


# Reponse 3.5
3.5 -> Déclaration d’un variable, saisie d’un nombre et affichage de ce nombre
```
sudo docker exec -ti fullrpc bash
```
```
nano saisie.c
```
Copier le code suivant puis tapez ctrl+x et Y et enter pour enregistrer
```
#include <stdio.h>
#include <stdlib.h>
void main(){
	int var = 0;
	printf("veuillez entrer un nombre entier\n");
	scanf("%d", &var);
	printf("vous avez entré? le nombre : %d \n", var);
}
```
```
gcc -c saisie.c 
```
```
gcc -o saisie saisie.o 
```
```
chmod +x saisie
```
```
./saisie
```
```
exit
```

# Reponse 3.6
3.6 -> Creation de fonction somme (entier)
```
sudo docker exec -ti fullrpc bash
```
```
nano fonc_somme.c
```
Copier le code suivant puis tapez ctrl+x et Y et enter pour enregistrer
```
#include <stdio.h>
#include <stdlib.h>

int somme(int nb1, int nb2){
	return nb1 + nb2;
}

void main(){
	int nombre1;
	int nombre2;
	int resultat; 

	printf("Entrer un nombre\n");
	scanf("%d", &nombre1);

	printf("Entrer un autre nombre\n");
	scanf("%d", &nombre2);
	
	resultat = somme(nombre1, nombre2);
	printf("la somme de %d et de %d est donc : %d\n", nombre1, nombre2, resultat);
}
```
```
gcc -c fonc_somme.c 
```
```
gcc -o fonc_somme fonc_somme.o 
```
```
chmod +x fonc_somme
```
```
./fonc_somme
```
```
exit
```

# Reponse 3.7
3.7 -> Creation d’une fonction somme avec verification overflow
```
sudo docker exec -ti fullrpc bash
```
```
nano overf_somme.c 
```
Copier le code suivant puis tapez ctrl+x et Y et enter pour enregistrer
```
#include <stdio.h>
#include <stdlib.h>

typedef struct result{
	unsigned int resultat;
	unsigned int errno;
}result;
result somme(unsigned int nb1, unsigned int nb2){
	result rr;
	rr.resultat = nb1 + nb2;
	//obtenir maximal 
	unsigned int max = nb1;
	if(nb2 > max){
		max = nb2;
	}
	if(rr.resultat > max){
		rr.errno = 0;
	}else {
		rr.errno = 1;
	}
	return rr;
}

void main(){
	unsigned int nombre1;
	unsigned int nombre2;
	result r; 
	printf("Entrer un nombre\n");
	scanf("%u", &nombre1);

	printf("Entrer un autre nombre\n");
	scanf("%u", &nombre2);

	r = somme(nombre1, nombre2);
	if (r.errno ==0){
		printf("la somme de %d et de %d est donc : %d\n", nombre1, nombre2, r.resultat);
	} else{
		printf("erreur de la somme\n");
	}
}
```
```
gcc -c overf_somme.c 
```
```
gcc -o overf_somme overf_somme.o 
```
```
chmod +x overf_somme
```
```
./overf_somme 
```
Le nombre maximal unsigned int est : 4294967295 </br>
Note bonus pour la verification overf_somme en utilisant int et non unsigned int ? </br>
```
exit
```



# Reponse 3.8 :
cf.  [video_indication](https://www.youtube.com/watch?v=cByXgJXaTB4) </br>
3.8 -> Creation d’une structure pour faire une function somme avec verification de overflow
```
sudo docker exec -ti fullrpc bash
```
```
nano somme_struct.c
```
Copier le code suivant puis tapez ctrl+x et Y et enter pour enregistrer
```
#include <stdio.h>
#include <stdlib.h>

typedef struct result{
	unsigned int resultat;
	unsigned int errno; //la fonction somme retourne -1 comme errno si c'est faux, retourne 1 sinon 
}result;

typedef struct entree{
	unsigned int nombre1;
	unsigned int nombre2;

}entree;

// une addition possè?de un overflow quand la somme des deux nombre est infè?rieure au maximal des deux nombres dont la somme est à faire 
result fonc_somme(entree e){
	result r;
	r.resultat  = e.nombre1 + e.nombre2;
	//obtenir maximal entre e.nombre1 et e.nombre2
	unsigned int max = e.nombre1;
	if(e.nombre2 > e.nombre1){
		max = e.nombre1;
	}
	
	if(r.resultat > max){
		r.errno = 0;
	}else{
		r.errno = 1;
	}
	return r;
}
void main(){
	unsigned int nb1;
	unsigned int nb2;
	printf("veuillez entrer un nombre \n");
	scanf("%u", &nb1);
	printf("veuillez entrer un autre nombre \n");
	scanf("%u", &nb2);
	
	entree t;
	t.nombre1 = nb1;
	t.nombre2 = nb2;
	result rr = fonc_somme(t);
	if( rr.errno ==  0){
		printf("la somme de %u et de %u donne %u\n", t.nombre1, t.nombre2, rr.resultat);
	}else{
		printf("erreur de la somme\n");
	}

}
```
```
gcc -c somme_struct.c 
```
```
gcc -o somme_struct somme_struct.o 
```
```
chmod +x somme_struct
```
```
./somme_struct
```
Le nombre maximal unsigned int est : 4294967295 </br> 
Note BONUS : Pour un code en C, non signé avec verification overflow ?
```
exit
```

# Reponse 3.9 
3.9 -> passage par pointeur de la function somme
```
sudo docker exec -ti fullrpc bash
```
```
nano pointeur_somme.c 
```
Copier le code suivant puis tapez ctrl+x et Y et enter pour enregistrer
```
#include <stdio.h>
#include <stdlib.h>

void somme(int *result, int nb1, int nb2){
	(*result) =  nb1 + nb2;
}

void main(){
	int nombre1;
	int nombre2;
	int resultat = -1; 

	printf("Entrer un nombre\n");
	scanf("%d", &nombre1);

	printf("Entrer un autre nombre\n");
	scanf("%d", &nombre2);
	
	somme(&resultat, nombre1, nombre2);
	printf("la somme de %d et de %d est donc : %d\n", nombre1, nombre2, resultat);
}
```
```
gcc -c pointeur_somme.c 
```
```
gcc -o pointeur_somme pointeur_somme.o 
```
```
chmod +x pointeur_somme
```
```
./pointeur_somme
```
```
exit
```


# Reponse 3.10 :
3.10 ->  Création d’une de la function somme C en utilisant une passage par pointeur 
```
sudo docker exec -ti fullrpc bash
```
```
nano somme_struct_pointeur.c 
```
Copier le code suivant puis tapez ctrl+x et Y et enter pour enregistrer
```
#include <stdio.h>
#include <stdlib.h>

typedef struct info{
	unsigned int nombre1;
	unsigned int nombre2;
	unsigned int resultat;
	unsigned int errno; //la fonction somme retourne -1 comme errno si c'est faux, retourne 1 sinon 
}info;


// une addition possè?de un overflow quand la somme des deux nombre est infè?rieure au maximal des deux nombres dont la somme est à? faire 
void fonc_somme(info *i){
	i->resultat  = i->nombre1 + i->nombre2;
	//obtenir maximal entre i->nombre1 et i->nombre2
	unsigned int max = i->nombre1;
	if(i->nombre2 > i->nombre1){
		max = i->nombre1;
	}
	
	if(i->resultat > max){
		i->errno = 0;
	}else{
		i->errno = 1;
	}
}
void main(){
	unsigned int nb1;
	unsigned int nb2;
	printf("veuillez entrer un nombre \n");
	scanf("%u", &nb1);
	printf("veuillez entrer un autre nombre \n");
	scanf("%u", &nb2);
	
	info data;
	data.nombre1 = nb1;
	data.nombre2 = nb2;
	fonc_somme(&data);
	if(data.errno ==  0){
		printf("la somme de %u et de %u donne %u\n", data.nombre1, data.nombre2, data.resultat);
	}else{
		printf("erreur de la somme\n");
	}

}
```
```
gcc -c somme_struct_pointeur.c 
```
```
gcc -c somme_struct_pointeur.c 
```
```
gcc -o somme_struct_pointeur somme_struct_pointeur.o 
```
```
chmod +x somme_struct_pointeur
```
```
./somme_struct
```
Le nombre maximal unsigned int est : 4294967295 </br>
```
exit 
```

# Exercice 4.1 : RPC calcul
TP RPC cf.  lecons 
```
sudo docker exec -ti fullrpc bash
```
```
mkdir RPC
```
```
cd RPC/
```
```
ls
```
```
mkdir somme
```
```
cd somme/
```
```
nano calcul.x
```
Copier la configuration IDL suivant puis tapez ctrl+x et Y et enter pour enregistrer
```
struct data {
  unsigned int arg1;
  unsigned int arg2;
};

typedef struct data data;

struct reponse {
  unsigned int somme;
  int errno;
};

typedef struct reponse reponse;

program CALCUL{
  version VERSION_UN{
    void CALCUL_NULL(void) = 0;
    reponse CALCUL_ADDITION(data) = 1;
  } = 1;
} = 0x20000001;
```
```
rpcgen -a calcul.x
```
```
ls
```
rpcgen a généré des code c et Makefile pour nous
```
gcc -c calcul_xdr.c
```
```
gcc -c calcul_clnt.c
```
```
gcc -c calcul_svc.c
```
En regardant dans le fichier  : 
```
nano calcul_server.c
```
Il faut modifier le code en implementant l’addition à faire au niveau de serveur en particulier dans la function calcul_addition_1_svc
``` 
#include "calcul.h"

void * 
calcul_null_1_svc(void *argp, struct svc_req *rqstp)
{
  static char* result;
  /* Ne rien faire */
  return((void*) &result);
}

reponse * 
calcul_addition_1_svc(data *argp, struct svc_req *rqstp)
{
  static reponse  result;
  unsigned int max;

  result.errno = 0; /* Pas d'erreur */

  /* Prend le max */
  max = argp->arg1 > argp->arg2 ? argp->arg1 : argp->arg2;

  /* On additionne */
  result.somme = argp->arg1 + argp->arg2; 

  /* Overflow ? */
  if ( result.somme < max ) {
    result.errno = 1;
  }
    
  return(&result);
}
```
```
gcc -c calcul_server.c
```
```
gcc -o server calcul_svc.o calcul_server.o calcul_xdr.o
```
```
chmod +x server
```
```
./server &
``` 
ctrl +shift + t
```
sudo docker exec -ti fullrpc bash
```
```
rpcinfo -p
```
```
cd RPC/somme
```
```
mkdir client
```
```
cp calcul.x client/
```
```
cd client
```
```
rpcgen -a calcul.x 
```
```
ls
```
```
gcc -c calcul_xdr.c
```
```
gcc -c calcul_clnt.c
```
```
gcc -c calcul_svc.c
```
Regardons d’abord le code calcul_client.c par : 
```
nano calcul_client.c
```
Changeons par le code adequate en particulier dans la fonction main tout en créant la function test_addition. </br>
Aprés modification, le code sera : (le mieux est d'effacer la fonction main est recopier le code) </br>
```
#include <limits.h>
#include "calcul.h"

CLIENT *clnt;

void
test_addition (uint param1, uint param2)
{	
  reponse  *resultat;
  data  parametre;

  /* 1. Preparer les arguments */
  
  parametre.arg1 = param1;
  parametre.arg2 = param2; 
  printf("Appel de la fonction CALCUL_ADDITION avec les parametres: %u et %u \n", parametre.arg1,parametre.arg2);

  /* 2. Appel de la fonction distante */
  
  resultat = calcul_addition_1 (&parametre, clnt);
  if (resultat == (reponse *) NULL) {
    clnt_perror (clnt, "call failed");
    clnt_destroy (clnt);
    exit(EXIT_FAILURE);
  }
  else if ( resultat->errno == 0 ) {
    printf("Le resultat de l'addition est: %u \n\n",resultat->somme);
  } else {
    printf("La fonction distante ne peut faire l'addition a cause d'un overflow \n\n");
  }
  
}

int
main (int argc, char *argv[])
{
  char *host;
  
  if (argc < 2) {
    printf ("usage: %s server_host\n", argv[0]);
    exit (1);
  }
  host = argv[1];
  
  clnt = clnt_create (host, CALCUL, VERSION_UN, "udp");
  if (clnt == NULL) {
    clnt_pcreateerror (host);
    exit (1);
  }
  
  test_addition ( UINT_MAX - 15, 10 );
  test_addition ( UINT_MAX, 10 );
  
  clnt_destroy (clnt);
  exit(EXIT_SUCCESS);
}
```
```
gcc -c calcul_client.c
```
```
gcc -o client calcul_client.o calcul_clnt.o calcul_xdr.o
```
```
chmod +x client
```
```
./client localhost
```
```
exit
```
# Exercice 4.2 : 
Ecrire le code en C pour faire  une Valeure absolue distante
```
sudo docker exec -ti fullrpc bash
```
```
cd RPC
```
```
mkdir valeurabsolue
```
```
cd valeurabsolue
```
```
nano va.x
``` 
Copier et enregistrer la configuration
``` 
struct data {
	int entree;
};

typedef struct data data;

struct reponse {
	int sortie;
};

typedef struct reponse reponse;

program VA{
  version VERSION_UN{
    void VA_NULL(void) = 0;
    reponse VA_abs(data) = 1;
  } = 1;
} = 0x20000001;
```
```
rpcgen -a va.x
```
```
gcc -c va_xdr.c
```
```
gcc -c va_clnt.c
```
```
gcc -c va_svc.c
```
```
nano va_server.c
```
Verifions d’abord le code par défaut </br>
Modifions le code de la function abs </br>
```
nano va_server.c
```
Copier puis enregistrer le code
``` 
/*
 * This is sample code generated by rpcgen.
 * These are only templates and you can use them
 * as a guideline for developing your own functions.
 */

#include "va.h"

void *
va_null_1_svc(void *argp, struct svc_req *rqstp)
{
	static char * result;

	/*
	 * insert server code here
	 */

	return (void *) &result;
}

reponse *
va_abs_1_svc(data *argp, struct svc_req *rqstp)
{
	static reponse  result;

	/*
	 * insert server code here
	 */
	if(argp->entree >= 0)
		result.sortie = argp->entree;
	else{
		result.sortie = -argp->entree;
	}

	return &result;
}
```
```
gcc -c va_server.c
```
```
gcc -o server va_svc.o va_server.o va_xdr.o
```
```
chmod +x server
```
```
./server &
```
Tapez ctrl+shit+T
``` 
sudo docker exec -ti fullrpc bash
```
```
rpcinfo
```
```
cd RPC/valeurabsolue 
```
```
mkdir client
```
```
cp va.x client/
```
```
cd client
```
```
rpcgen -a va.x
```
```
ls
```
```
gcc -c va_xdr.c
```
```
gcc -c va_clnt.c
```
```
gcc -c va_svc.c
```
Le code initial dans va_client est: </br>
Modifions le code dans le main pour faire l’appel de Valeur absolue </br>
```
nano va_client.c
```
```
/*
 * This is sample code generated by rpcgen.
 * These are only templates and you can use them
 * as a guideline for developing your own functions.
 */
#include <limits.h>
#include "va.h"

CLIENT *clnt;

void test_va(int nombre){
	reponse  *resultat;
 	data  parametre;
	
	parametre.entree = nombre;
	resultat = va_abs_1 (&parametre, clnt);
	if (resultat == (reponse *) NULL) {
    		clnt_perror (clnt, "call failed");
    		clnt_destroy (clnt);
    		exit(EXIT_FAILURE);
  	}
  	else {
  	  printf("la valeur de valeur %d est %d \n", parametre.entree, resultat->sortie);
  	} 



}
int
main (int argc, char *argv[])
{
	char *host;

	if (argc < 2) {
		printf ("usage: %s server_host\n", argv[0]);
		exit (1);
	}
	host = argv[1];
	/*adding code valeur absolue*/
	  clnt = clnt_create (host, VA, VERSION_UN, "udp");
	  if (clnt == NULL) {
    		clnt_pcreateerror (host);
   		  exit (1);
  	}
  	test_va ( -15);
  	test_va ( 15 );
  	clnt_destroy (clnt);	
exit (0);
}
```
```
gcc -c va_client.c
```
```
gcc -o client va_client.o va_clnt.o va_xdr.o
```
```
chmod +x client
```
```
./client localhost
```
```
exit
```

# EXERCICE 4.3
Faire un code C RPC permettant de factoriser un nombre en produit de deux nombres premiers 
```
sudo docker exec -ti fullrpc bash
```
```
cd RPC
```
```
mkdir factorisation
```
```
cd factorisation
```
```
nano factorisation.x
```
Copier et enregister la configuration
```
struct data {
	int n;
};

typedef struct data data;

struct reponse {
	int p;
	int q;
	int errno;
};

typedef struct reponse reponse;

program FACTORISATION{
  version VERSION_UN{
    void FACTORISATION_NULL(void) = 0;
    reponse FACTORISATION_UN(data) = 1;
  } = 1;
} = 0x20000001;
```
```
rpcgen -a factorisation.x
```
```
gcc -c factorisation_xdr.c
```
```
gcc -c factorisation_clnt.c
```
```
gcc -c factorisation_svc.c
```
Verifions d’abord le code par défaut </br>
Modifions le code de la function factorisation </br>
```
nano factorisation_server.c
```
Copier et enregister le code
```
/*
 * This is sample code generated by rpcgen.
 * These are only templates and you can use them
 * as a guideline for developing your own functions.
 */

#include "factorisation.h"

void *
factorisation_null_1_svc(void *argp, struct svc_req *rqstp)
{
	static char * result;

	/*
	 * insert server code here
	 */

	return (void *) &result;
}

/* 
fonction pour verifier si nombre premier
*/
int est_premier(int nbr){
    int i = 0;
    if(nbr == 2){
        return 1;
    }
    for(i=2; i < nbr-1; i++){
        if(nbr%2 == 0){
            return 0;
        }
    }
    return 1;
}


reponse *
factorisation_un_1_svc(data *argp, struct svc_req *rqstp)
{
	static reponse  result;

	result.p = -1;
	result.q = -1;
	result.errno = 1;
	int i = 0;
	for(i = 2; i< argp->n; i++){
		if(argp->n%i ==0){
			int p = i;
			int q = (argp->n)/i;
			if((p*q == argp->n)&&(est_premier(p))&&(est_premier(q))){
				result.p = p;
				result.q = q;
				result.errno = 0;
								
			}

		}
	}


	return &result;
}
```
```
gcc -c factorisation_server.c
```
```
gcc -o server factorisation_svc.o factorisation_server.o factorisation_xdr.o
```
```
chmod +x server
```
```
./server &
```
ctrl + shift + t
```
sudo docker exec -ti fullrpc bash
```
```
rpcinfo
```
```
cd RPC/factorisation 
```
```
mkdir client
```
```
cp factorisation.x client/
```
```
cd client
```
```
rpcgen -a factorisation.x
```
```
ls
```
```
gcc -c factorisation_xdr.c
```
```
gcc -c factorisation_clnt.c
```
```
gcc -c factorisation_svc.c
```
Le code initial dans factorisation_client est: </br>
Modifions le code dans le main pour faire l’appel de la function factorisation </br>
```
nano factorisation_client.c
```
Copier et enregistrer le code
```
/*
 * This is sample code generated by rpcgen.
 * These are only templates and you can use them
 * as a guideline for developing your own functions.
 */

#include "factorisation.h"

CLIENT *clnt;


void test_factorisation(int nombre){
	reponse  *resultat;
 	data  parametre;
	
	parametre.n = nombre;
	resultat = factorisation_un_1 (&parametre, clnt);
	if (resultat == (reponse *) NULL) {
    		clnt_perror (clnt, "call failed");
    		clnt_destroy (clnt);
    		exit(EXIT_FAILURE);
  	}
  	else {
	  if(resultat->errno != 1){
	  	  printf("Donc %d = %d * %d \n", parametre.n, resultat->p, resultat->q);
  
           }else{
		printf("Erreur de factorisation\n");

	  }

  	} 
}


int
main (int argc, char *argv[])
{
	char *host;

	if (argc < 2) {
		printf ("usage: %s server_host\n", argv[0]);
		exit (1);
	}
	host = argv[1];
	  clnt = clnt_create (host, FACTORISATION, VERSION_UN, "udp");
	  if (clnt == NULL) {
    		clnt_pcreateerror (host); 
   		  exit (1); 
  	} 
  	test_factorisation (77); 
  	test_factorisation ( 21 );
 	test_factorisation ( 12 );
 
  	clnt_destroy (clnt);	


exit (0);
}
```
```
gcc -c factorisation_client.c
```
```
gcc -o client factorisation_client.o factorisation_clnt.o factorisation_xdr.o
```
```
chmod +x client
```
```
./client localhost
```
```
exit
```
# EXERCICE 5 : 
Vérifier vraiment que vous utilisez une tabulation et non
# Reponse 5.1 : Makefile type 1
```
sudo docker exec -ti fullrpc bash
```
```
mkdir TP_MAKEFILE
```
```
cd TP_MAKEFILE
```
```
mkdir TP_MAKEFILE1
```
```
git clone https://github.com/SitrakaResearchAndPOC/FullRPC_LXD 
```
```
mv FullRPC_LXD/*.c TP_MAKEFILE1
```
```
mv FullRPC_LXD/*.h TP_MAKEFILE1
```
```
rm -rf FullRPC_LXD
```
```
cd TP_MAKEFILE1
```
```
nano Makefile
```
Copier et Enregistrer
```
all: exec

main.o: main.c tri.h
        gcc -c main.c -o main.o

fonction_tri.o: fonction_tri.c tri.h
                gcc -c fonction_tri.c -o fonction_tri.o

fonction_tableau.o: fonction_tableau.c tri.h
                        gcc -c fonction_tableau.c -o fonction_tableau.o

exec: fonction_tableau.o fonction_tri.o main.o
        gcc fonction_tableau.o fonction_tri.o main.o -o exec

clean:
        rm -rf *.o
        rm -rf exec
```
```
make all
```
```
chmod +x exec 
```
```
./exec 
```
```
make clean
```
```
cd ..
```
```
exit
```


# Reponse 5.2 : TP_MAKEFILE2
```
sudo docker exec -ti fullrpc bash
```
```
cd TP_MAKEFILE
```
```
mkdir TP_MAKEFILE2
```
```
git clone https://github.com/SitrakaResearchAndPOC/FullRPC_LXD 
```
```
mv FullRPC_LXD/*.c TP_MAKEFILE2
```
```
mv FullRPC_LXD/*.h TP_MAKEFILE2
```
```
rm -rf FullRPC_LXD
```
```
cd TP_MAKEFILE2
```
```
nano Makefile
```
Copier et Enregistrer
```
all: exec

main.o: main.c tri.h
         gcc -c $< -o $@

fonction_tri.o: fonction_tri.c tri.h
         gcc -c $< -o $@

fonction_tableau.o: fonction_tableau.c tri.h
         gcc -c $< -o $@

exec: fonction_tableau.o fonction_tri.o main.o
        gcc $^ -o $@

clean:
        rm -rf *.o
        rm -rf exec
```
```
make all
```
```
chmod +x  exec
```
```
./exec 
```
```
make clean
```
```
cd ..
```
```
exit
```

# reponse 5.3 : TP_MAKEFILE3
```
sudo docker exec -ti fullrpc bash
```
```
cd TP_MAKEFILE
```
```
mkdir TP_MAKEFILE3
```
```
git clone https://github.com/SitrakaResearchAndPOC/FullRPC_LXD
```
```
mv FullRPC_LXD/*.c TP_MAKEFILE3
```
```
mv FullRPC_LXD/*.h TP_MAKEFILE3
```
```
rm -rf FullRPC_LXD
```
```
cd TP_MAKEFILE3
```
```
nano Makefile
```
Copier et Enregistrer
```
CC=gcc
SRC=$(wildcard *.c)
OBJ=$(SRC:.c=.o)
all: exec

main.o: main.c tri.h
         $(CC) -c $< -o $@

fonction_tri.o: fonction_tri.c tri.h
         $(CC) -c $< -o $@

fonction_tableau.o: fonction_tableau.c tri.h
         $(CC) -c $< -o $@

exec: $(OBJ)
        $(CC) $^ -o $@

clean:
        rm -rf *.o
        rm -rf exec
```
```
make all
```
```
chmod +x exec 
```
```
./exec 
```
```
make clean
```
```
cd ..
```
```
exit
```

# reponse 5.4 : TP_MAKEFILE4
```
sudo docker exec -ti fullrpc bash
```
```
cd TP_MAKEFILE
```
```
mkdir TP_MAKEFILE4
```
```
git clone https://github.com/SitrakaResearchAndPOC/FullRPC_LXD 
```
```
mv FullRPC_LXD/*.c TP_MAKEFILE4
```
```
mv FullRPC_LXD/*.h TP_MAKEFILE4
```
```
rm -rf FullRPC_LXD
```
```
cd TP_MAKEFILE4
```
```
nano Makefile
```
Copier et Enregistrer
```
CC=gcc
SRC=$(wildcard *.c)
OBJ=$(SRC:.c=.o)
all: exec

%.o: %.c tri.h
        $(CC) -c $< -o $@

exec: $(OBJ)
        $(CC) $^ -o $@

clean:
        rm -rf *.o
        rm -rf exec
```
```
make all
```
```
chmod +x exec
```
```
./exec 
```
```
make clean
```
```
cd ..
```
```
exit
```
# exercice 5.5 : à faire
* [Makefile](https://www.cs.colby.edu/maxwell/courses/tutorials/maketutor/)
* [Makefile_pdf](https://github.com/SitrakaResearchAndPOC/FullRPC_LXD/blob/main/A%20Simple%20Makefile%20Tutorial.pdf)


# SAVE THE FILE SYSTEM 
```
docker ps 
```
finding <id> of fullrpc
```
docker commit <id> fullrpc
```
```
docker save fullrpc > fullrpc.tar.gz
```

# LOAD AND RUN
```
docker load < fullrpc.tar.gz
```
```  
docker run -tid --privileged -v /dev/bus/usb:/dev/bus/usb -v /tmp/.X11-unix:/tmp/.X11-unix:ro -v $XAUTHORITY:/home/user/.Xauthority:ro --net=host --env="DISPLAY=$DISPLAY" --env="LC_ALL=C.UTF-8" --env="LANG=C.UTF-8" --name fullrpc debian:bullseye
```  
```  
xhost +
```  
```  
docker exec -ti fullrpc /bin/bash
```  

