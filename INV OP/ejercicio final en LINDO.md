```txt
max z) 2 x1 + 5 x2 +3 x3
st
MO) 3 x1 + 5 x2 + 2 x3 < 650
MP) 7 x1 + 4 x2 + 3 x3 < 420
demanda) x1 + x2 + x3 > 130
end
```
resultado:
```txt
 LP OPTIMUM FOUND AT STEP      3
        OBJECTIVE FUNCTION VALUE
        Z)      450.0000
  VARIABLE        VALUE          REDUCED COST
        X1         0.000000          9.000000
        X2        30.000000          0.000000
        X3       100.000000          0.000000
        
       ROW   SLACK OR SURPLUS     DUAL PRICES
       MO)       300.000000          0.000000
       MP)         0.000000          2.000000
  DEMANDA)         0.000000         -3.000000

 NO. ITERATIONS=       3

 RANGES IN WHICH THE BASIS IS UNCHANGED:
                           OBJ COEFFICIENT RANGES
 VARIABLE         CURRENT        ALLOWABLE        ALLOWABLE
                   COEF          INCREASE         DECREASE
       X1        2.000000         9.000000         INFINITY
       X2        5.000000         INFINITY         1.000000
       X3        3.000000         0.750000         INFINITY

                           RIGHTHAND SIDE RANGES
      ROW         CURRENT        ALLOWABLE        ALLOWABLE
                    RHS          INCREASE         DECREASE
       MO      650.000000         INFINITY       300.000000
       MP      420.000000       100.000000        30.000000
  DEMANDA      130.000000        10.000000        25.000000
```
su dual:
```txt
min z) 650 y1 + 420 y2 - 130 y3
st
R1) 3 y1 + 7 y2 - y3 > 2
R2) 5 y1 + 4 y2 - y3 > 5 
R5) 2 y1 + 3 y2 - y3 > 3
end
```
la solución dual:
```txt
 LP OPTIMUM FOUND AT STEP      1
        OBJECTIVE FUNCTION VALUE
        Z)      450.0000
  VARIABLE        VALUE          REDUCED COST
        Y1         0.000000        300.000000
        Y2         2.000000          0.000000
        Y3         3.000000          0.000000
        
       ROW   SLACK OR SURPLUS     DUAL PRICES
       R1)         9.000000          0.000000
       R2)         0.000000        -30.000000
       R5)         0.000000       -100.000000

 NO. ITERATIONS=       1

 RANGES IN WHICH THE BASIS IS UNCHANGED:
                           OBJ COEFFICIENT RANGES
 VARIABLE         CURRENT        ALLOWABLE        ALLOWABLE
                   COEF          INCREASE         DECREASE
       Y1      650.000000         INFINITY       300.000000
       Y2      420.000000       100.000000        30.000000
       Y3     -130.000000        25.000000        10.000000
       
                           RIGHTHAND SIDE RANGES
      ROW         CURRENT        ALLOWABLE        ALLOWABLE
                    RHS          INCREASE         DECREASE
       R1        2.000000         9.000000         INFINITY
       R2        5.000000         INFINITY         1.000000
       R5        3.000000         0.750000         INFINITY
```

ahora le cambio el signo multiplicando -1 a la demanda
```txt
max z) 2 x1 + 5 x2 +3 x3
st
MO) 3 x1 + 5 x2 + 2 x3 < 650
MP) 7 x1 + 4 x2 + 3 x3 < 420
demanda) - x1 - x2 - x3 < - 130
end
```
```txt
 LP OPTIMUM FOUND AT STEP      1
        OBJECTIVE FUNCTION VALUE
        Z)      450.0000

  VARIABLE        VALUE          REDUCED COST
        X1         0.000000          9.000000
        X2        30.000000          0.000000
        X3       100.000000          0.000000

       ROW   SLACK OR SURPLUS     DUAL PRICES
       MO)       300.000000          0.000000
       MP)         0.000000          2.000000
  DEMANDA)         0.000000          3.000000

 NO. ITERATIONS=       1

 RANGES IN WHICH THE BASIS IS UNCHANGED:

                           OBJ COEFFICIENT RANGES
 VARIABLE         CURRENT        ALLOWABLE        ALLOWABLE
                   COEF          INCREASE         DECREASE
       X1        2.000000         9.000000         INFINITY
       X2        5.000000         INFINITY         1.000000
       X3        3.000000         0.750000         INFINITY

                           RIGHTHAND SIDE RANGES
      ROW         CURRENT        ALLOWABLE        ALLOWABLE
                    RHS          INCREASE         DECREASE
       MO      650.000000         INFINITY       300.000000
       MP      420.000000       100.000000        30.000000
  DEMANDA     -130.000000        25.000000        10.000000
```
---
bajo la cantidad demandada de 130 a 125
```txt
max z) 2 x1 + 5 x2 +3 x3
st
MO) 3 x1 + 5 x2 + 2 x3 < 650
MP) 7 x1 + 4 x2 + 3 x3 < 420
demanda) x1 + x2 + x3 > 125
end
```
y AUMENTA EL funcional Z
```txt
 LP OPTIMUM FOUND AT STEP      0
        OBJECTIVE FUNCTION VALUE
        Z)      465.0000
  VARIABLE        VALUE          REDUCED COST
        X1         0.000000          9.000000
        X2        45.000000          0.000000
        X3        80.000000          0.000000

       ROW   SLACK OR SURPLUS     DUAL PRICES
       MO)       265.000000          0.000000
       MP)         0.000000          2.000000
  DEMANDA)         0.000000         -3.000000

 NO. ITERATIONS=       0

 RANGES IN WHICH THE BASIS IS UNCHANGED:

                           OBJ COEFFICIENT RANGES
 VARIABLE         CURRENT        ALLOWABLE        ALLOWABLE
                   COEF          INCREASE         DECREASE
       X1        2.000000         9.000000         INFINITY
       X2        5.000000         INFINITY         1.000000
       X3        3.000000         0.750000         INFINITY

                           RIGHTHAND SIDE RANGES
      ROW         CURRENT        ALLOWABLE        ALLOWABLE
                    RHS          INCREASE         DECREASE
       MO      650.000000         INFINITY       265.000000
       MP      420.000000        80.000000        45.000000
  DEMANDA      125.000000        15.000000        20.000000
```