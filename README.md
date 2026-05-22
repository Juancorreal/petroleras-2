# LIBRERIAS
# Para la raíz cuadrada en el cálculo de IMC
import math
# Para limpiar la pantalla entre secciones
import os
print("Librerías cargadas correctamente")
# Clase para perfil físico
class UserProfile:

    """Perfil físico del usuario."""

    # Constructor principal clase
    def __init__(self, nombre, edad, peso, altura, sexo, nivel):

        self.nombre = nombre      # Guarda nombre usuario
        self.edad   = edad        # Guarda edad usuario
        self.peso   = peso        # Guarda peso corporal
        self.altura = altura      # Guarda altura usuario
        self.sexo   = sexo        # Guarda sexo biológico
        self.nivel  = nivel       # Guarda nivel actividad

    # Método cálculo IMC
    @property
    def imc(self):

        # Fórmula índice corporal
        return self.peso / ((self.altura / 100) ** 2)

    # Método categoría IMC
    @property
    def categoria_imc(self):

        # Guarda valor IMC
        b = self.imc

        # Condición bajo peso
        if b < 18.5:
            return "Bajo peso"

        # Condición peso normal
        if b < 25:
            return "Peso normal ✅"

        # Condición sobrepeso corporal
        if b < 30:
            return "Sobrepeso"

        # Caso obesidad corporal
        return "Obesidad"

    # Método metabolismo basal
    @property
    def tmb(self):

        # Fórmula para hombres
        if self.sexo == 'm':

            return (
                88.36                    # Valor base fórmula
                + 13.4 * self.peso      # Ajuste según peso
                + 4.8 * self.altura     # Ajuste según altura
                - 5.7 * self.edad       # Ajuste según edad
            )

        # Fórmula para mujeres
        return (
            447.6                   # Valor base fórmula
            + 9.2 * self.peso      # Ajuste según peso
            + 3.1 * self.altura    # Ajuste según altura
            - 4.3 * self.edad      # Ajuste según edad
        )

    # Método gasto calórico
    @property
    def tdee(self):

        # Diccionario niveles actividad
        factores = {

            'sedentario': 1.2,     # Actividad física mínima
            'ligero':     1.375,   # Ejercicio pocas veces
            'moderado':   1.55,    # Ejercicio frecuencia media
            'activo':     1.725    # Entrenamiento alta frecuencia
        }

        # Multiplica metabolismo y actividad
        return round(self.tmb * factores.get(self.nivel, 1.2))

    # Método calorías objetivo
    def calorias_objetivo(self, meta):

        # Superávit ganar músculo
        if meta == 'musculo':
            return self.tdee + 300

        # Déficit bajar grasa
        if meta == 'bajar':
            return self.tdee - 400

        # Mantiene mismas calorías
        return self.tdee

    # Método peso proyectado
    def peso_objetivo(self, meta):

        # Incremento masa muscular
        if meta == 'musculo':
            return round(self.peso * 1.05, 1)

        # Reducción peso corporal
        if meta == 'bajar':
            return round(self.peso * 0.92, 1)

        # Mantener peso actual
        return self.peso

    # Método resumen usuario
    def resumen(self):

        # Muestra nombre usuario
        print(f"  Nombre   : {self.nombre}")

        # Muestra edad usuario
        print(f"  Edad     : {self.edad} años")

        # Muestra peso corporal
        print(f"  Peso     : {self.peso} kg")

        # Muestra altura corporal
        print(f"  Altura   : {self.altura} cm")

        # Muestra IMC calculado
        print(f"  IMC      : {self.imc:.1f} — {self.categoria_imc}")

        # Muestra metabolismo basal
        print(f"  TMB      : {round(self.tmb)} kcal/día")

        # Muestra gasto calórico diario
        print(f"  TDEE     : {self.tdee} kcal/día")


