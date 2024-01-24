import random
class Carte:
    def __init__(self, rang, couleur):
        self.rang = rang
        self.couleur = couleur

    def __str__(self):
        return str(self.rang) + " de " + self.couleur


class Joueur:
    def __init__(self, nom, couleur):
        self.nom = nom
        self.couleur = couleur
        self.main = []

    def jouer(self, atout):
        carte = self.main.pop()
        if carte.couleur == atout:
            return carte
        else:
            return random.choice(self.main)


class Equipe:
    def __init__(self, nom, joueurs):
        self.nom = nom
        self.joueurs = joueurs

    def marquer(self, points):
        self.points += points

    def __str__(self):
        return self.nom + " (" + str(self.points) + " points)"


class Partie:
    def __init__(self, joueurs):
        self.joueurs = joueurs
        self.atout = random.randint(1, 4)
        self.tour = 0
        self.scores = [0, 0]

    def distribuer(self):
        for joueur in self.joueurs:
            joueur.main = []
            for i in range(5):
                joueur.main.append(Carte(random.randint(1, 13), random.randint(1, 4)))
            for i in range(4):
                joueur.main.append(Carte(random.randint(1, 13), self.atout))

    def jouer(self):
        self.tour += 1
        joueur = self.joueurs[self.tour % 4]
        carte = joueur.jouer(self.atout)
        self.scores[self.tour % 2] += carte.rang
        for adversaire in self.joueurs:
            if adversaire.main[0].couleur == carte.couleur:
                adversaire.main.pop(0)

    def estTerminee(self):
        return self.scores[0] >= 501 or self.scores[1] >= 501

    def afficher(self):
        print("Scores :")
        for i in range(2):
            print(self.joueurs[i].nom + " : " + str(self.scores[i]))

def main():
    joueurs = [
        Joueur("Jean", 1),
        Joueur("Marie", 2),
        Joueur("Pierre", 3),
        Joueur("Paul", 4),
    ]
    partie = Partie(joueurs)
    partie.distribuer()
    while not partie.estTerminee():
        partie.jouer()
        partie.afficher()
    print("L'équipe gagnante est " + partie.joueurs[partie.scores.index(max(partie.scores))].nom)


if __name__ == "__main__":
    main()
class Carte:
    def __init__(self, rang, couleur):
        self.rang = rang
        self.couleur = couleur

    def __str__(self):
        return str(self.rang) + " de " + self.couleur
class Joueur:
    def __init__(self, nom, couleur):
        self.nom = nom
        self.couleur = couleur
        self.main = []

    def jouer(self, atout):
        carte = self.main.pop()
        if carte.couleur == atout:
            return carte
        else:
