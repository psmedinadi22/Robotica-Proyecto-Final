# Robotica Proyecto Final

> ## Integrantes
> 
> - [Camilo Andrés Borda Gil](https://github.com/Canborda) (caabordagi@unal.edu.co)
> - [Paula Sofía Medina Diaz](https://github.com/psmedinadi22) (psmedinadi@unal.edu.co)
> - Robinson Jair Orduxz Gomez (rjorduzg@unal.edu.co)

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
