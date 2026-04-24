**Sistemas Operativos (SO): Software fundamental que actúa como intermediario entre el hardware y los programas.**

- **1. Conceptos y Funciones Principales**
    
    - **Administración de recursos:** Gestiona la memoria, el procesador, el almacenamiento y los dispositivos de entrada/salida.
    - **Interfaz de usuario:** Proporciona un entorno (intuitivo o por comandos) para interactuar con el hardware.
    - **Sistemas Embebidos:** SO integrados en chips (como la BIOS) que no dependen necesariamente de un disco para funcionar.
- **2. Tipos de Sistemas y Plataformas**
    
    - **Sistemas Comunes:** Windows, MacOS, Linux y Android.
    - **Sistemas Ligeros/Especializados:** Haiku (rapidez), ReactOS (compatible con Windows), FreeBSD (estabilidad) y Solaris (servidores).
    - **Sistemas para Proyectos:** Raspberry Pi OS (proyectos), Chrome OS (basado en la nube) y RetroOS (emulación de arcades).
- **3. El Proceso de Boot (Arranque)**
    
    - **Definición:** Proceso de encendido y carga donde la máquina busca un dispositivo para iniciar.
    - **Bootloader:** Programa encargado de encontrar y poner en marcha el sistema operativo.
    - **Kernel:** El cerebro del SO que gestiona el funcionamiento interno del hardware y software.
- **4. Medios y Herramientas de Instalación**
    
    - **Soportes físicos:**
        - **Pendrive:** Recomendado de al menos 32 GB para albergar múltiples herramientas o sistemas.
        - **Otros medios:** Tarjetas Micro SD (consolas/Raspberry), red (Internet/Ethernet en Macs) y DVD/CD (equipos antiguos).
    - **Software de creación de buteables:**
        - **Rufus:** Herramienta estándar para crear un solo arranque (Windows/Hirens).
        - **Multiboot:** Ventoy (múltiples ISOs), Yumi (ideal para Linux) y Sardu.
        - **Específicos:** Balena Etcher (para juegos/Batocera) y UNetbootin.
- **5. Arquitectura y Particionamiento**
    
    - **Esquemas de partición:**
        - **MBR (Master Boot Record):** Para sistemas antiguos (BIOS Legacy) y almacenamientos de menos de 2 TB.
        - **GPT (GUID Partition Table):** Para sistemas modernos (UEFI), soporta más particiones y más de 2 TB.
    - **Gestión por comandos (Diskpart):** Uso de `list disk`, `clean` y `convert` para formatear o cambiar esquemas de partición desde la terminal.
- **6. Virtualización**
    
    - **Software:** VirtualBox, VMware y Hyper-V.
    - **Propósito:** Crear entornos aislados para probar software, virus o desarrollar aplicaciones sin afectar al sistema host.
- **7. Errores Comunes en la Instalación**
    
    - **Configuración de BIOS:** Orden de buteo incorrecto o Secure Boot activado que impide el reconocimiento de medios.
    - **Compatibilidad:** Conflictos entre esquemas MBR/GPT o la necesidad de activar/desactivar el módulo CSM.
    - **Controladores faltantes:** Necesidad de cargar drivers específicos (RAID/IST) durante la instalación para reconocer almacenamientos NVM en placas modernas.