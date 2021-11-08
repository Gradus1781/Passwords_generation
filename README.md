# Passwords_generation
# -*- coding: utf-8 -*-
from random import choice
from re import sub
from string import digits, ascii_lowercase, ascii_uppercase, punctuation


def answer_to_the_question() -> bool:
    while True:
        answer = input(">>> ").lower()
        if answer == "да":
            return True
        elif answer == "нет":
            return False
        else:
            continue


def check_correct_input(num: str):
    while True:
        if num.isdigit():
            return int(num)
        else:
            print("Введите число: ")


def settings():
    chars = digits + ascii_uppercase + ascii_lowercase + punctuation
    count_of_passwords = check_correct_input(input("Сколько паролей будем генерировать? "))
    lenght_of_single_password = check_correct_input(input("Какой длины будет каждый пароль? "))
    print("Задать стандартную генерацию паролей?(да, нет)")
    if answer_to_the_question():
        return count_of_passwords, lenght_of_single_password, chars
    else:
        # При отрицательных ответах из стека символов будут убираться выбранные
        print("Пароль должен включать цифры?(да, нет)")
        if not answer_to_the_question():
            chars = sub(digits, '', chars)
        print("Пароль должен включать строчные буквы?(да, нет)")
        if not answer_to_the_question():
            chars = sub(ascii_lowercase, '', chars)
        print("Пароль должен включать прописные буквы?(да, нет)")
        if not answer_to_the_question():
            chars = sub(ascii_uppercase, '', chars)
        print(f"Пароль должен включать пунктуационные знаки?({punctuation})(да, нет)")
        if not answer_to_the_question():
            chars = sub(punctuation, '', chars)
        print(f"Исключать неоднозначные символы 'il1Lo0O'?(да, нет)")
        if answer_to_the_question():
            chars = sub(r'[il1Lo0O]', '', chars)
        return count_of_passwords, lenght_of_single_password, chars


def get_passwords() -> list:
    COUNT_OF_PASSWORDS, LENGHT_OF_SINGLE_PASSWORD, CHARS = settings()
    passwords = []
    for _ in range(COUNT_OF_PASSWORDS):  # начинаем генерацию паролей
        item = ""
        for _ in range(LENGHT_OF_SINGLE_PASSWORD):
            item += choice(CHARS)
        passwords.append(item)
    return passwords


def print_passwords(passwords):
    for num, password in enumerate(passwords, start=1):  # красиво выводим все полученные пароли
        print(str(num) + '.', password)


def main():
    passwords = get_passwords()
    print_passwords(passwords)


if __name__ == "__main__":
    main()
