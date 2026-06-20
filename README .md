# Calorica Souver

App de salud y nutricion con planes de ejercicio por somatotipo, comidas recomendadas por pais y presupuesto, podometro nativo en segundo plano, contador de calorias y cronometro de rutinas con calculo de calorias en tiempo real. Diseño monocromatico estilo Apple Health. 100% offline.

---

## Descripcion

Calorica Souver es una aplicacion instalable como app nativa en Android (.apk) e iOS (.ipa). Ofrece:

- Planes de ejercicio segun tu tipo de cuerpo (ectomorfo, mesomorfo, endomorfo)
- Cronometro en tiempo real que calcula calorias quemadas durante cada rutina
- 5000+ comidas recomendadas filtradas por pais (10 paises) y presupuesto
- Podometro nativo que cuenta pasos en segundo plano, incluso con la app cerrada
- Conteo de calorias con anillo animado estilo Apple Health
- Notificaciones push con 10 sonidos sintetizados
- Todo funciona sin internet

---

## Caracteristicas principales

### Planes de ejercicio (80+ rutinas)

- 80+ rutinas organizadas por grupo muscular: Pecho, Espalda, Piernas, Hombros, Brazos, Abdomen, Cardio, Full body, Push/Pull/Legs, Circuitos HIIT, Potencia, Resistencia, Movilidad
- Filtro por dificultad: Principiante, Intermedio, Avanzado
- Filtro por somatotipo: Ectomorfo, Mesomorfo, Endomorfo
- Cronometro en tiempo real al iniciar cada rutina
- Calculo de calorias quemadas usando formula MET x peso x tiempo
- Cada ejercicio con series, repeticiones, descanso y musculo trabajado

### Somatotipos

- Ectomorfo: cuerpo delgado, metabolismo rapido. Plan de hipertrofia con pesos pesados
- Mesomorfo: cuerpo atletico. Entrenamiento balanceado
- Endomorfo: cuerpo robusto, metabolismo lento. Circuitos HIIT + cardio alto

### Comidas por pais (5000+ comidas)

- 10 paises: Venezuela, Colombia, Mexico, Argentina, Chile, Peru, Espana, Ecuador, Estados Unidos, Brasil
- 500+ comidas por pais generadas con combinaciones de proteinas, carbohidratos, verduras, frutas y snacks
- Cada comida con calorias, proteinas, carbohidratos, grasas, precio y descripcion
- Filtro por presupuesto: bajo ($), medio ($$), alto ($$$)
- Busqueda por nombre
- Filtrado por somatotipo

### Podometro nativo en segundo plano

- Servicio nativo de Android (StepCounterService) con sensor TYPE_STEP_COUNTER
- Plugin nativo de Capacitor (StepCounterPlugin) que conecta el sensor con la app
- Cuenta pasos incluso con la app cerrada
- Se reinicia solo si Android lo cierra (START_STICKY)
- Resetea los pasos cada dia automaticamente
- Calcula kilometros y calorias quemadas
- Permisos solicitados al abrir la app por primera vez

### Conteo de calorias

- Anillo de calorias animado estilo Apple Health
- Anillos de macronutrientes
- Base de datos local con mas de 60 alimentos
- Grafica semanal de consumo
- Navegacion entre dias

### Notificaciones push

- 9 tipos de notificaciones contextuales
- Recordatorio diario configurable
- 10 sonidos sintetizados (Web Audio API)
- Vibracion personalizada
- Icono de la app en cada notificacion

---

## Tecnologias utilizadas

| Categoria | Tecnologia | Uso |
|-----------|-----------|-----|
| Framework | Next.js 16 (App Router) | Renderizado y API routes |
| Lenguaje | TypeScript 5 | Tipado estatico |
| Estilos | Tailwind CSS 4 + shadcn/ui | Diseño |
| Base de datos | Prisma ORM + SQLite | Persistencia web |
| Almacenamiento | IndexedDB | Datos offline |
| Estado | Zustand + TanStack Query | Estado global |
| Animaciones | Framer Motion | Transiciones |
| Iconos | Lucide React | Iconos monocromos |
| Sensores | TYPE_STEP_COUNTER + DeviceMotion | Podometro nativo |
| PWA | Manifest + Service Worker | Instalacion y offline |
| Notificaciones | Notifications API + Service Worker | Push + recordatorios |
| Audio | Web Audio API | 10 sonidos |
| Movil | Capacitor 8 | APK e IPA |
| Android | Gradle + Android SDK 34 + Java | APK nativo |
| iOS | xcframeworks arm64 | IPA nativo |
| CI/CD | GitHub Actions | Compilacion automatica |

---

## Instalacion

```bash
git clone https://github.com/TU_USUARIO/calorica-souver.git
cd calorica-souver
bun install
bun run db:push
bun run dev
```

---

## Descargar APK / IPA

### PWA
Abre la app en Chrome o Safari -> "Agregar a pantalla de inicio"

### APK (Android)
Descarga `souver.apk`, activa "Origenes desconocidos" e instala

### IPA (iOS)
Descarga `souver.ipa`, instala con AltStore o Sideloadly

### Compilar
```bash
./build-apk.sh   # Android
./build-ipa.sh   # iOS
```

---

## Estructura del proyecto

```
calorica-souver/
|-- src/
|   |-- app/
|   |   |-- page.tsx              # Orquestador
|   |   |-- souver.apk            # APK compilado
|   |   |-- souver.ipa            # IPA compilado
|   |   +-- api/                  # API routes (web)
|   |-- components/
|   |   |-- splash-screen.tsx     # Splash animado
|   |   |-- onboarding.tsx        # Registro con apellido
|   |   |-- dashboard.tsx         # Inicio con anillo
|   |   |-- workout-screen.tsx    # 80+ rutinas + cronometro
|   |   |-- food-screen.tsx       # 5000+ comidas por pais
|   |   |-- activity-screen.tsx   # Podometro
|   |   |-- profile.tsx           # Perfil + IMC
|   |   |-- settings.tsx          # Ajustes + sonidos
|   |   +-- bottom-nav.tsx        # Navegacion
|   +-- lib/
|       |-- body-types.ts         # Somatotipos + planes
|       |-- gym-routines.ts       # 80+ rutinas + MET
|       |-- country-foods.ts      # 5000+ comidas
|       |-- calories.ts           # BMR/TDEE + macros
|       |-- pedometer.ts          # Podometro nativo + web
|       |-- notifications.ts      # Push + 10 sonidos
|       |-- local-db.ts           # IndexedDB
|       +-- store.ts              # Zustand
|-- android/
|   +-- app/src/main/java/com/calorica/souver/
|       |-- MainActivity.java     # Permisos + servicio
|       |-- StepCounterService.java  # Podometro nativo
|       +-- StepCounterPlugin.java   # Bridge Capacitor
|-- ios/                          # Proyecto iOS
|-- .github/workflows/            # GitHub Actions
+-- package.json
```

---

## Archivos compilados

| Archivo | Version | Tamaño | Plataforma |
|---------|---------|--------|------------|
| souver.apk | 3.2.2 | 41 MB | Android |
| souver.ipa | 3.2.2 | 5.7 MB | iOS |

---

## Licencia

Proyecto de portafolio. (c) 2025 Calorica Souver.

---

Calorica Souver v3.2.2 - Tu app de salud, nutricion y ejercicio
