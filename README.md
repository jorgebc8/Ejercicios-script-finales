# ejercicios-scripts-Linux


## Script 1: 
#### Escriba un script que elimine un archivo o directorio pasado como parámetro, y le pregunte si está seguro de llevar a cabo la acción.
~~~~
#!/bin/bash


clear

if [[ -e $1 ]]; then
	if [[ -d $1 ]]; then
			read -p "¿Está seguro que quiere borrar el directorio $1? (S/N): " opcion
			if [[ $opcion == "s" || $opcion == "S" ]]; then
				rm -r $1
			fi
			
	else

			read -p "¿Está seguro que quiere borrar el fichero $1? (S/N): " opcion
			if [[ $opcion == "s" || $opcion == "S" ]]; then
				rm $1
			fi
	fi	
else
	echo "No existe el directorio o fichero introducido."
fi
~~~~

## Script 2: 
#### Escribir un script que pueda mostrar información de un comando al ejecutar dicho script y pasar como parámetro el comando.
~~~~
#!/bin/bash


clear
$1 --help
~~~~

## Script 3: 
#### Realiza un script que compruebe si el usuario actual del sistema es blas, si es así visualiza su nombre 5 veces, sino te despides de él amigablemente.
~~~~
#!/bin/bash

clear

USUARIO=$(whoami)

if [[ $USUARIO == blas ]]; then
	echo $USUARIO
	echo $USUARIO
	echo $USUARIO
	echo $USUARIO
	echo $USUARIO
else
	echo "Hasta luego, $USUARIO."
fi
~~~~

## Script 4: 
#### En un fichero tengo una palabra clave. Haz un script que muestre si dicha palabra es el parámetro pasado o no.
~~~~
#!/bin/bash


clear

#te crea el fichero clave si no existe
if [[ ! -e ficheroclave.txt ]]; then
	$(echo "jamon" > ficheroclave.txt)
fi

clave=$(cat ficheroclave.txt)

if [[ $clave == $1 ]]; then
	echo "¡Has acertado, la palabra era $1!"
else
	echo "No has acertado, prueba otra vez..."
fi
~~~~

## Script 5: 
#### Tenemos un menu principal: (1) Suma: Lee dos numeros y los suma. (2) Resta. (3) Multiplicación. (4) Salir:Termina el script.
~~~~
#!/bin/bash


clear

read -p "Introduce: 
1/Suma | 2/Resta | 3/Multiplicación | 4/Salir: " opcion

case $opcion in
	1)  read -p "Primer número: " n1
		read -p "Segundo número: " n2
		suma=$(($n1 + $n2))
		echo "$n1 + $n2 = $suma"
	;;

	2)  read -p "Primer número: " n1
		read -p "Segundo número: " n2
		resta=$(($n1 - $n2))
		echo "$n1 - $n2 = $resta"
	;;

	3)  read -p "Primer número: " n1
		read -p "Segundo número: " n2
		multi=$(($n1 * $n2))
		echo "$n1 * $n2 = $multi"
	;;

	*) exit 0
esac
~~~~

## Script 6: 
#### Nos pide la edad y nos dice si es mayor de edad o menor.
~~~~
#!/bin/bash


clear

read -p "Introduce tu edad: " edad

if [[ $edad -ge 18 ]]; then
	echo "Eres mayor de edad."
else
	echo "Eres menor de edad."
fi
~~~~

## Script 7: 
#### Script que reciba un nombre de fichero, verifique que existe y que es un fichero de lectura-escritura, lo convierta en ejecutable para el usuario y el grupo y muestre el estado final de los permisos.
~~~~
#!/bin/bash


clear

if [[ ! -f $1 ]]; then
	read -p "El fichero no existe o es un directorio.

¿Desea crear el fichero $1? S/N: " opcion
	if [[ $opcion == "S" || $opcion == "s" ]]; then
		echo > $1
	fi
elif [[ -r $1 && -w $1 ]]; then
	echo "Tiene permisos de lectura y escritura."
		chmod ug+x $1
		ls -l $1
	else
		echo "El fichero no tiene permisos de lectura-escritura."
fi
~~~~

## Script 8: 
#### Script que nos diga al pulsar una tecla, si es letra, numero o caracter especial.
~~~~
#!/bin/bash


clear

while true; do
	read -rsn1 entrada
	if [[ "$entrada" = [0-9] ]]; then
		echo "Ha introducido el número: $entrada"
	elif [[ "$entrada" = [a-z,A-Z] ]]; then
		echo "Ha introducido la letra: $entrada"
	else
		echo "Ha introducido el caracter especial: $entrada"
	fi
done
~~~~

## Script 9: 
#### Realizar un script que reciba varios parametros y nos diga cuantos de esos parametros son de directorios y cuantos son archivos. $# contador que indica cuantos parametros se pasan.
~~~~
#!/bin/bash



