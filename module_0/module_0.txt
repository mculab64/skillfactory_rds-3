import numpy as np

amount_elements = 100  # Кол-во элементов (чисел) по которым будет произведен поиск


def game_core_v3(number):
    """Функция использует бинарный поиск для минимизации количества попыток поиска числа."""
    count = 1
    middle_of_search = int(amount_elements / 2)
    predict = middle_of_search
    while number != predict:
        count += 1
        middle_of_search -= int(middle_of_search / 2)
        if number > predict:
            predict += middle_of_search

        elif number < predict:
            predict -= middle_of_search

    return (count)


def score_game(game_core):
    """Функция запускает игру 1000 раз, чтобы узнать, как быстро игра угадывает число."""
    count_ls = []
    np.random.seed(1)  # фиксируем RANDOM SEED, чтобы ваш эксперимент был воспроизводим!
    random_array = np.random.randint(1, amount_elements + 1, size=(1000))
    for number in random_array:
        count_ls.append(game_core(number))

    score = int(np.mean(count_ls))
    print(f"Ваш алгоритм угадывает число в среднем за {score} попыток")


score_game(game_core_v3)