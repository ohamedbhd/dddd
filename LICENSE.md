# World War Game

import random

class Soldier:
    def __init__(self, name, health, attack_power):
        self.name = name
        self.health = health
        self.attack_power = attack_power

    def attack(self, other):
        damage = random.randint(0, self.attack_power)
        other.health -= damage
        return damage

class Army:
    def __init__(self, name):
        self.name = name
        self.soldiers = []

    def add_soldier(self, soldier):
        self.soldiers.append(soldier)

    def is_defeated(self):
        return all(soldier.health <= 0 for soldier in self.soldiers)

def battle(army1, army2):
    while not army1.is_defeated() and not army2.is_defeated():
        for soldier in army1.soldiers:
            if not army2.is_defeated():
                damage = soldier.attack(random.choice(army2.soldiers))
                print(f"{soldier.name} attacks! Deals {damage} damage.")
        
        for soldier in army2.soldiers:
            if not army1.is_defeated():
                damage = soldier.attack(random.choice(army1.soldiers))
                print(f"{soldier.name} attacks! Deals {damage} damage.")

    if army1.is_defeated():
        print(f"{army2.name} wins!")
    else:
        print(f"{army1.name} wins!")

# Example usage
army1 = Army("Red Army")
army1.add_soldier(Soldier("Soldier A", 100, 20))
army1.add_soldier(Soldier("Soldier B", 100, 20))

army2 = Army("Blue Army")
army2.add_soldier(Soldier("Soldier C", 100, 20))
army2.add_soldier(Soldier("Soldier D", 100, 20))

battle(army1, army2)
