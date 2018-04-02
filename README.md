# Projet_vin


class Statistiques:
    
    """Classe permettant d'effectuer des statistiques descriptives sur tout ou partie d'une base de            
    données"""
    
    
    def __init__(self,donnees,selection,critere):
        
        """Constructeur de la classe :
        donnees est une instance de la classe Bdd
        critere est un ENTIER entre 0 et 13 associé au critère sur lequel on veut effectuer des statistiques
        selection est l'ensemble des indices sélectionnés, chaque indice correspondant à un vin donné
        """
        
        self.d = donnees.data
        self.c = critere
        self.s = selection
        
        
        
        
    def triStat(self):
        
        """Cette fonction trie la sélection par ordre croissant du critère, grâce à un algorithme de tri par
        insertion"""
        
        n = len(self.s)
        
        if n == 0:
            return "La sélection est vide, on ne peut pas faire le tri"
        elif n == 1:
            return self.s
        else:
            t = []
            for i in self.s:
                t.append(self.d[i][self.c])
            for k in range(1,n):
                temp=t[k]
                j=k
                while j>0 and temp<t[j-1]:
                    t[j]=t[j-1]
                    j-=1
                t[j]=temp
            return t
        
        
        
        
    def nbrElements(self):
        
        """Renvoie le nombre d'éléments présents dans la sélection"""
        
        return len(self.s)
        
        
    def afficheNbrElements(self):
        
        """Affiche le nombre d'éléments de la sélection"""
        
        print("Il y a ", self.nbrElements(), "éléments dans la sélection")
        
        
       
        
    def mediane(self):
        
        """Renvoie la médiane du critère de la sélection"""
        
        trie = self.triStat()
        n = len(trie)
        
        if n == 0:
            return "La sélection est vide, la médiane n'existe pas"
        elif n == 1:
            return trie[0]
        elif n%2 == 1:
            return trie[n//2]
        else:
            return (trie[(n//2)-1] + trie[n//2])*0.5
            
            
    def afficheMediane(self):
        
        """Affiche la médiane du critère de la sélection"""
        
        print("La médiane de la sélection pour ce critère : ", self.mediane())
        
        
       
        
    def moyenne(self):
        
        """Renvoie la moyenne du critère de la sélection"""
        
        if self.s == []:
            return "La sélection est vide, le calcul de la moyenne est impossible"
            
        n = len(self.s)
        somme = 0
        
        for i in self.s:
            somme += self.d[i][self.c]
        return somme/n
        
        
    def afficheMoyenne(self):
        
        """Affiche la moyenne du critère de la sélection"""
        
        print("La moyenne de la sélection pour ce critère : ", self.moyenne())
        
        
        
        
    def variance(self):
        
        """Renvoie la variance du critère de la sélection"""
        
        if self.s == []:
            return "La sélection est vide, le calcul de la variance est impossible"
            
        n = len(self.s)
        moy = self.moyenne()
        somme = 0
        
        for i in self.s:
            somme += self.d[i][self.c]**2
        return somme/n - moy**2
        
        
    def afficheVariance(self):
        
        """Affiche la moyenne du critère de la sélection"""
        
        print("La variance de la sélection pour ce critère : ", self.variance())
        
        
            
            
            
    def afficheTout(self):
        
        """Méthode permettant d'afficher les principales statistiques relatives au critère de la
        sélection"""
            
        print("************************************************************") 
        print("Résumé des statistiques relatives au critère de la sélection")
        print("************************************************************") 
        print("                                                            ")
        print("Critère retenu : ", self.c) 
        print("                                                            ") 
        print("Nombre d'éléments sélectionnés : ", self.nbrElements())
        print("Médiane : ", self.mediane())
        print("Moyenne : ", self.moyenne())
        print("Variance : ", self.variance())
        print("Médiane : ", self.mediane())
           
        