# Confirma creación clase
print("Clase UserProfile definida")
# Clase para rutinas gimnasio
class WorkoutPlan:

    """Rutina semanal personalizada."""

    # Constructor principal clase
    def __init__(self, meta, nivel):

        # Guarda objetivo físico
        self.meta  = meta
        # Guarda nivel actividad
        self.nivel = nivel

    # Días según actividad
    @property
    def dias_por_nivel(self):

        """Cantidad semanal entrenamiento."""

        # Retorna días entrenamiento
        return {'sedentario': 3,'ligero': 4,'moderado': 5,'activo': 6}.get(self.nivel, 4)

    # Rutina ganar músculo
    def _rutina_musculo(self):

        # Lista rutina hipertrofia
        return [

            (
                "Lunes",
                "Pecho + Tríceps",

                [   # Lista ejercicios

                    ("Press de banca plano","4x8"),
                    ("Press inclinado mancuernas","3x10"),
                    ("Aperturas en polea","3x12"),
                    ("Fondos en paralelas","3x10"),
                    ("Extensión tríceps polea","3x12")
                ]
            ),

            (
                "Martes",
                "Espalda + Bíceps",

                [
                    ("Dominadas (o jalón al pecho)","4x8"),
                    ("Remo con barra","4x8"),
                    ("Remo en polea baja","3x10"),
                    ("Curl barra","3x10"),
                    ("Curl martillo mancuernas","3x12")
                ]
            ),

            (
                "Miércoles",
                "Piernas",

                [
                    ("Sentadilla con barra","4x8"),
                    ("Prensa de piernas","3x10"),
                    ("Extensión cuádriceps","3x12"),
                    ("Curl femoral","3x12"),
                    ("Pantorrilla de pie","4x15")
                ]
            ),

            (
                "Jueves",
                "Hombros",

                [
                    ("Press militar con barra","4x8"),
                    ("Elevaciones laterales","4x12"),
                    ("Elevaciones frontales","3x12"),
                    ("Pájaros (posterior)","3x12"),
                    ("Encogimientos trapecio","3x12")
                ]
            ),

            (
                "Viernes",
                "Full body + Core",

                [
                    ("Peso muerto","4x6"),
                    ("Press de banca","3x8"),
                    ("Sentadilla goblet","3x10"),
                    ("Plancha frontal","3x45s"),
                    ("Crunch en polea","3x15")
                ]
            ),

            (
                "Sábado",
                "Brazos + Core",

                [
                    ("Curl en predicador","4x10"),
                    ("Press francés","4x10"),
                    ("Curl concentrado","3x12"),
                    ("Extensión tríceps 1 brazo","3x12"),
                    ("Abdominales en rueda","3x10")
                ]
            )
        ]

    # Rutina pérdida grasa
    def _rutina_bajar(self):

        # Lista rutina definición
        return [

            (
                "Lunes",
                "Cardio + Pecho",

                [
                    ("Caminadora inclinada","20 min"),
                    ("Press banca mancuernas","3x15"),
                    ("Aperturas en cable","3x15"),
                    ("Flexiones","3x20"),
                    ("Box jumps","3x10")
                ]
            ),

            (
                "Martes",
                "Espalda + HIIT",

                [
                    ("Jalón al pecho agarre ancho","4x15"),
                    ("Remo sentado en polea","4x15"),
                    ("Face pull","3x15"),
                    ("Burpees","4x12"),
                    ("Remo con mancuerna","3x15")
                ]
            ),

            (
                "Miércoles",
                "Piernas + Cardio",

                [
                    ("Sentadilla sumo","4x15"),
                    ("Zancadas con mancuernas","3x12c/l"),
                    ("Prensa de piernas","3x15"),
                    ("Bicicleta estática","15 min"),
                    ("Pantorrillas en máquina","4x20")
                ]
            ),

            (
                "Jueves",
                "Full body metabólico",

                [
                    ("Peso muerto rumano","4x12"),
                    ("Press hombros mancuernas","3x15"),
                    ("Remo con mancuerna","3x15"),
                    ("Mountain climbers","3x30s"),
                    ("Plancha lateral","3x30sc/l")
                ]
            ),

            (
                "Viernes",
                "Cardio + Core",

                [
                    ("Elíptica o caminadora","25 min"),
                    ("Crunch bicicleta","4x20"),
                    ("Elevación piernas colgado","3x15"),
                    ("Plancha frontal","3x45s"),
                    ("Russian twists","3x20")
                ]
            )
        ]

    # Rutina mantenimiento físico
    def _rutina_mantener(self):

        # Lista rutina mantenimiento
        return [

            (
                "Lunes",
                "Pecho + Espalda",

                [
                    ("Press de banca","3x10"),
                    ("Remo con barra","3x10"),
                    ("Dominadas asistidas","3x8"),
                    ("Aperturas mancuernas","3x12"),
                    ("Cardio suave","10 min")
                ]
            ),

            (
                "Miércoles",
                "Piernas + Core",

                [
                    ("Sentadilla libre","3x10"),
                    ("Prensa de piernas","3x12"),
                    ("Zancadas","3x10c/l"),
                    ("Plancha frontal","3x40s"),
                    ("Abdominales","3x15")
                ]
            ),

            (
                "Viernes",
                "Full body",

                [
                    ("Peso muerto","3x8"),
                    ("Press hombros","3x10"),
                    ("Curl bíceps","3x12"),
                    ("Extensión tríceps","3x12"),
                    ("Cardio suave","15 min")
                ]
            ),

            (
                "Sábado",
                "Cardio + Movilidad",

                [
                    ("Caminadora / bicicleta","25 min"),
                    ("Estiramientos globales","10 min"),
                    ("Yoga / movilidad","15 min"),
                    ("Remo en máquina","10 min"),
                    ("Plancha + respiración","3x30s")
                ]
            ),

            (
                "Martes",
                "Hombros + Brazos",

                [
                    ("Press militar","3x10"),
                    ("Elevaciones laterales","3x12"),
                    ("Curl mancuernas","3x12"),
                    ("Fondos banco tríceps","3x12"),
                    ("Cardio 10 min","moderado")
                ]
            )
        ]

    # Selecciona rutina objetivo
    def get_rutina(self):

        """Devuelve rutina personalizada."""

        # Diccionario tipos rutina
        mapa = {

            'musculo':  self._rutina_musculo,
            'bajar':    self._rutina_bajar,
            'mantener': self._rutina_mantener
        }

        # Obtiene rutina correspondiente
        todos = mapa.get(
            self.meta,
            self._rutina_mantener
        )()

        # Filtra días necesarios
        return [

            dia for dia in todos[:self.dias_por_nivel]
        ]

    # Imprime rutina organizada
    def imprimir_rutina(self):

        """Muestra rutina semanal."""

        # Guarda rutina usuario
        rutina = self.get_rutina()

        # Recorre cada día
        for dia, foco, ejercicios in rutina:

            # Imprime encabezado día
            print(f"\n  📅 {dia.upper()} — {foco}")

            # Imprime línea separación
            print("  " + "-" * 40)

            # Formatea ejercicios rutina
            lineas = [

                f"  {e:<35} {s}"

                for e, s in ejercicios
            ]

            # Recorre ejercicios formateados
            for l in lineas:

                # Imprime ejercicio individual
                print(l)


