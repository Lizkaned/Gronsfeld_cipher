# Gronsfeld_cipher
ALPHABET: str = 'abcdefghijklmnopqrstuvwxyz'

def normalize_key_length(text: str, key: str):
    result: str = ''
    i: int = 0

    for char in text:
        if ALPHABET.find(char.lower()) != -1:
            result += key[i % len(key)]
            i += 1
        else:
            result += ' '
    return result

def encrypt(text: str, key: str):
    key: str = normalize_key_length(text, key)
    result: str = ''

    for i in range(0, len(text)):
        position_in_alphabet = ALPHABET.find(text[i].lower())
        if position_in_alphabet == -1:
            result += text[i]
            continue

        slide: int = int(key[i])
        position_letter_for_replace = position_in_alphabet + slide
        letter_for_replace: str = ''
        if position_letter_for_replace >= len(ALPHABET):
            letter_for_replace = ALPHABET[position_letter_for_replace -
                                          len(ALPHABET)]
        else:
            letter_for_replace = ALPHABET[position_letter_for_replace]

        if text[i] != text[i].lower():
            letter_for_replace = letter_for_replace.upper()

        result += letter_for_replace

    return result

def decrypt(text: str, key: str):
    key: str = normalize_key_length(text, key)
    result: str = ''

    for i in range(0, len(text)):
        position_in_alphabet = ALPHABET.find(text[i].lower())
        if position_in_alphabet == -1:
            result += text[i]
            continue

        slide: int = int(key[i])
        position_letter_for_replace = position_in_alphabet - slide
        letter_for_replace: str = ''
        if position_letter_for_replace < 0:
            letter_for_replace = ALPHABET[position_letter_for_replace +
                                          len(ALPHABET)]
        else:
            letter_for_replace = ALPHABET[position_letter_for_replace]

        if text[i] != text[i].lower():
            letter_for_replace = letter_for_replace.upper()

        result += letter_for_replace

    return result

text: str = input('Enter text: ')
key = input('Enter key: ')
encrypted: str = encrypt(text, key)
print("Encrypted: ", encrypted)
print("Decrypted: ", decrypt(encrypted, key))
