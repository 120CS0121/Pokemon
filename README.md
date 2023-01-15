# Pokemon
class Pokemon:
    def __init__(self, name, primary_type, max_hp):  # max health power that it can ever have
        self.name = name
        self.primary_type = primary_type  # water, fire, grass
        self.max_hp = max_hp
        self.hp = max_hp

    def __str__(self):    # to access the string
        return f"{self.name} ({self.primary_type}: {self.hp}/{self.max_hp})"  # returning f string like bulbsaur (grass)


    def feed(self):  # feed them to increase health
        if self.hp < self.max_hp:
            self.hp += 1
            print(f"{self.name} has now {self.hp} HP.")
        else:
            print(f"{self.name} is full.")

    def battle(self, other):
        print("Battle:", self.name, "vs", other.name)
        result = self.typewheel(self.primary_type, other.primary_type)
        if result == "lose":
            self.hp -= 10
            print(f"{self.name} lost and now has {self.hp} HP.")
        print(f"{self.name} fought {other.name} and the result is a {result}")
    @staticmethod # if not it will show an error like, it needs self and all
    def typewheel(type1, type2):   # like what type of things they are
        # making a dictionary
        result_map = {0: "lose", 1: "win", -1: "tie"}
        # The mapping between types and result conditions
        game_map = {"water": 0, "fire": 1, "grass": 2}
        # Win-lose matrix
        rps_table = [
            [-1, 1, 0],  # water
            [0, -1, 1],  # fire
            [1, 0, -1]  # grass
        ]
# water # 1. water vs water => tie = -1 # 2. water vs fire => win = 1
        result = rps_table[game_map[type1]][game_map[type2]]      # using a list lookup to declare a winner
        return result_map[result]


if __name__ == '__main__':
    mahi = Pokemon(name="Mahishasur", primary_type="grass", max_hp=100)
    kamsa = Pokemon(name="Kamsasur", primary_type="fire", max_hp=150)
    ravan = Pokemon(name="Ravanasur", primary_type="fire", max_hp=150)
    mahi.battle(ravan)