# Mensaje confirmación clase
print("Clase WorkoutPlan definida")
# Funciones auxiliares programa

# Función dibujar silueta
def dibujar_silueta(imc, meta, es_actual=True):

    """Genera silueta corporal ASCII."""

    # Verifica silueta actual
    if es_actual:

        # Caso bajo peso
        if imc < 18.5:
            torso = "  |  |"

        # Caso peso normal
        elif imc < 25:
            torso = " | | |"

        # Caso sobrepeso corporal
        elif imc < 30:
            torso = "| | | |"

        # Caso obesidad corporal
        else:
            torso = "||| |||"

    # Caso silueta objetivo
    else:

        # Meta ganar músculo
        if meta == 'musculo':
            torso = "||[ ]||"

        # Meta perder peso
        elif meta == 'bajar':
            torso = "  |  | "

        # Meta mantenimiento físico
        else:
            torso = " | | | "

    # Lista partes cuerpo
    figura = [

        "   ( o )",          # Cabeza silueta
        "   \\___/",         # Cuello silueta
        f" /{torso}\\\n",      # Parte superior torso
        f"/ {torso} \\",     # Parte media torso
        f"  {torso}  ",      # Parte inferior torso
        f"  {torso}  ",      # Cadera silueta
        "  || ||",           # Piernas superiores
        "  || ||",           # Piernas inferiores
        " _|| ||_",          # Pies silueta
    ]

    # Retorna figura completa
    return figura


