# Sudoku
#CODIGO 
#Es un generador de sudokus para poder llenar de forma creativa
import random

# Quiero meter este cambio
###Segundo cambio con Jeison


def imprimir_tablero(tablero):
    for fila in tablero:
        print(" ".join(str(num) if num != 0 else '.' for num in fila))

def es_valido(tablero, fila, col, num):
    # Verificar si el número ya está en la fila
    if num in tablero[fila]:
        return False

    # Verificar si el número ya está en la columna
    if num in [tablero[i][col] for i in range(9)]:
        return False

    # Verificar si el número ya está en el subcuadro 3x3
    inicio_fila = (fila // 3) * 3
    inicio_col = (col // 3) * 3
    for i in range(inicio_fila, inicio_fila + 3):
        for j in range(inicio_col, inicio_col + 3):
            if tablero[i][j] == num:
                return False

    return True

def llenar_tablero(tablero):
    for fila in range(9):
        for col in range(9):
            if tablero[fila][col] == 0:
                # Probar números del 1 al 9 en orden aleatorio
                numeros = list(range(1, 10))
                random.shuffle(numeros)
                for num in numeros:
                    if es_valido(tablero, fila, col, num):
                        tablero[fila][col] = num
                        if llenar_tablero(tablero):
                            return True
                        tablero[fila][col] = 0
                return False
    return True

def generar_sudoku():
    # Crear un tablero vacío
    tablero = [[0 for _ in range(9)] for _ in range(9)]
    # Llenar el tablero de manera válida
    llenar_tablero(tablero)
    return tablero

def remover_numeros(tablero, vacios=40):
    # Remover números para crear el rompecabezas
    while vacios > 0:
        fila = random.randint(0, 8)
        col = random.randint(0, 8)
        if tablero[fila][col] != 0:
            tablero[fila][col] = 0
            vacios -= 1

# Generar el sudoku
tablero_sudoku = generar_sudoku()
remover_numeros(tablero_sudoku, vacios=40)

# Imprimir el sudoku generado
imprimir_tablero(tablero_sudoku)
