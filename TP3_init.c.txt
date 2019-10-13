//
//  TP3_init.c
//  
//
//  Created by Lucas Letocart on 10/10/2017.
//
/* compilation
 gcc -o exe TP3_init.c -I/LOCAL/CPLEX_Studio1251/cplex/include/ilcplex/ -L/LOCAL/CPLEX_Studio1251/cplex/lib/x86-64_sles10_4.1/static_pic/ -lcplex -lm -lpthread
 */

#include <stdio.h>
#include "/LOCAL/CPLEX_Studio1251/cplex/include/ilcplex/cplex.h"
int main()
{
   // declarations
   CPXENVptr env = NULL;        // environnement Cplex
   CPXLPptr lp = NULL;          // PL Cplex
   int    statut = 0;           // statut technique des fonctions

    // ouverture de Cplex
    env = CPXopenCPLEX (&statut);
    
    // creation d'un PL
    lp = CPXcreateprob(env, &statut, "gros_probleme");
    
    // instanciation d'un PL
    statut = CPXreadcopyprob(env, lp, "mon_pb.lp", NULL);
    
    // resolution d'un PL
    statut = CPXprimopt(env, lp);
    
    // sauvegarde de la solution dans un fichier
    statut = CPXsolwrite(env, lp, "resolution.txt");
    
    // liberation de l'espace memoire
    statut = CPXfreeprob (env, &lp);
    statut = CPXcloseCPLEX (&env);
    
    // on s'en va !
    return 0;
}
