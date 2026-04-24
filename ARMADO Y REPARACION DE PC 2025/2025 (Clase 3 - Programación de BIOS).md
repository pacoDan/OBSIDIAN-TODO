#### Temas Principales Cubiertos
- **Definición de BIOS**: Sistema básico de entrada/salida (Basic Input Output System). Diferencias entre BIOS Legacy (16 bits, interfaz texto, teclado) y UEFI (32/64 bits, interfaz gráfica, mouse/teclado, soporte GPT, Secure Boot).
- **Chips de BIOS**: Tipos históricos (EPROM, EEPROM, Flash NOR/NAND, SPI Flash). Identificación: pata 1 con marca, voltajes (3.3V, 1.8V), modelos (Winbond W25Q, Macronix MX). Ubicación en placa madre.
- **Programación de BIOS**: Uso de CH341A (programador USB con pinza/zócalo). Pasos: detectar chip, leer/backup, borrar, escribir binario, verificar. Adaptadores para voltajes bajos. Métodos alternos: USB con botón de flash, software (HP, MSI), reset CMOS (sacar pila CR2032 o usar jumper).
- **Errores Comunes**: Corrupción por corte de energía durante flash, incompatibilidades (procesador/BIOS), voltajes incorrectos. Recuperación: pinza, desoldar chip, o métodos USB.
- **Hardware Relacionado**: Pila CR2032 (guarda cambios, dura años, errores si baja <2.2V). Jumper CMOS (para reset). Orden de arranque, particiones (MBR vs GPT).
- **Ejemplos Prácticos**: Desbloqueo de notebooks del gobierno (Juana Manso, Plan Sarmiento) con binarios del Drive. Actualización de BIOS para compatibilidad (ej. Ryzen en placas DDR4).

#### Preguntas de Validación y Respuestas (Para Exámenes)
Estas son preguntas explícitas marcadas como "de validación" o útiles para exámenes, con respuestas directas del profesor. Se recopilan todas, incluyendo detalles técnicos.

- **¿Cómo identificar las patas de un chip SPI Flash?**  
  Respuesta: Pata 1 tiene una marca (punto o indentación). Orden: 1-2-3-4 (fila superior), 5-6-7-8 (fila inferior, con 5 frente a 4 y 8 frente a 1). Cable rojo de pinza va en pata 1.

- **¿Dónde se conecta la pinza en el CH341A?**  
  Respuesta: Cable rojo en pata 1 del chip. Pinza para chips SPI Flash (ej. W25Q para 25-series, W24 para 24-series).

- **¿Cuáles son los pasos para programar BIOS con CH341A?**  
  Respuesta: 1) Detectar chip. 2) Leer (backup). 3) Borrar (erase). 4) Leer nuevamente (verificar vacío: todo 0 o F). 5) Seleccionar binario. 6) Escribir (write). 7) Verificar. Desconectar batería, RAM y pila CMOS antes. Usar adaptador si voltaje <3.3V.

- **¿Qué es la pila CR2032 y para qué sirve?**  
  Respuesta: Pila de 3V que guarda cambios de BIOS (configuraciones). Si baja <2.2V, errores de checksum, hora/fecha incorrecta. Reset CMOS: sacarla 10 min o usar jumper.

- **¿Qué diferencia hay entre BIOS Legacy y UEFI?**  
  Respuesta: Legacy: 16 bits, texto/teclado, MBR, arranque secuencial, actualización riesgosa. UEFI: 32/64 bits, gráfica/mouse, GPT, arranque paralelo, Secure Boot, actualización fácil (USB/software).

- **¿Cómo saber si una BIOS es Legacy o UEFI?**  
  Respuesta: Visual: Legacy es texto simple; UEFI es gráfica. Técnica: Ver soporte GPT, Secure Boot, interfaz.

- **¿Qué pasa si conectas un chip de 1.8V sin adaptador?**  
  Respuesta: Se quema el chip (voltaje excesivo). Siempre usar adaptador para voltajes bajos.

