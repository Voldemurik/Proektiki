# Proektiki
Мои мини-проекты, творческие работы, конспекты и другие продукты интеллектуального и творческого труда.

## Сводка по работе в GitVerse. Конспект на 30 мин
Ссылочка на конспект: [tutorial](https://github.com/Voldemurik/Proektiki/blob/main/%D0%9A%D0%BE%D0%BD%D1%81%D0%BF%D0%B5%D0%BA%D1%82%20GitVerse.md)
По данной сводке можно научиться ориентироваться по довольно обширной инструкции Gitverse и быстро находить уже в самой [документации](https://gitverse.ru/docs/gitverse/basics/quick-start/) нужную информацию.

## Обучение Markdown
Собираюсь научиться читать синтаксис языка разметки Markdown. Всё-таки в эпоху нейросетей это чуть ли не основной язык взаимодействия ИИ с текстом. Бывает, что и мне необходимо работать с ним, например при написании данного текста. Постараюсь научиться делать ссылки, редактировать шрифты, цвета текста и другое.
Обучение буду проходить по документации GitVerse, ИИ и Интернета. Скоро буду выкладывать здесь результаты моей работы. Вероятно, это будут мини-тексты с графиками, таблицами и другой разметкой. 

### Библиотека Pandas: гайд для новичков

**Pandas** — это библиотека Python для работы с табличными данными. С ней удобно загружать, чистить, фильтровать и анализировать данные, почти как в Excel, только с помощью кода.

#### Установка и подключение

pip install pandas

import pandas as pd

#### Основные структуры данных

- **Series** — одномерный массив с подписями (как один столбец таблицы).
- **DataFrame** — двумерная таблица со строками и столбцами (как лист Excel).

#### Загрузка данных

Чаще всего данные читают из CSV-файла (текстовая таблица, где значения разделены запятыми):

df = pd.read_csv("data.csv")

#### Первый взгляд на данные

- `df.head()` — первые 5 строк;
- `df.info()` — типы столбцов и пропуски;
- `df.describe()` — базовая статистика (среднее, минимум, максимум).

#### Выбор и фильтрация

- `df["age"]` — выбрать один столбец;
- `df[df["age"] > 18]` — оставить строки, где возраст больше 18.

#### Работа с пропусками

- `df.dropna()` — удалить строки с пустыми значениями;
- `df.fillna(0)` — заменить пропуски нулями.

#### Группировка

Метод `groupby` объединяет строки по признаку и считает итоги:

df.groupby("city")["salary"].mean()

#### Сохранение результата

df.to_csv("result.csv", index=False)

#### Совет

Начните с небольшого набора данных, например с сайта Kaggle (платформа с открытыми датасетами — готовыми наборами данных), и попробуйте каждую команду из этого гайда.

## Игра Крестики-Нолики на Python

def winning_line(strings):
    strings = set(strings)
    return len(strings) == 1 and ' ' not in strings

def row_winner(board):
    return any(winning_line(row) for row in board)

def column_winner(board):
    return row_winner(zip(*board))

def main_diagonal_winner(board):
    return winning_line(row[i] for i, row in enumerate(board))

def diagonal_winner(board):
    return main_diagonal_winner(board) or main_diagonal_winner(reversed(board))

def winner(board):
    return row_winner(board) or column_winner(board) or diagonal_winner(board)

def format_board(board):
    size = len(board)
    line = f'\n  {"+".join("-" * size)}\n'
    rows = [f'{i + 1} {"|".join(row)}' for i, row in enumerate(board)]
    return f'  {" ".join(str(i + 1) for i in range(size))}\n{line.join(rows)}'

def play_move(board, player):
    print(f'{player} to play:')
    row = int(input()) - 1
    col = int(input()) - 1
    board[row][col] = player
    print(format_board(board))

def make_board(size):
    return [[' '] * size for _ in range(size)]

def print_winner(player):
    print(f'{player} wins!')

def print_draw():
    print("It's a draw!")

def play_game(board_size, player1, player2):
    board = make_board(board_size)
    print(format_board(board))

    player = player1
    for _ in range(board_size * board_size):
        play_move(board, player)
        if winner(board):
            print_winner(player)
            return
        if player == player1:
            player = player2
        else:
            player = player1

    print_draw()

play_game(3, 'X', 'O')