# Función mostrar siluetas
def mostrar_siluetas(perfil, meta):

    """Muestra comparación corporal."""

    # Genera silueta actual
    actual = dibujar_silueta(
        perfil.imc,
        meta,
        es_actual=True
    )

    # Genera silueta objetivo
    objetivo = dibujar_silueta(
        perfil.imc,
        meta,
        es_actual=False
    )

    # Texto peso actual
    etiqueta_actual = f"  ACTUAL ({perfil.peso} kg)"

    # Texto peso objetivo
    etiqueta_objetivo = (
        f"  OBJETIVO ({perfil.peso_objetivo(meta)} kg)"
    )

    # Imprime títulos siluetas
    print(
        f"\n  {etiqueta_actual:<22}  {etiqueta_objetivo}"
    )

    # Recorre ambas siluetas
    for a, o in zip(actual, objetivo):

        # Imprime siluetas alineadas
        print(f"  {a:<22}  {o}")

    # Salto línea visual
    print()


# Función barra IMC
def barra_imc(imc):

    """Muestra barra visual IMC."""

    # Categorías índice corporal
    categorias = [

        (18.5, "Bajo peso"),
        (25, "Normal"),
        (30, "Sobrepeso"),
        (40, "Obesidad")
    ]

    # Crea barra base
    barra = "[" + "=" * 30 + "]"

    # Calcula posición indicador
    pos = int(min(max((imc - 15) / (40 - 15), 0),1) * 30)

    # Construye barra final
    barra = ("[" + "-" * pos + "▲" + "-" * (30 - pos) + "]")

    # Imprime barra visual
    print(f"  IMC {imc:.1f}  {barra}")

    # Imprime categorías referencia
    print(f"  {'Bajo':>8}   {'Normal':>8}   {'Sobrepeso':>10}   Obesidad")

# Función validar inputs
def pedir_input_validado(mensaje,tipo,minval=None,maxval=None,opciones=None):

    """Valida datos ingresados."""

    # Ciclo validación continua
    while True:

        # Guarda entrada usuario
        raw = input(mensaje).strip()

        try:

            # Convierte tipo dato
            valor = tipo(raw)

            # Verifica opciones válidas
            if opciones and valor not in opciones:

                # Mensaje opciones válidas
                print(f"Opciones válidas: {opciones}")

                # Reinicia ciclo validación
                continue

            # Verifica valor mínimo
            if minval is not None and valor < minval:

                # Mensaje valor mínimo
                print(f"El valor mínimo es {minval}")

                # Reinicia ciclo validación
                continue

            # Verifica valor máximo
            if maxval is not None and valor > maxval:

                # Mensaje valor máximo
                print(f"El valor máximo es {maxval}")

                # Reinicia ciclo validación
                continue

            # Retorna valor válido
            return valor

        # Error conversión dato
        except ValueError:

            # Mensaje entrada inválida
            print(f"Entrada inválida. Intenta de nuevo.")


# Confirma funciones creadas
print("Funciones auxiliares definidas")
# Aplicación principal sistema