- **¿Cómo resetear BIOS (Clear CMOS)?**  
  Respuesta: Sacar pila CR2032 10 min, o usar jumper en pines CLR CMOS (conectar 2-3 para reset, luego volver a 1-2).

- **¿Qué comandos de teclas para flashear BIOS en notebooks?**  
  Respuesta: Dependiente del fabricante: HP (F10 o Windows+B larga), Asus (F2), MSI (botón USB). Mantener escape + power + Windows+B corta/larga.

- **¿Por qué no actualizar BIOS desde Windows?**  
  Respuesta: Riesgo de corrupción si hay BSOD o corte de luz. Mejor usar USB o botón de flash.

- **¿Qué hacer si se corta luz durante flash?**  
  Respuesta: Chip corrupto; recuperar con pinza CH341A o reemplazar chip.

- **¿Cómo identificar voltaje de chip?**  
  Respuesta: Leer datasheet (ej. Winbond W25Q64: 3.3V). Si <3V, usar adaptador en CH341A.

- **¿Qué es un jumper y para qué se usa en BIOS?**  
  Respuesta: Conector que une pines (ej. para Clear CMOS o configurar master/slave en discos antiguos).

- **¿Diferencia entre particiones MBR y GPT?**  
  Respuesta: MBR: Legacy, hasta 2TB. GPT: UEFI, >2TB, más seguro.

- **¿Qué es Secure Boot y cuándo usarlo?**  
  Respuesta: Arranque seguro; verifica firmware/drivers firmados. Usar en juegos (Valorant) o sistemas modernos.

#### Consultas y Respuestas Durante la Clase
Recopilación de todas las consultas del chat y respuestas del profesor, útiles para exámenes y comprensión.

- **¿Cuánto tiempo dura la clase?**  
  Respuesta: Mínimo 2 horas para asistencia completa.

- **¿Cómo recuperar clases faltadas?**  
  Respuesta: Mail con instrucciones; responder pregunta privada al profesor.

- **¿Se puede cambiar de 32 a 64 bits en compus viejas?**  
  Respuesta: Sí, reinstalando Windows actual, pero usar Mini OS para compatibilidad.

- **¿Qué pasa si instalas Windows 10 en Legacy?**  
  Respuesta: Dificultad; usar GPT con compatibilidad MBR.

- **¿Por qué Legacy no soporta >2TB?**  
  Respuesta: Limitación de 16 bits.

- **¿Diferencia entre BIOS Legacy y modo Legacy en UEFI?**  
  Respuesta: Legacy es BIOS antigua; modo Legacy en UEFI es compatibilidad.

- **¿Cómo saber BIOS de mi PC?**  
  Respuesta: Entrar a setup (F2, Del, etc.) o comando DXDIAG en Windows.

- **¿Recomiendas beta de BIOS?**  
  Respuesta: No; usar versiones estables.

- **¿Qué pasa si BIOS corrupta?**  
  Respuesta: No prende; recuperar con USB, pinza o desoldar.

- **¿Cómo flashear BIOS en notebooks HP?**  
  Respuesta: Software HP BIOS Update o USB con comandos de teclas.

- **¿Por qué no usar utilidad Gigabyte para BIOS?**  
  Respuesta: Riesgo alto durante ejecución en Windows.

- **¿Todas las PCs tienen pila CR2032?**  
  Respuesta: No; algunas notebooks no; desktops sí.

- **¿Qué hacer si siento descarga en chasis?**  
  Respuesta: Posible defecto; inspeccionar profesionalmente, no usar.

#### Recomendaciones y Lo Que No Se Debe Hacer
Basado en la transcripción, con énfasis en programación de BIOS y seguridad.

