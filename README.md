# GonzalezFabian_Fibonacci.asm
Se debe pedir al usuario por consola cuántos número de la serie Fibonacci desea generar, posteriormente, y con base en el número introducido generé la serie y muestre por consola el resultado
# Programa: Serie de Fibonacci y suma de términos
# Autor: Fabian Gonzalez
# Archivo: GonzalezFabian_Fibonacci.asm
# Descripción: El programa solicita al usuario cuántos números desea generar de la serie
#              de Fibonacci, imprime la serie en consola y finalmente muestra la suma
#              de todos los términos.

.data
    msg1: .asciiz "¿Cuántos números de la serie Fibonacci desea generar?: "
    msg2: .asciiz "Serie Fibonacci: "
    msg3: .asciiz "\nLa suma de los números es: "
    espacio: .asciiz " "

.text
.globl main
main:

    # --- Pedir cantidad de términos ---
    li $v0, 4
    la $a0, msg1
    syscall

    li $v0, 5
    syscall
    move $t0, $v0          # $t0 = cantidad de términos (n)

    # Inicializar valores de Fibonacci
    li $t1, 0              # primer término (F0 = 0)
    li $t2, 1              # segundo término (F1 = 1)
    li $t3, 0              # suma total

    # Imprimir mensaje "Serie Fibonacci:"
    li $v0, 4
    la $a0, msg2
    syscall

    # --- Imprimir y sumar serie ---
    li $t4, 0              # contador

loop_fib:
    beq $t4, $t0, fin      # si contador == n, salir

    # Imprimir término actual ($t1)
    li $v0, 1
    move $a0, $t1
    syscall

    # Imprimir espacio
    li $v0, 4
    la $a0, espacio
    syscall

    # Sumar término actual
    add $t3, $t3, $t1

    # Calcular siguiente término
    add $t5, $t1, $t2      # $t5 = $t1 + $t2
    move $t1, $t2          # actualizar $t1
    move $t2, $t5          # actualizar $t2

    # Incrementar contador
    addi $t4, $t4, 1
    j loop_fib

# --- Mostrar suma final ---
fin:
    li $v0, 4
    la $a0, msg3
    syscall

    li $v0, 1
    move $a0, $t3
    syscall

    # Salir del programa
    li $v0, 10
    syscall
