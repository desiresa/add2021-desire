
``````
#!/usr/bin/env ruby

puts "====================="
puts "Script    softwarectl"
puts "====================="

# Definir variables

sys = ARGV[0]
fichero = ARGV[1]

# PASO 1: Parámetro '--help'

if sys == ()
  puts "Please try 'systemctml --help' to see all comands"

#elsif para tomar mas decisiones en funcion del valor de la variable

elsif sys == '--help'
  # Leer fichero txt, con la información de help
  # 'r' solo lectura, comienza al principio del fichero
  File.open('help.txt','r') do |f1|
    while linea = f1.gets
      puts linea
    end
  end
#PASO 2: Parámetro --version
elsif sys == '--version'
    puts "*Autor: Mª Desiré Sánchez Álvarez*\n*Fecha creación: 16-02-2021*"

#PASO 3: Parámetro --status FILENAME

elsif sys == '--status'
#Leemos el fichero
  File.open('filename.txt','r') do |f1|
    while linea = f1.gets
#Que nos lo muestre por fila
      b = linea.split(":")

#Comprobar si esta instalado
        recibir = `zypper info #{b[0]} | grep Instalado |grep Sí|wc -l`.chop
#Que nos muestre si esta instalado o no
        if recibir == "1" then
          puts "Estado del paquete #{b[0]}: Instalado"
        else
          puts "Estado del paquete #{b[0]}: No instalado"
        end

    end
end

# PASO 4: Parámetro --run FILENAME
elsif sys == '--run' then
  # Comprobar si lo ejecutamos como root
  user = `whoami | grep root | wc -l`.chop
  if user == "1" then
    # Leemos el archivo filename.txt
    File.open('filename.txt','r') do |f1|
      while linea = f1.gets
        b = linea.split(":")
        if b[1].chomp == 'install' then
          # Instalar programas de filename
          system = ("zypper install -y #{b[1]}")
          puts "Instalando #{b[0]}"
        else b[1].chomp == 'remove'
          # Desinstalar programas de filename
          system = ("zypper remove #{b[1]}")
          puts "Desinstalando #{b[0]}"
        end
      end
    end
  else
    puts "[ERROR] Tienes que ser usuario root"
    exit 1
  end
end
