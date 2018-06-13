import random

separator = '-' * 20
spaces = [None] * 100
c_l_spaces = {r'slid down a snakes ': [[14, 3], [20, 15], [39, 33], [66, 53], [69, 58], [79, 67], [84, 71], [88, 36]],
              'climbed up a ladder |=|': [[6, 17], [24, 26], [30, 44], [49, 62], [82, 86]]}
print("Do you want to begin?")
print("Type YES or NO")
a = input()
if a == 'YES':
    print('Okay! Beginning your game...')
    print(' ')
elif a == 'NO':
    print('Okay,Come back later')
if a == 'YES':
    print('In your bedroom you see a light behind your closet.')
    print('You then peak in the closet and you get sucked into ')
    print('a dark and scary forest. The door closes behind you ')
    print('and automatically locks you in. You are now trapped! ')
    print('In order to escape you have to travel fifty blocks but ')
    print('beware of all the obstacles that you may encounter. ')
    print('First to escape from the forest leads them back to ')
    print('their house.')
    print("Type START to start")
    b = input()


class Player:

    def __init__(self, number):
        self.number = number
        self.space = 0

    def move(self, roll):
        global spaces
        if (self.space + roll) > 90:
            return (1, 'Your roll would move you off the game board.You remain at space {0}.'.format(self.space))
        elif (self.space + roll) == 90:
            return (0, 'You moved to the last space. You won the game!')
        else:
            self.space += roll
            try:
                space_type = spaces[self.space - 1][0]
                self.space = spaces[self.space - 1][1]
            except TypeError:
                return (1, 'You moved to space {0}.'.format(self.space))
            else:
                return (1, 'You {0} to space {1}!'.format(space_type, self.space))


def roll_die():
    roll = random.randint(1, 6)
    print('You rolled {0}.'.format(roll))
    return roll


def populate_game_board():
    global spaces
    for key, values in c_l_spaces.items():
        for space in values:
            spaces[space[0] - 1] = [key, space[1]]


def initialize_players():
    while True:
        try:
            num_players = int(input('Enter the number of players (0 to exit): '))
        except ValueError:
            print('You have entered an invalid response.n')
        else:
            if num_players == 0:
                print('You have quit the game.')
                return
            elif 1 <= num_players <= 4:
                break
            elif (num_players < 0) or (num_players > 4):
                print('You have entered an invalid number of players.n')

    players = []
    for num in range(num_players):
        players.append(Player(num + 1))

    return players


def start_game(players):
    game = 1
    while game:
        for player in players:
            print('Player {0}'.format(player.number))
            print('You are currently on space {0}.'.format(player.space))
            import random
            for i in range(1, 10):
                ops = ['+']
            num1 = random.randint(1, 50)
            num2 = random.randint(1, 20)
            operation = random.choice(ops)

            answer = int(input(str(num1) + operation + str(num2) + '='))
            sum = num1 + num2

            if (answer == sum):
                print('Correct ')
                game_update = player.move(roll_die())
                print('You are currently on space {0}.'.format(player.space))
            if (answer != sum):
                print('Incorrect!Stay where you are.')


def initialize_game():
    players = initialize_players()
    if players:
        populate_game_board()
        start_game(players)


if __name__ == '__main__':
    initialize_game()
import random
import operator


def quiz():
    print('Welcome to level 2 of snakes and ladders!')
    print('Congraltions, you have reached the end of the game board.')
    print(' Now in order to finsh off the game, you have to complete')
    print('a math quiz. Once when you answer ten math questions correctly,')
    print('you will be the winner of the game')

    name = input("Please enter your name")
    print("Hello", name, " Let's begin the quiz!")
    score = 0
    for i in range(10):
        correct = askQuestion()
        if correct:
            score += 1
            print('Correct!')
            print
            "Score", (score), "\n"
        else:
            print('Incorrect!')

    print("Congraltions, you have won the game!")
    print(' A bright light now birgtens up a dark pathway.')
    print('the light leads you back to your closet, which then leads')
    print(' you back to your bedroom.')
    print('you are now back your bedroom.')


def askQuestion():
    answer = randomCalc()
    guess = float(input())
    return guess == answer


def randomCalc():
    ops = {'+': operator.add,
           '-': operator.sub,
           '*': operator.mul}
    num1 = random.randint(0, 11)
    num2 = random.randint(1, 11)
    op = random.choice(list(ops.keys()))
    answer = ops.get(op)(num1, num2)
    print('What is {} {} {}?'.format(num1, op, num2))
    return answer


quiz()
# askQuestion()
# randomCalc()