# Línea separación principal
SEP = "=" * 55

# Línea separación secundaria
SEP2 = "-" * 55

# Imprime separación principal
print(SEP)

# Título aplicación fitness
print("   🏋️  FITNESS TRACKER — ANÁLISIS Y RUTINAS")

# Imprime separación principal
print(SEP)

# Salto línea visual
print()


# Paso perfil usuario
print("📋 PASO 1 — Tu perfil físico")

# Imprime separación secundaria
print(SEP2)

# Pide nombre usuario
nombre = input(
    "  Nombre: "
).strip().capitalize()

# Pide edad validada
edad = pedir_input_validado(

    "  Edad (años): ",
    int,
    minval=14,
    maxval=80
)

# Pide peso validado
peso = pedir_input_validado(

    "  Peso actual (kg): ",
    float,
    minval=40,
    maxval=200
)

# Pide altura validada
altura = pedir_input_validado(

    "  Altura (cm): ",
    float,
    minval=140,
    maxval=220
)

# Texto sexo biológico
print("  Sexo biológico:")

# Opción sexo masculino
print("    m = Masculino")

# Opción sexo femenino
print("    f = Femenino")

# Pide sexo validado
sexo = pedir_input_validado(

    "  Tu opción: ",
    str,
    opciones=['m','f']
)

# Texto nivel actividad
print("  Nivel de actividad actual:")

# Opción sedentario
print(
    "    1 = Sedentario   (poco o ningún ejercicio)"
)

# Opción actividad ligera
print(
    "    2 = Ligero       (1–2 veces/semana)"
)

# Opción actividad moderada
print(
    "    3 = Moderado     (3–4 veces/semana)"
)

# Opción actividad alta
print(
    "    4 = Activo       (5+ veces/semana)"
)

# Pide nivel validado
nivel_num = pedir_input_validado(

    "  Tu opción (1–4): ",
    int,
    opciones=[1,2,3,4]
)

# Diccionario niveles actividad
nivel_map = {

    1:'sedentario',
    2:'ligero',
    3:'moderado',
    4:'activo'
}

# Traduce nivel numérico
nivel = nivel_map[nivel_num]

# Crea objeto perfil
perfil = UserProfile(

    nombre,
    edad,
    peso,
    altura,
    sexo,
    nivel
)

# Salto línea visual
print()

# Imprime separación principal
print(SEP)

# Título perfil físico
print("   📊 PASO 2 — Tu perfil físico")

# Imprime separación principal
print(SEP)

# Muestra resumen usuario
perfil.resumen()

# Salto línea visual
print()

# Muestra barra IMC
barra_imc(perfil.imc)


# Salto línea visual
print()

# Imprime separación principal
print(SEP)

# Título objetivo físico
print("   🎯 PASO 3 — Tu objetivo")

# Imprime separación principal
print(SEP)

# Opción ganar músculo
print(
    "  1 = 💪 Ganar músculo   (volumen + fuerza)"
)

# Opción bajar peso
print(
    "  2 = 🔥 Bajar de peso   (déficit + cardio)"
)

# Opción mantenimiento
print(
    "  3 = ⚖️  Mantenerse      (salud y forma física)"
)

# Pide objetivo validado
meta_num = pedir_input_validado(

    "  Tu opción (1–3): ",
    int,
    opciones=[1,2,3]
)

# Diccionario tipos metas
meta_map = {

    1:'musculo',
    2:'bajar',
    3:'mantener'
}

# Diccionario nombres metas
meta_label = {

    1:'💪 Ganar músculo',
    2:'🔥 Bajar de peso',
    3:'⚖️ Mantenerse'
}

# Traduce meta numérica
meta = meta_map[meta_num]


# Salto línea visual
print()

# Imprime separación principal
print(SEP)

# Título simulación corporal
print("   👤 PASO 4 — Simulación de cuerpo")

# Imprime separación principal
print(SEP)

