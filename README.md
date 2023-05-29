
# ¿SE PUEDE APLICAR LA PROBABILIDAD PARA GANAR DINERO EN EL MERCADO DE VALORES?


Ciertamente, la probabilidad se puede aplicar para tomar decisiones de inversión informadas en el mercado de valores. Si bien no garantiza el éxito, comprender y utilizar la probabilidad puede ayudar a los inversores a evaluar los riesgos, evaluar los posibles rendimientos y tomar decisiones más informadas.

En este proyecto, nuestro objetivo es aprovechar las habilidades de programación para analizar datos históricos del mercado de valores, desarrollar modelos predictivos y evaluar las probabilidades de diferentes resultados en el mercado. Mediante el uso de técnicas estadísticas y de aprendizaje automático, podemos identificar patrones, tendencias y posibles oportunidades en el mercado.



## Authors

- Ricardo Falcón Díaz
- Laura Odette Cruz Jasso

## ¿ QUÉ TIPOS DE PROBLEMA RESUELVE?
MÉTODO DE DESVIACIÓN ESTÁNDAR
 

Supongamos que tienes una cartera
de inversión con el 60% de tus fondos
asignados a una empresa de
tecnología (rendimiento promedio del
12% y desviación estándar del 8%) y el
40% de tus fondos asignados a una
empresa de energía (rendimiento
promedio del 8% y desviación
estándar del 6%). Quieres calcular el
rendimiento esperado y la desviación
estándar de tu cartera.

MÉTODO DEL RUIDO
BLANCO


Supongamos que estás estudiando el
comportamiento de una partícula en un medio
líquido y deseas simular su movimiento
utilizando una caminata aleatoria con ruido
blanco. Quieres analizar cómo la partícula se
mueve a lo largo de 100 pasos, donde cada paso
representa un intervalo de tiempo. donde la
media es 0.2 y la desviación es 0.5

MÉTODO DE BLACK
SCHOLES


Supongamos que estás interesado en
calcular el valor de una opción de
compra ( call option ) utilizando el
modelo Black Scholes. Tienes los
siguientes datos:Precio actual de la
acción (S): $100Precio de ejercicio
(K): $105Vencimiento de la opción en
6 mesesDeseas calcular el valor de la
opción de compra utilizando una tasa
de interés libre de riesgo del 5% anual
y una volatilidad anual del 20%.

