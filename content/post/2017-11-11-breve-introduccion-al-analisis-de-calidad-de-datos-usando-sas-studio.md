---
title: Breve Introducción al Análisis de Calidad de Datos usando SAS Studio
author: Alberto Negron
date: '2017-11-11'
slug: breve-introduccion-al-analisis-de-calidad-de-datos-usando-sas-studio
categories:
  - SAS
tags:
  - DQ
description: ''
featured: ''
featuredalt: ''
featuredpath: ''
linktitle: ''
---


>"Data is the new oil." Clive Humby

El británico *Clive Humby*  tenía la visión muy clara de hacia donde se dirijía la tendencia digital cuando en el 2006 acuño la frase **Los datos son el nuevo petróleo**.

En 2017, está frase sigue tan o más vigente que nunca. Vivimos en la era del *Big Data* donde casi cualquier dispositivo con el que interactuamos esta conectado a Internet generando datos a cada segundo (móviles, tabletas, laptops, televisores inteligentes, relojes, compañías por cable, accesorios deportivos, etc).

Los datos convertidos en información ha pasado de ser un recurso más en las empresas a convertirse en el recurso más importante. Las empresas están invirtiendo cientos de millones de dólares al año en tecnologías y procesos que les permitan recolectar y gestionar toda esta data que viene en una gran variedad de formatos y frecuencias.

De allí la suprema importancia de la calidad de los datos. Pero, ¿qué es calidad de datos? La calidad de datos son los estándares definidos por cada empresa o sector (farmacéutico, financiero, gas y petróleo, comercio, etc) para asegurar que la data que está almancenada en sus sistemas de información es veraz y oportuna.

Existe un marco teórico de calidad de datos que se usa como punto de partida pero que posteriormente es personalizado a los requerimientos de cada empresa. Los estándares de calidad de datos en el sector farmacéutico son distintos a los de una entidad financiera por ejemplo.

Algunos ejemplos prácticos de calidad de datos son:

- Eliminar registros duplicados. Imagínense por un momento, una empresa de ventas por catálogos que tiene clientes duplicados en su base datos y que a cada cliente le llegue 2 ó más catálogos. Pérdida de dinero y confianza.
- Asegurarse que no llamemos "Sr." a María Laura o "Srta." a Pedro Fernandez.
- Que valores de un indicador estén dentro de un rango acceptable de valores. Piensen en alguien con -1 año de edad o que nació el 13 de Enero de 1598 y compró un reloj online hace 2 días.
- Asegurarse que los datos que se cargan en un proceso ETL tengan el formato correcto. Imaginen un archivo CSV que generalmente viene con la edad de un usuario en la segunda columna y que en una actualización del archivo la columna 2 posee el salario.

Se puede decir que los ejemplos sobre reglas para validar la calidad de los datos son un conjunto finito no numberable!

Pasemos al ejemplo práctico con SAS. El siguiente código es bastante sencillo que tiene como objetivo mostrar como con una pocas líneas de código se pueden hacer cosas muy interesantes con SAS y el tema de la calidad de los datos.

Es un ejemplo muy sencillo pero que espero les sirva para evaluar el poder de SAS.

No los quiero aburrir mucho más con una lectura larga de la lógica detrás del código. Para eso he creado un vídeo en mi canal de Youtube donde hago una explicación exhaustiva.

Link del vídeo [aquí](https://youtu.be/KVLh2-G5zv0)



En el siguiente ejemplo he creado una data artificial sobre 5 pacientes. Esta data contiene información sobre el nombre del paciente y ciertos indicadores sobre su estado de salud. Seguidamente le vamos a aplicar unas reglas muy sencillas de calidad datos para validar la veracidad de la información.

```
libname valido "/folders/myshortcuts/sas/data/proj003_dq/validos";
libname invalido "/folders/myshortcuts/sas/data/proj003_dq/invalidos";


data work.pacientes;
infile datalines delimiter=",";
length pat_no $5 nombre $50 sexo $1 ritmo 3. presion_sis 3.  presion_dia 3.  cod_diag $5 ;
input pat_no $ nombre $ sexo $ ritmo  presion_sis  presion_dia  cod_diag $ ;
label pat_no = '# Paciente'
      nombre = 'Nombre Paciente'
      sexo   = 'Sexo'
      ritmo  = 'Ritmo Cardíaco'
      presion_sis = 'Presión Arterial (Sistólica)'
      presion_dia = 'Presión Arterial (Diastólica)'
      cod_diag    = 'Código Diagnóstico';
datalines;
00025,Jhon Bishop,M,90,125,70,123
00A23,Carlos Ortega,M,500,130,65,125
03123,Adriana Perez,2,45,210,50,ABC
03122,Violeta Chamorros,f,60,120,83,23
00025,Luis Moretti,M,97,115,79,9239
;
proc print label; run;
```

Las reglas de calidad de datos son muy sencillas:

```

**** Reglas de Calidad de Datos ************
pat_no: Sólo acepta números
nombre: al menos 2 palabras (nombre y Apellido)
sexo: "M" o "F"
ritmo: Valores entre 40 y 100 
presion_sis: Valores entre 80 y 200  
presion_dia: Valores entre 60 y 120  
cod_diag: entre 1 y 3 digitos
*********************************************;

data  valido.pacientes(drop=dq: tot:) invalido.dq_pacientes;
  set work.pacientes;
dq_patno  = (verify(pat_no,'0123456789'))>0;
dq_nombre = countw(nombre) < 2;
dq_sexo   = sexo not in ('M','F');
dq_ritmo  = abs((40<=ritmo<=100) - 1); 
dq_sis    = abs((80<=presion_sis<=200) - 1); 
dq_dia    = abs((60<=presion_dia<=120) - 1); 
dq_cod	  = anyalpha(cod_diag) or length(cod_diag)>3 or missing(cod_diag);
tot_dq_r  = sum(of dq_:);
dq_vector = cats(dq_patno,dq_nombre,dq_sexo,dq_ritmo,dq_sis,dq_dia,dq_cod);
if tot_dq_r > 0 then output invalido.dq_pacientes;
 else output valido.pacientes;
run;
```

Espero que hayan encontrado el post útil.

SASludos,