El archivo describe en detalle cómo fabricar un **UPS (Sistema de Potencia Ininterrumpida)** para mantener encendidos dispositivos como routers o módems durante un corte eléctrico. A continuación se listan los **materiales** necesarios y los **procedimientos técnicos** tanto para electricistas como para técnicos electrónicos basados en el contenido del documento. 

---

## Materiales necesarios

- Batería de **12 V**, puede ser:
    
    - Batería de gel
        
    - Batería de motocicleta
        
    - Batería de automóvil 
        
- **Relé** de **12 V DC**, con contactos:
    
    - Común (COM)
        
    - Normalmente Cerrado (NC)
        
    - Normalmente Abierto (NO) 
        
- **Conector DC** compatible con el módem (positivo en el pin central y negativo externo) 
    
- **Fuente de alimentación de 12 V 2 A** (el adaptador original del módem) 
    
- **Cables** rojo y negro (calibre mínimo 18 AWG) para las conexiones de potencia 
    
- **Pinzas tipo cocodrilo** grandes (para conexión flexible a baterías de diferentes tipos) 
    
- **Multímetro digital** para verificar continuidad y polaridad 
    
- **Soldador y estaño** para unir los cables 
    
- **Capacitor electrolítico** de **2200 µF / 50 V** para evitar caídas momentáneas de voltaje 
    
- **Cargador de baterías** automático de 12 V y 3 A (para recargar la batería cuando se agote) 
    
- Cinta termo-retráctil o aislante eléctrica para proteger uniones 
    

---

## Procedimiento para electricistas

1. **Verificar polaridad de la fuente**:  
    Con el multímetro, identificar el positivo (centro) y el negativo (exterior) del conector del adaptador. 
    
2. **Preparar el relé**:  
    Determinar los terminales de:
    
    - Bobina de 12 V
        
    - Contacto común (COM)
        
    - Normalmente Cerrado (NC)
        
    - Normalmente Abierto (NO) 
        
3. **Realizar las conexiones principales**:
    
    - Unir **todos los negativos** (batería, adaptador, módem) a un punto común.
        
    - El **positivo del módem** va al **común (COM)** del relé.
        
    - El **positivo del adaptador** va al **contacto normalmente abierto (NO)**.
        
    - El **positivo de la batería** va al **normalmente cerrado (NC)**. 
        
4. **Alimentar la bobina del relé**:  
    Conectar directamente a la salida de la fuente de 12 V (alimentador del módem).  
    Esto permite que el relé permanezca activado mientras haya energía eléctrica. 
    
5. **Verificar funcionamiento**:
    
    - Con energía, el relé conecta el adaptador al módem.
        
    - Sin energía, el relé cambia y conecta la batería automáticamente. 
        
6. **Agregar el capacitor**:  
    Colocar el capacitor en la entrada del módem (positivo al positivo, negativo al negativo) para evitar apagones microinterrumpidos durante el cambio de fuente. 
    

---

## Procedimiento para técnicos electrónicos

1. **Medición de continuidad y polaridad**:  
    Confirmar con el multímetro qué cable corresponde al pin interno (positivo) y cuál al externo (negativo). 
    
2. **Comprobación del relé**:  
    Alimentar la bobina y medir continuidad entre COM y NO / NC para confirmar el estado de los contactos. 
    
3. **Montaje del circuito**:
    
    - Soldar la bobina del relé a los 12 V del adaptador.
        
    - Soldar el positivo de salida del relé al módem (COM).
        
    - Unir todos los negativos con soldadura firme. 
        
4. **Prueba de activación**:  
    Medir el voltaje en la salida con adaptador conectado (≈12 V); luego desconectar para confirmar la conmutación automática a la batería (≈12.7 V). 
    
5. **Ajuste de continuidad de energía**:  
    Añadir el capacitor de 2200 µF entre positivo y negativo del módem para mantener el suministro estable durante el cambio de estado del relé. 
    
6. **Carga de batería**:  
    Usar un cargador automático que desconecte al llegar a carga completa, evitando sobrecarga. 
    

---

## Esquema lógico del UPS artesanal

- **12 V Adaptador → Relé (bobina y NO)**
    
- **Batería 12 V → Relé (NC)**
    
- **Salida COM → Módem**
    
- **Negativos todos unidos**
    
- **Capacitor paralelo en entrada del módem (2200 µF / 50 V)
    

---

Este diseño implementa un **sistema de conmutación automática** simple y económico, ideal para mantener pequeños dispositivos de red encendidos durante cortes eléctricos, sin necesidad de un inversor AC.
