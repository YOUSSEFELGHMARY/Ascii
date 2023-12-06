import random

def choose_word():
    words = ["python", "programming", "hangman", "computer", "developer", "learning"]
    return random.choice(words).lower()

def display_word(word, guessed_letters):
    display = ""
    for letter in word:
        if letter in guessed_letters:
            display += letter + " "
        else:
            display += "_ "
    return display.strip()

def display_hangman(attempts):
    hangman_parts = [
        "  ------\n  |    |\n  |    O\n  |   /|\\\n  |   / \\",
        "  ------\n  |    |\n  |    O\n  |   /|\\\n  |   /\n",
        "  ------\n  |    |\n  |    O\n  |   /|\\\n  |\n",
        "  ------\n  |    |\n  |    O\n  |   /|\n  |\n",
        "  ------\n  |    |\n  |    O\n  |    |\n  |\n",
        "  ------\n  |    |\n  |    O\n  |\n  |\n",
        "  ------\n  |    |\n  |\n  |\n  |\n",
        "  ------\n  |\n  |\n  |\n  |\n",
        "  ------\n\n\n\n",
        "  \n\n\n\n"
    ]

    print(hangman_parts[attempts])

def hangman():
    target_word = choose_word()
    guessed_letters = set()
    max_attempts = len(display_hangman) - 1  # عدد الأجزاء في الدمية

    print("مرحبًا بك في لعبة تخمين الكلمة!")
    print(display_word(target_word, guessed_letters))

    while max_attempts > 0:
        guess = input("تخمين حرف: ").lower()

        if guess in guessed_letters:
            print("لقد حاولت هذا الحرف من قبل.")
        elif guess in target_word:
            guessed_letters.add(guess)
            print("تخمين صحيح!")
        else:
            max_attempts -= 1
            print(f"تخمين خاطئ. لديك {max_attempts} محاولة متبقية.")
            display_hangman(max_attempts)

        print(display_word(target_word, guessed_letters))

        if "_" not in display_word(target_word, guessed_letters):
            print("تهانينا! لقد فزت. الكلمة هي:", target_word)
            break

    if max_attempts == 0:
        print(f"للأسف، لقد نفذت جميع المحاولات. الكلمة الصحيحة هي: {target_word}")

if __name__ == "__main__":
    hangman()