# Muestra siluetas corporales
mostrar_siluetas(perfil, meta)


# Imprime separación principal
print(SEP)

# Título proyección física
print("   📈 PASO 5 — Proyección a 3 meses")

# Imprime separación principal
print(SEP)

# Calcula diferencia peso
dif_peso = round(

    perfil.peso_objetivo(meta)
    - perfil.peso,
    1
)

# Define signo resultado
signo = "+" if dif_peso >= 0 else ""

# Imprime objetivo elegido
print(
    f"  Objetivo elegido    : {meta_label[meta_num]}"
)

# Imprime peso actual
print(
    f"  Peso actual         : {perfil.peso} kg"
)

# Imprime peso proyectado
print(

    f"  Peso objetivo       : "
    f"{perfil.peso_objetivo(meta)} kg  "
    f"({signo}{dif_peso} kg)"
)

# Imprime calorías mantenimiento
print(
    f"  Calorías de mant.   : {perfil.tdee} kcal/día"
)

# Imprime calorías objetivo
print(

    f"  Calorías objetivo   : "
    f"{perfil.calorias_objetivo(meta)} kcal/día"
)

# Salto línea visual
print()

# Lista consejos generales
todos_los_consejos = [

    (
        'musculo',
        "Consume 1.6–2.2 g de proteína por kg de peso corporal al día."
    ),

    (
        'musculo',
        "Duerme 7–9 horas. La hipertrofia ocurre en la recuperación."
    ),

    (
        'musculo',
        "Aumenta pesos progresivamente (sobrecarga progresiva)."
    ),

    (
        'bajar',
        "Mantén un déficit de 300–500 kcal. No recortes más: perderás músculo."
    ),

    (
        'bajar',
        "La dieta representa ~80% del resultado. El cardio complementa."
    ),

    (
        'bajar',
        "No elimines la proteína al recortar calorías (mínimo 1.6 g/kg)."
    ),

    (
        'mantener',
        "Varía ejercicios cada 6–8 semanas para evitar el estancamiento."
    ),

    (
        'mantener',
        "Prioriza el sueño y el manejo del estrés tanto como el entrenamiento."
    ),

    (
        'mantener',
        "Consistencia ante todo: 3 días buenos > 6 días irregulares."
    ),
]

# Filtra consejos meta elegida
consejos = [

    c for m, c in todos_los_consejos
    if m == meta
]

# Título consejos clave
print("Consejos clave:")

# Recorre consejos filtrados
for i, c in enumerate(consejos, 1):

    # Imprime consejo individual
    print(f"  {i}. {c}")


# Crea plan entrenamiento
plan = WorkoutPlan(meta, nivel)

# Guarda cantidad días
dias = plan.dias_por_nivel

# Salto línea visual
print()

# Imprime separación principal
print(SEP)

# Título rutina semanal
print(
    f"   🗓️  PASO 6 — Tu rutina semanal ({dias} días)"
)

# Imprime separación principal
print(SEP)

# Imprime rutina personalizada
plan.imprimir_rutina()

# Guarda nombres entrenamientos
nombres_dias = [

    dia for dia, foco, ejercicios
    in plan.get_rutina()
]

# Calcula días descanso
dias_descanso = [

    d for d in [

        'Lunes',
        'Martes',
        'Miércoles',
        'Jueves',
        'Viernes',
        'Sábado',
        'Domingo'

    ]

    if d not in nombres_dias
]

# Salto línea visual
print()

# Imprime días descanso
print(

    f"  🛌 Días de descanso: "
    f"{', '.join(dias_descanso)}"
)

# Salto línea visual
print()

# Imprime separación principal
print(SEP)

# Mensaje final usuario
print(
    f"¡Éxitos en tu proceso, {perfil.nombre}!"
)

# Advertencia profesional salud
print(
    "Consulta un profesional de la salud antes de iniciar."
)

# Imprime separación principal
print(SEP)
