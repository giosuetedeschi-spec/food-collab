"""
Nome: Tommaso Grippaldi
Corso: BAD
Anno: 2026

Programma gestione biblioteca.
"""

from termcolor import colored


def normalize_input(text):
    """
    Normalizza una stringa: rimuove spazi e mette in maiuscolo
    """
    return text.strip().upper()


def register_book(library):
    """
    Registra un nuovo libro nella biblioteca
    """
    try:
        title = normalize_input(input("Inserisci titolo libro: "))
        qty = int(input("Inserisci quantità: "))

        if qty <= 0:
            raise ValueError("Quantità deve essere maggiore di 0")

        if title in library:
            library[title][0] += qty
            print(colored("Libro già presente, quantità aggiornata.", "yellow"))
        else:
            library[title] = [qty, 0, set()]
            print(colored("Libro aggiunto correttamente.", "green"))

    except ValueError as e:
        print(colored(f"Errore: {e}", "red"))
    finally:
        print(colored("Operazione completata.\n", "cyan"))


def delete_book(library):
    """
    Elimina un libro dalla biblioteca
    """
    title = normalize_input(input("Inserisci titolo da eliminare: "))

    if title not in library:
        print(colored("Libro non trovato!", "red"))
        return

    qty, out, borrows = library[title]

    if out > 0:
        print(colored("Non puoi eliminare: ci sono copie in prestito", "red"))
        return

    print(colored(f"\nTitolo: {title}", "yellow"))
    print(colored(f"Copie totali: {qty}", "yellow"))

    confirm = input("Confermi eliminazione? (s/n): ").lower()

    if confirm == "s":
        del library[title]
        print(colored("Libro eliminato.", "green"))
    else:
        print(colored("Operazione annullata.", "cyan"))


def show_library(library):
    """
    Visualizza tutta la biblioteca
    """
    if not library:
        print(colored("Biblioteca vuota.", "yellow"))
        return

    total_books = 0
    total_out = 0
    users = {}

    for title, data in library.items():
        qty, out, borrows = data

        print(colored(f"\nTitolo: {title}", "blue"))
        print(f"Copie totali: {qty}")
        print(f"Copie in prestito: {out}")
        print(f"Utenti: {', '.join(borrows) if borrows else 'Nessuno'}")

        total_books += 1
        total_out += out

        for user in borrows:
            users[user] = users.get(user, 0) + 1

    print(colored("\n--- RIEPILOGO ---", "magenta"))
    print(f"Numero libri: {total_books}")
    print(f"Copie in prestito: {total_out}")

    print("Utenti:")
    for user, count in users.items():
        print(f"{user}: {count} libri")


def borrow_book(library):
    """
    Gestisce il prestito di un libro
    """
    title = normalize_input(input("Titolo libro: "))
    user = normalize_input(input("Nome utente: "))

    if title not in library:
        print(colored("Libro non esistente!", "red"))
        return

    qty, out, borrows = library[title]

    if out >= qty:
        print(colored("Nessuna copia disponibile!", "red"))
        return

    if user in borrows:
        print(colored("Utente ha già questo libro!", "red"))
        return

    borrows.add(user)
    library[title][1] += 1

    print(colored("Prestito registrato.", "green"))


def return_book(library):
    """
    Gestisce la restituzione di un libro
    """
    title = normalize_input(input("Titolo libro: "))
    user = normalize_input(input("Nome utente: "))

    if title not in library:
        print(colored("Libro non esistente!", "red"))
        return

    qty, out, borrows = library[title]

    if out == 0:
        print(colored("Nessun prestito attivo!", "red"))
        return

    if user not in borrows:
        print(colored("Utente non ha questo libro!", "red"))
        return

    borrows.remove(user)
    library[title][1] -= 1

    print(colored("Restituzione registrata.", "green"))


def menu():
    """
    Menu principale
    """
    print(colored("\n--- MENU BIBLIOTECA ---", "cyan"))
    print("1. Registra libro")
    print("2. Elimina libro")
    print("3. Visualizza biblioteca")
    print("4. Prestito libro")
    print("5. Restituzione libro")
    print("6. Esci")


def main():
    """
    Funzione principale
    """
    library = {}  # dict principale

    while True:
        menu()
        choice = input("Scelta: ")

        if choice == "1":
            register_book(library)
        elif choice == "2":
            delete_book(library)
        elif choice == "3":
            show_library(library)
        elif choice == "4":
            borrow_book(library)
        elif choice == "5":
            return_book(library)
        elif choice == "6":
            print(colored("Uscita dal programma...", "cyan"))
            break
        else:
            print(colored("Scelta non valida!", "red"))


if __name__ == "__main__":
    main()