clear

contadorDirectorios=0
contadorFicheros=0
for i in $@; do
	if [[ -d $i ]]; then
		contadorDirectorios=$(($contadorDirectorios+1))

	elif [[ -f $i ]]; then
		contadorFicheros=$(($contadorFicheros+1))
	fi
done

echo "Número de directorios: $contadorDirectorios"
echo "Número de ficheros: $contadorFicheros"
~~~~

## Script 10: 
#### Mostramos menu, con productos para vender, luego nos pide que introduzcamos la opcion. luego mensaje que indica que introduzca moneda. Si ponemos precio exacto nos da mensaje, "Gracias buen provecho", si ponemos menos, nos diga falta. Si poner mas valor, nos indique el cambio con mensaje.
~~~~
#!/bin/bash



clear

read -p "Productos a la venta:
1) KitKat: 4€
2) Donetes: 2€
3) Cereales: 1€
4) Salir
Introduzca el producto que desea comprar: " opcion


case $opcion in
	 1) read -p "Introduce los 4 euros: " dinero
		if [[ $dinero = 4 ]]; then
			echo "Gracias buen provecho."
		elif [[ $dinero -gt 4 ]]; then
			echo "El cambio: "$((dinero - 4))
		elif [[ $dinero -lt 4 ]]; then
			echo "Falta dinero."
		fi
		;;

	 2) read -p "Introduce los 2 euros: " dinero
		if [[ $dinero = 2 ]]; then
			echo "Gracias buen provecho."
		elif [[ $dinero -gt 2 ]]; then
			echo "El cambio: "$((dinero - 2))
		elif [[ $dinero -lt 2 ]]; then
			echo "Falta dinero."
		fi
		;;

	 3) read -p "Introduce los 1 euro: " dinero
		if [[ $dinero = 1 ]]; then
			echo "Gracias buen provecho."
		elif [[ $dinero -gt 1 ]]; then
			echo "El cambio: "$((dinero - 1))
		elif [[ $dinero -lt 1 ]]; then
			echo "Falta dinero."
		fi
		;;
		
	 *) exit 0
		;;
		
esac
~~~~

## Script 11: 
#### Realizar un script que pida introducir la ruta de un directorio por teclado (Hay que validar que la variable introducida sea un directorio) nos diga cuantos archivos y cuantos directorios hay dentro de ese directorio.
~~~~
#!/bin/bash



clear

read -p "Introduzca la ruta del directorio: " directorio

contadorDirectorios=$(find $directorio/* -type f | wc -l)
contadorFicheros=$(find $directorio/* -type d | wc -l)

echo "Dentro del directorio hay $contadorDirectorios directorios y $contadorFicheros ficheros."
~~~~

## Script 12: 
#### Realiza un script que introduzca número por parámetro y muestre tabla de multiplicar.
~~~~
#!/bin/bash


clear

echo "La tabla de multiplicar del $1 es: "

for (( i = 1; i <= 10; i++ )); do
	resultado=$(($1 * $i))
	echo "$1 * $i = $resultado"
done
~~~~

## Script 13: 
#### Script que limpie todas las reglas, y de permiso a todas las conexiones.
~~~~
#! /bin/bash


clear

#limpia las reglas
iptables -t nat -F
iptables -t mangle -F
iptables -F
iptables -X
iptables -Z

#permite conexiones
iptables -P INPUT ACCEPT
iptables -P OUTPUT ACCEPT
iptables -P FORWARD ACCEPT
iptables -I INPUT -j ACCEPT
~~~~

## Script 14: 
#### Script que limpie todas las reglas, y prohíba cualquier conexión.
~~~~
#!/bin/bash


clear

#limpia las reglas
iptables -t nat -F
iptables -t mangle -F
iptables -F
iptables -X
iptables -Z

#permite conexiones
iptables -P INPUT DROP
iptables -P OUTPUT DROP
iptables -P FORWARD DROP
iptables -I INPUT -j DROP
~~~~

## Script 15: 
#### Tendrá 3 parámetros: red(ip), entrada-salida, aceptar-denegar. Dará estos permisos a iptables.
~~~~
#!/bin/bash


clear

if [[ $2 == "entrada" ]]; then
	if [[ $3 == "aceptar" ]]; then
		iptables -A INPUT -s $1 -j ACCEPT
		echo "entrada aceptar"
	elif [[ $3 == "denegar" ]]; then
		iptables -A INPUT -s $1 -j DROP
		echo "entrada denegar"
	fi

elif [[ $2 == "salida" ]]; then
	if [[ $3 == "aceptar" ]]; then
		iptables -A INPUT -s $1 -j ACCEPT
		echo "salida aceptar"
	elif [[ $3 == "denegar" ]]; then
		iptables -A INPUT -s $1 -j DROP
		echo "salida denegar"
	fi
fi

~~~~
