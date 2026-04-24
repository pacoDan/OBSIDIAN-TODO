
# 🥇 1. **`pdftk` (PDF Toolkit)** — el más clásico

Es una herramienta de línea de comandos para manipular PDFs: unir, dividir, rotar, cifrar, etc. ([Linux Command Library](https://linuxcommandlibrary.com/man/pdftk?utm_source=chatgpt.com "pdftk man | Linux Command Library"))

### Instalar

**Linux (Ubuntu / Debian)**

```bash
sudo apt install pdftk
```

o versión moderna:

```bash
sudo apt install pdftk-java
```

**Windows**

Descargar el binario o usar `pdftk-java`.

---

### Unir PDFs

```bash
pdftk archivo1.pdf archivo2.pdf cat output combinado.pdf
```

### Unir muchos PDFs

```bash
pdftk *.pdf cat output combinado.pdf
```

---

# 🥈 2. **`pdfunite` (muy simple y rápido)**

Es parte de **poppler-utils** y sirve específicamente para **fusionar PDFs**. ([Linux Command Library](https://linuxcommandlibrary.com/man/pdfunite?utm_source=chatgpt.com "pdfunite man | Linux Command Library"))

### Instalar

```bash
sudo apt install poppler-utils
```

### Usar

```bash
pdfunite archivo1.pdf archivo2.pdf salida.pdf
```

### Combinar muchos

```bash
pdfunite *.pdf combinado.pdf
```

Ventaja:

- Muy simple
    
- Muy rápido
    
- Viene en muchas distros Linux
    

Limitación:

- No permite elegir páginas específicas.
    

---

# 🥉 3. **`qpdf` (muy potente)**

Herramienta open source para manipular la estructura de PDFs: unir, dividir, cifrar, optimizar. ([Wikipedia](https://en.wikipedia.org/wiki/QPDF?utm_source=chatgpt.com "QPDF"))

### Instalar

Linux:

```bash
sudo apt install qpdf
```

Windows:

```bash
choco install qpdf
```

### Unir PDFs

```bash
qpdf --empty --pages file1.pdf file2.pdf -- merged.pdf
```

---

# 🧠 4. Usar **Ghostscript** (muy universal)

```bash
gs -q -dBATCH -dNOPAUSE -sDEVICE=pdfwrite -sOutputFile=merged.pdf file1.pdf file2.pdf
```

Funciona en:

- Linux
    
- Windows
    
- macOS
    

([CPU Killer](https://www.cpukiller.com/linux/linux-merge-pdf/?utm_source=chatgpt.com "Linux Merge Pdf - CPU Killer"))

---

# ⭐ Recomendación práctica

Para terminal yo recomiendo:

|herramienta|dificultad|potencia|
|---|---|---|
|**pdfunite**|muy fácil|básica|
|**pdftk**|fácil|muy potente|
|**qpdf**|media|muy potente|
|**ghostscript**|media|muy flexible|

---

# 🚀 Comando más simple de todos

Si solo querés unir PDFs:

```bash
pdfunite *.pdf resultado.pdf
```

---

✅ **Conclusión:**  
Las mejores herramientas open-source para unir PDFs desde terminal son:

- **pdftk**
    
- **pdfunite**
    
- **qpdf**
    
- **ghostscript**
    

---

💡 Si querés, también puedo darte **un script de 3 líneas para unir cientos de PDFs automáticamente en Linux o Windows**, algo que se usa mucho en servidores o automatización.