- **Recomendaciones**:
  - Siempre hacer backup del binario original antes de escribir.
  - Usar voltaje correcto (adaptador si necesario) para evitar quemar chips.
  - Desconectar batería, RAM y pila CMOS antes de programar.
  - Leer datasheet del chip para confirmar modelo y pines.
  - Probar con pinza antes de desoldar; desoldar solo como último recurso.
  - Actualizar BIOS solo si es necesario (incompatibilidad de hardware).
  - Usar cargadores originales y verificar tierra en tomas.
  - Repasar con Drive y clases grabadas para exámenes.
  - Completar asistencia inmediatamente; usar comandos (!files, !asistencia).
  - Participar en grupo WhatsApp para consultas externas.
  - Cambiar pila CR2032 si hay errores de checksum o hora.

- **Lo Que No Se Debe Hacer**:
  - No cortar energía durante flash (corrompe BIOS).
  - No conectar chips de bajo voltaje sin adaptador (quema).
  - No usar versiones beta de BIOS.
  - No actualizar desde Windows (riesgo de corrupción).
  - No tocar pines al revés o sin identificar pata 1.
  - No forzar jumper o pila sin desconectar todo.
  - No usar IA o copiar respuestas en exámenes (verificado por profesor).
  - No ignorar descargas eléctricas; dejar de usar hasta reparar.
  - No formatear USB en FAT32 incorrectamente para flash.
  - No olvidar backup; perder datos originales.
  - No exceder vida útil de chips (reescribir mucho los daña).
  - No mezclar binarios incompatibles (verificar modelo de placa/procesador).

#### Lecciones Aprendidas
- **Programación de BIOS es Técnica y Riesgosa**: Requiere precisión; un error puede inutilizar la PC. Siempre priorizar backup y verificación.
- **Diferencias Legacy vs UEFI**: Entender para compatibilidad (ej. Windows 11 requiere UEFI).
- **Hardware Básico**: Chips, voltajes y reset CMOS son fundamentales; no subestimar la pila o jumper.
- **Seguridad Primero**: Descargas eléctricas indican fallos; no ignorar.
- **Preparación para Exámenes**: 100 preguntas de desarrollo; repasar transcripciones, Drive y comandos. Honestidad en respuestas.
- **Comunidad y Recursos**: Usar Drive, WhatsApp y Twitch para soporte; el curso es gratuito y vocacional.
- **Práctica Ética**: Cobrar honestamente; no ser "chanta" con precios inflados.

#### Conclusión y Avisos Finales
- **Cierre de Clase**: A las 21:46, se detiene contador de tiempo. Felices fiestas deseadas.
- **Avisos**: Examen requiere desarrollo; recuperar clases pronto. Certificado tarda; asistencia completa obligatoria. Próxima clase: primer sábado de enero. Profesor disponible en WhatsApp (no siempre). Enlaces: WhatsApp (consultas), Drive (materiales), Formulario (asistencia). No usar IA en respuestas.



---


- **¿Cuándo yo selecciono Windows 7 en Rufus?**  
  Respuesta: Automáticamente me va a elegir MBR. (Relacionado con particiones: Windows 7 usa MBR, Windows 10/11 usa GPT por defecto).

- **¿Cómo identificar las patas de nuestro chip?**  
  Respuesta: Pata 1 tiene una marca (punto o indentación). Orden: 1-2-3-4 (fila superior), 5-6-7-8 (fila inferior, con 5 frente a 4 y 8 frente a 1). Cable rojo de pinza va en pata 1. (Específico para chips SPI Flash en programación de BIOS).

- **¿Cuáles son los pasos a seguir cuando conectan y van a hacer una programación de BIOS con el CH341A y el programmer?**  
  Respuesta: Una vez que detecta el chip, leerlo (backup), borrarlo, leer nuevamente (verificar vacío: todo 0 o F), seleccionar binario, escribirlo, verificar. Desconectar batería, RAM y pila CMOS antes. Usar adaptador si voltaje <3.3V. (Pasos completos para evitar errores en flash de BIOS).