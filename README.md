import random

def crea_puzzle(dim):
    numeri = list(range(dim * dim))
    random.shuffle(numeri)
    puzzle = [numeri[i:i+dim] for i in range(0, dim*dim, dim)]
    return puzzle

def stampa_puzzle(puzzle):
    for riga in puzzle:
        print(" ".join(map(lambda x: f"{x:2}", riga)))

def trova_posizione_vuota(puzzle):
    for i in range(len(puzzle)):
        for j in range(len(puzzle[i])):
            if puzzle[i][j] == 0:
                return i, j

def scambia_celle(puzzle, riga1, col1, riga2, col2):
    puzzle[riga1][col1], puzzle[riga2][col2] = puzzle[riga2][col2], puzzle[riga1][col1]

def gioca():
    dimensione = 3
    puzzle = crea_puzzle(dimensione)
    stampa_puzzle(puzzle)

    while True:
        riga_vuota, col_vuota = trova_posizione_vuota(puzzle)

        direzione = input("Muovi la cella vuota (w/a/s/d): ").lower()
        
        if direzione == 'w' and riga_vuota > 0:
            scambia_celle(puzzle, riga_vuota, col_vuota, riga_vuota - 1, col_vuota)
        elif direzione == 'a' and col_vuota > 0:
            scambia_celle(puzzle, riga_vuota, col_vuota, riga_vuota, col_vuota - 1)
        elif direzione == 's' and riga_vuota < dimensione - 1:
            scambia_celle(puzzle, riga_vuota, col_vuota, riga_vuota + 1, col_vuota)
        elif direzione == 'd' and col_vuota < dimensione - 1:
            scambia_celle(puzzle, riga_vuota, col_vuota, riga_vuota, col_vuota + 1)
        else:
            print("Mossa non valida. Riprova.")
            continue

        stampa_puzzle(puzzle)

        if all(puzzle[i][j] == i * dimensione + j + 1 for i in range(dimensione) for j in range(dimensione - 1)):
            print("Complimenti! Hai risolto il puzzle.")
            break

if __name__ == "__main__":
    gioca() 
