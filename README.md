# Robótica- Proyecto Final

> ## Integrantes
> 
> - [Camilo Andrés Borda Gil](https://github.com/Canborda) (caabordagi@unal.edu.co)
> - [Paula Sofía Medina Diaz](https://github.com/psmedinadi22) (psmedinadi@unal.edu.co)
> - Robinson Jair Orduxz Gomez (rjorduzg@unal.edu.co)

Diseño de herramienta porta ventosa
-------


Rutina Pick and Place en RobotStudio
-----


Código RAPID
-----------------------
EL código implementado se encuentra en la carpeta RAPID, a continuación se realiza una breve descripción de las secciones principales del código.

## Main

    PROC main()
        WaitDI DI_01,1;   !Espera entrada activación digital 
        Ensamble1;        !Empieza rutina de peak and place
    ENDPROC
    PROC Ensamble1()
        Path_home;        !Va a la posicion de home
        Path_Pick2;       !Recoge pieza
        Path_Place2;      !Coloca pieza
        Path_Pick1;
        Path_Place1;
        Path_Pick3;
        Path_Place3;
        Path_Pick4;
        Path_Place4;
        Path_Pick5;
        Path_Place5;
        Path_home;        !Va a la posicion de home
    ENDPROC

## Pick

    PROC Path_Pick1()
        MoveJ Target_30,v200,z0,T_ventosa\WObj:=WO_Peak;   !movimiento articular para de posicionamiento
        MoveL Target_20,v200,z0,T_ventosa\WObj:=WO_Peak;   !movimiento lineal para acercamiento
        MoveL Target_10,v200,z0,T_ventosa\WObj:=WO_Peak;   !movimiento lineal cooredenadas de la pieza
        WaitTime 1;                                        !espera de 1s
        SetDO DO_02,0;                                     !desactiva señal para soltar
        SetDO DO_01,1;                                     !activa señal para succiónar
        WaitTime 1;                                        !espera de 1s
        MoveL Target_20,v200,z0,T_ventosa\WObj:=WO_Peak;   !movimiento lineal intermedio para alejarse
        MoveL Target_30,v200,z0,T_ventosa\WObj:=WO_Peak;   !movimiento lineal final 
   ENDPROC

## Place

```
 PROC Path_Place1()
        MoveL Target_60,v200,z0,T_ventosa\WObj:=WO_Place;   !movimiento articular para de posicionamiento
        MoveL Target_50,v200,z0,T_ventosa\WObj:=WO_Place;   !movimiento lineal para acercamiento
        MoveL Target_40,v200,z0,T_ventosa\WObj:=WO_Place;   !movimiento lineal cooredenadas de la pieza
        WaitTime 1;                                         !espera de 1s
        SetDO DO_01,0;                                      !desactiva señal para succiónar
        SetDO DO_02,1;                                      !activa señal para soltar
        WaitTime 1;                                         !espera de 1s
        MoveL Target_50,v200,z0,T_ventosa\WObj:=WO_Place;   !movimiento lineal intermedio para alejarse
        MoveL Target_60,v200,z0,T_ventosa\WObj:=WO_Place;   !movimiento lineal final 
    ENDPROC
```


Resultados
----

Para el desarrollo de este proyecto se inició verificando la conexión neumática de la ventosa, seguido fue necesario verificar el voltaje de alimentación de la ventosa e identificar con una fuente de alimentación la conexión que activa y desactiva el sistema. Como la ventosa funciona a 24V permite la conexión directa al módulo de entradas y salidas, no obstante fue necesario verificar el cableado para confirmar la tierra y la ubicación de entradas y salidas predefinidas en el controlador DI_01 DO_01 y DO_02.

---
# Conclusiones
- Al momento de diseñar un proceso de ensamble, manufactura o de cualquier indole industrial es preciso tener en cuenta cuales son los requisitos y limitaciones tanto de espacio, dispositivo como a tareas a realizar, pues son estas las que definirán los diseños desde herramientas hasta los procesos mismos.

- Para la rutina desarrollada y el peso de cada pieza se evidenció que es posible optimizar la trayectoria, particularmente la velocidad de desplazamiento de entre los espacios de trabajo reduciendo el tiempo de ensamble del mecanismo.

- Para aplicaciones de pick and place es indispensable definir adecuadamente la orientación de los targets pues en este tipo de rutinas la precisión resulta muy importante a la hora ensamblar partes. También es importante resaltar que al realizar rutinas de pick la ventosa no debe acercarse y tocar la pieza de forma abrupta pues puede desplazar la pieza a sujetar y llegado el caso también piezas aledañas a esta, por tanto para este ejercicio se tomo un espacio entre la ventosa y el ensamble de un centímetro para que la ventosa se acercase.

- Si bien crear los espacios de pick and place de manera separada hace que en entornos industriales los procesos sean mas versátiles y flexibles al tener la capacidad y posibilidad de mover las diferentes estaciones a conveniencia, para este ejercicio académico haber tenido los espacios de pick and place en una sola estación hubiera facilitado el proceso al disminuir un proceso de calibración de un workspace extra.

- De cara a evitar singularidades es importante evitar en la mayor medida trayectorias que impliquen desplazamientos lineales que produzcan movimientos considerables en las articulaciones, y para esto se debe hacer una correcta planeación que va desde la disposición y orientación de cada uno de los elementos a ensamblar hasta la misma ubicación de las estaciones de trabajo.


---
# Referencias

- Laboratorio 5 - Cinemática Inversa - Robot Phantom X - ROS
- Apuntes de clase, Robótica 2023-1

---