## Python code
```python
import math
import os
import random
import matplotlib.pyplot as plt
def clear_screen():
    os.system('cls' if os.name == 'nt' else 'clear')

def mostrar_menu():
    clear_screen()
    print("Menu:")
    print("1. Método de Desviación Estandar ")
    print("2. Método del ruido blanco")
    print("3. Método de Black Scholes")
    print("4. Simulación")
    print(" 5 Salir")

while True:
    mostrar_menu()
    opcion = input("Seleccione una opción (1-4): ")

    if opcion == "1":
        clear_screen()
        print("Método de Desviación Estandar")


        def calcular_rendimiento_esperado(ponderaciones, rendimientos):

            rendimiento_esperado = sum(
                ponderacion * rendimiento for ponderacion, rendimiento in zip(ponderaciones, rendimientos))
            return rendimiento_esperado


        def calcular_varianza(ponderaciones, rendimientos, desviaciones):
            varianza = sum(
                ponderacion ** 2 * desviacion ** 2 for ponderacion, desviacion in zip(ponderaciones, desviaciones))
            return varianza


        def calcular_desviacion_estandar(varianza):
            desviacion_estandar = math.sqrt(varianza)
            return desviacion_estandar


        # Datos de la cartera de inversiones
        p1 = int(input("Dame el porcentaje de asignacion en acciones de la primer empresa: "))
        p2 = int(input("Dame el porcentaje de asignacion en acciones de la segunda empresa: "))
        p11 = p1 / 100
        p22 = p2 / 100
        r1 = int(input("Dame el rendimiento promedio para la primer empresa: "))
        r2 = int(input("Dame el rendimiento promedio para la segunda empresa: "))
        r11 = r1 / 100
        r22 = r2 / 100
        d1 = int(input("Dame la desviación estándar para la primer empresa: "))
        d2 = int(input("Dame la desviación estándar para la segunda empresa: "))
        d11 = d1 / 100
        d22 = d2 / 100
        ponderaciones = [p11, p22]
        rendimientos = [r11, r22]
        desviaciones = [d11, d22]

        rendimiento_esperado = calcular_rendimiento_esperado(ponderaciones, rendimientos)
        varianza = calcular_varianza(ponderaciones, rendimientos, desviaciones)
        desviacion_estandar = calcular_desviacion_estandar(varianza)
        print(f"Rendimiento esperado de la cartera: {rendimiento_esperado}")
        print(f"Desviación estándar de la cartera: {desviacion_estandar}")

        input("Presione Enter para continuar...")

    elif opcion == "2":
        clear_screen()
        print("Método del ruido blanco")


        def caminata_aleatoria_ruido(n_pasos, mu, sigma):
            posicion = 0
            historia = [posicion]

            for _ in range(n_pasos):
                incremento = random.gauss(mu, sigma)

                posicion += incremento

                historia.append(posicion)

            return historia


        n_pasos = int(input("Dame el numero de movimientos que se realizara en la caminata: "))
        mu = float(input("Dame la media del ruido blanco: "))
        sigma = float(input("Dame la desviación estándar del ruido blanco: "))

        historia = caminata_aleatoria_ruido(n_pasos, mu, sigma)

        plt.plot(range(n_pasos + 1), historia)
        plt.xlabel('Pasos')
        plt.ylabel('Posición')
        plt.title('Caminata Aleatoria con Ruido Blanco')
        plt.show()
        input("Presione Enter para continuar...")

    elif opcion == "3":
        clear_screen()
        print("Ha seleccionado el método de Black Scholes")

        def black_scholes(S, K, T, r, sigma):
            d1 = (math.log(S / K) + (r + 0.5 * sigma ** 2) * T) / (sigma * math.sqrt(T))
            d2 = d1 - sigma * math.sqrt(T)
            call_price = S * norm_cdf(d1) - K * math.exp(-r * T) * norm_cdf(d2)
            return call_price

        def norm_cdf(x):
            return (1.0 + math.erf(x / math.sqrt(2.0))) / 2.0


        S = float(input("Hola, por favor ingresa el precio actual de la acción: "))
        K = float(input("Ingresa el precio de ejercicio (strike price): "))
        m = float(input("Ingresa en cuántos meses quieres que venza (no mayor a 12 meses): "))
        T = m / 12
        i = float(input("Dame el porcentaje de interés libre de riesgo: "))
        r = i / 100
        s = float(input("Dame la volatilidad anual: "))
        sigma = s / 100  # Volatilidad anual (20%)


        respuesta = black_scholes(S, K, T, r, sigma)


        print(f"El valor de la opción de compra es: {respuesta}")

        input("Presione Enter para continuar...")
    elif opcion == "4":
        clear_screen()
        print("Bienvenido a la Simulación, elige una:")
        while True:
            print("1. Método de Desviación Estándar")
            print("2. Método del Ruido Blanco")
            print("3. Método de Black-Scholes")
            print("4. Salir")

            opcion = input("Ingrese el número de opción: ")

            if opcion == "1":
                clear_screen()
                print("Método de Desviación Estándar")
                import random
                import math


                def calcular_rendimiento_esperado(ponderaciones, rendimientos):
                    rendimiento_esperado = sum(
                        ponderacion * rendimiento for ponderacion, rendimiento in zip(ponderaciones, rendimientos))
                    return rendimiento_esperado


                def calcular_varianza(ponderaciones, rendimientos, desviaciones):
                    varianza = sum(ponderacion ** 2 * desviacion ** 2 for ponderacion, desviacion in
                                   zip(ponderaciones, desviaciones))
                    return varianza


                def calcular_desviacion_estandar(varianza):
                    desviacion_estandar = math.sqrt(varianza)
                    return desviacion_estandar


                # Datos de la cartera de inversiones generados aleatoriamente
                p1 = random.randint(0, 100)
                p2 = random.randint(0, 100)
                p11 = p1 / 100
                p22 = p2 / 100

                r1 = random.uniform(0, 10)
                r2 = random.uniform(0, 10)
                r11 = r1 / 100
                r22 = r2 / 100

                d1 = random.uniform(0, 5)
                d2 = random.uniform(0, 5)
                d11 = d1 / 100
                d22 = d2 / 100

                ponderaciones = [p11, p22]
                rendimientos = [r11, r22]
                desviaciones = [d11, d22]

                rendimiento_esperado = calcular_rendimiento_esperado(ponderaciones, rendimientos)
                varianza = calcular_varianza(ponderaciones, rendimientos, desviaciones)
                desviacion_estandar = calcular_desviacion_estandar(varianza)

                print("Método de Desviación Estándar")
                print(f"Porcentaje de asignación en acciones de la primer empresa: {p1}")
                print(f"Porcentaje de asignación en acciones de la segunda empresa: {p2}")
                print(f"Rendimiento promedio para la primer empresa: {r1}")
                print(f"Rendimiento promedio para la segunda empresa: {r2}")
                print(f"Desviación estándar para la primer empresa: {d1}")
                print(f"Desviación estándar para la segunda empresa: {d2}")
                print(f"Rendimiento esperado de la cartera: {rendimiento_esperado}")
                print(f"Desviación estándar de la cartera: {desviacion_estandar}")

                input("Presione Enter para continuar...")


            elif opcion == "2":
                clear_screen()
                print("Método del Ruido Blanco")
                import random
                import math
                import matplotlib.pyplot as plt


                def caminata_aleatoria_ruido(n_pasos, mu, sigma):
                    posicion = 0
                    historia = [posicion]

                    for _ in range(n_pasos):
                        incremento = random.gauss(mu, sigma)
                        posicion += incremento
                        historia.append(posicion)

                    return historia


                n_pasos = random.randint(10, 100)
                mu = random.uniform(-1, 1)
                sigma = random.uniform(0.1, 1)

                historia = caminata_aleatoria_ruido(n_pasos, mu, sigma)

                plt.plot(range(n_pasos + 1), historia)
                plt.xlabel('Pasos')
                plt.ylabel('Posición')
                plt.title('Caminata Aleatoria con Ruido Blanco')
                plt.show()

                input("Presione Enter para continuar...")


            elif opcion == "3":
                clear_screen()
                print("Método de Black-Scholes")
                import random
                import math


                def black_scholes(S, K, T, r, sigma):
                    d1 = (math.log(S / K) + (r + 0.5 * sigma ** 2) * T) / (sigma * math.sqrt(T))
                    d2 = d1 - sigma * math.sqrt(T)
                    call_price = S * norm_cdf(d1) - K * math.exp(-r * T) * norm_cdf(d2)
                    return call_price


                def norm_cdf(x):
                    return (1.0 + math.erf(x / math.sqrt(2.0))) / 2.0


                S = random.uniform(50, 100)
                K = random.uniform(0, 50)
                m = random.randint(1, 12)
                T = m / 12
                i = random.uniform(0, 10)
                r = i / 100
                s = random.uniform(10, 50)
                sigma = s / 100

                respuesta = black_scholes(S, K, T, r, sigma)

                print("Ha seleccionado el método de Black Scholes")
                print(f"Precio actual de la acción: {S}")
                print(f"Precio de ejercicio (strike price): {K}")
                print(f"Meses hasta el vencimiento: {m}")
                print(f"Porcentaje de interés libre de riesgo: {i}")
                print(f"Volatilidad anual: {s}")

                print(f"\nEl valor de la opción de compra es: {respuesta}")
                input("Presione Enter para continuar...")


            elif opcion == "4":
                break

            else:
                print("Opción inválida. Por favor, ingrese un número válido.")

        print("¡Hasta luego!")

        break



    elif opcion == "5":

        clear_screen()
        print("Saliendo del programa...")
        break

    else:
        print("Opción inválida. Por favor, seleccione nuevamente.")
        input("Presione Enter para continuar...")

