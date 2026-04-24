Aquí tienes la estructura técnica de la clase sobre **Programación de BIOS** organizada en forma de árbol:

**Programación de BIOS: Software fundamental (firmware) que inicializa el hardware y carga el sistema operativo.**

- **1. Diferencias entre BIOS Legacy y UEFI**
    
    - **BIOS Legacy:** Arquitectura de 16 bits, esquema de partición MBR, límite de 2 TB en discos, interfaz de solo teclado.
    - **UEFI (Unified Extensible Firmware Interface):** Arquitectura de 32/64 bits, esquema GPT, soporte para discos de gran capacidad (Zab), interfaz gráfica con mouse.
    - **Seguridad:** UEFI incluye **Secure Boot** (arranque seguro) para evitar malware a nivel de firmware.
- **2. Identificación y Hardware del Chip**
    
    - **Tipos de Chips:** EPROM (borrable por UV), EEPROM (eléctrico), Flash NOR/NAND y **SPI Flash** (el más común de 8 patas).
    - **Marcas Comunes:** Winbond (W25), Macronics (MX25), ATMEL.
    - **Mapeo de Pines (8 patas):**
        - **Pata 1:** Identificada con una muesca o punto.
        - **Pata 8:** Ubicada frente a la Pata 1 (VCC/Voltaje).
        - **Voltajes:** Estándar de 3.3V/3V; chips modernos pueden ser de **1.8V** (requieren adaptador).
- **3. Programación con CH341A (Flujo de Trabajo)**
    
    - **Detección:** Reconocimiento del chip por el software.
    - **Lectura (Read):** Visualización del contenido en hexadecimal y símbolos.
    - **Copia de Seguridad (Backup):** Guardar el binario original (.BIN o .ROM) antes de modificar.
    - **Borrado (Erase):** Limpiar el chip hasta que verifique valores en "0" o "F".
    - **Escritura (Write):** Cargar el nuevo binario compatible.
    - **Verificación:** Confirmar que los datos grabados coinciden con el archivo fuente.
- **4. Métodos de Reseteo y Mantenimiento (CMOS)**
    
    - **Pila CR2032 (3V):** Mantiene la configuración personalizada y el reloj en tiempo real.
    - **Clear CMOS:** Procedimiento para volver a valores de fábrica mediante:
        - Extracción de la pila por 10 minutos.
        - Uso de **Jumpers** (puentes) en los pines CLR_CMOS.
        - Botón dedicado en placas de gama alta.
- **5. Actualización y Recuperación Externa**
    
    - **Flash por USB:** Uso de pendrive en formato **FAT32** con el archivo renombrado según el fabricante.
    - **Botón BIOS Flashback:** Permite actualizar la BIOS sin necesidad de procesador o memoria RAM instalados.
    - **Recovery en Notebooks:** Combinación de teclas (ej. Win + B) para restaurar BIOS corruptas en marcas como HP.
- **6. Precauciones Técnicas**
    
    - **Desconexión Total:** Retirar batería, cargador, memoria RAM y pila CMOS antes de usar el programador físico.
    - **Inhibición de Pata 8:** Técnica avanzada para leer chips difíciles inhabilitando el pin de voltaje si hay conflicto en placa.