# Game_using_oops

#CODE IS GIVEN BELOW

from random import randint
from typing import Final
from enum import Enum, auto


class CharacterType(Enum):
    SUPERHERO = auto()
    VILLAIN = auto()


class Character:
    def __init__(self, name: str, attack_power: int, life: int) -> None:
        self.name = name
        self.attack_power = attack_power
        self.life = life

    def __str__(self) -> str:
        return (
            f" Name: {self.name}, Attack Power: {self.attack_power}, life: {self.life}"
        )


class SuperHero(Character):
    def __init__(self, name: str, attack_power: int, life: int) -> None:
        super().__init__(name, attack_power, life)
        self.role = CharacterType.SUPERHERO

    def __str__(self) -> str:
        return (
            f" Superhero => Name: {self.name}, Attack Power: {self.attack_power},"
            f"life: {self.life}"
        )


class Villain(Character):
    def __init__(self, name: str, attack_power: int, life: int) -> None:
        super().__init__(name, attack_power, life)
        self.role = CharacterType.VILLAIN

    def __str__(self) -> str:
        return (
            f" VILLAIN => Name: {self.name}, Attack Power: {self.attack_power},"
            f"life: {self.life}"
        )





class Life:
    hero_life = 0
    villain_life = 0

    @staticmethod
    def inc_hero_life(life: int) -> None:
        Life.hero_life += life

    @staticmethod
    def dec_hero_life(life: int) -> None:
        Life.hero_life -= life

    @staticmethod
    def inc_villain_life(life: int) -> None:
        Life.villain_life += life

    @staticmethod
    def dec_villain_life(life: int) -> None:
        Life.villain_life -= life


def get_all_superheros() -> list[SuperHero]:
    # supwer heroes
    ironman = SuperHero(name="Ironman", attack_power=250, life=1000)
    blackwidow = SuperHero(name="blackwidow", attack_power=180, life=800)
    spiderman = SuperHero(name="spiderman", attack_power=190, life=700)
    hulk = SuperHero(name="Hulk", attack_power=300, life=1100)

    superheros: list[SuperHero] = [ironman, blackwidow, spiderman, hulk]
    return superheros


def get_superhero(index: int) -> SuperHero | None:
    superheros = get_all_superheros()
    if index < len(superheros):
        return superheros[index]
    else:
        return None


def get_all_villains() -> list[Villain]:
    # SUPER VILLAINS
    thanos = Villain(name="thanos", attack_power=250, life=1500)
    redskull = Villain(name="redskull", attack_power=300, life=800)
    proxima = Villain(name="proxima", attack_power=320, life=800)

    villains: list[Villain] = [thanos, redskull, proxima]
    return villains


def get_villain(index: int) -> Villain | None:
    villains = get_all_villains()
    if index < len(villains):
        return villains[index]
    else:
        return None


def attack() -> None:
    for attack_num in range(3):
        hero_index = randint(0, 3)
        villain_index = randint(0, 2)
        current_superhero = get_superhero(hero_index)
        current_villain = get_villain(villain_index)

        if current_superhero and current_villain:
            simulate_attack(attack_num, current_villain, current_superhero)
        else:
            print(f"Error! NO superhero or villains to fight")


def simulate_attack(attack_num: int, villain: Villain, superhero: SuperHero) -> None:
    # hero life
    Life.inc_hero_life(superhero.life)
    Life.inc_villain_life(villain.life)

    print(
        f"Attack : {attack_num + 1} => {superhero.name} is going to fight with : {villain.name}")

    # attack
    Life.dec_hero_life(villain.attack_power)
    Life.dec_villain_life(superhero.attack_power)

    # print a nice separating line
    print("=" * 58)


def win_or_loose() -> None:
    # win or loss
    WIN_MSG: Final[str] = "YOu won!!! . you successful save zortan!!!! ***"
    LOST_MST: Final[str] = "You lost!!. Thanos killed Avengers and captured Zortan!!!"

    if Life.hero_life >= Life.villain_life:
        print("hero life is :", Life.hero_life)
        print("villain life is : ", Life.villain_life)
        print(WIN_MSG)
    else:
        print("hero life is :", Life.hero_life)
        print("villain life is : ", Life.villain_life)
        print(LOST_MST)


def main() -> None:
    attack()
    win_or_loose()


main()
