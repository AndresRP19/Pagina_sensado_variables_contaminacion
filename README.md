# Pagina_sensado_variables_contaminacion
#CODIGO PYTHON para generar las lecturas de los sensores

import mysql.connector
import random
from datetime import datetime

def current_date_format(date):
    months = ("Enero", "Febrero", "Marzo", "Abri", "Mayo", "Junio",
     "Julio", "Agosto", "Septiembre", "Octubre", "Noviembre", "Diciembre")
    day = date.day
    month = months[date.month - 1]
    year = date.year
    messsage = "{} de {} del {}".format(day, month, year)

    return messsage

now = datetime.now()
format = now.strftime('%H:%M:%S')

conexion1=mysql.connector.connect(host="localhost",
                                  user="root",
                                  passwd="CONTRASEÑA",
                                  database="datos_sensado")
cursor1=conexion1.cursor()
sql="insert into variables(co, co2,tolueno,nh4,nodo,fecha,hora) values (%s,%s,%s,%s,%s,%s,%s)"
datos=(random.randint(200,2000),random.randint(0,5000),random.randint(1,50),
random.randint(0,100),"nodo 1",current_date_format(now),format)
cursor1.execute(sql, datos)
datos=(random.randint(200,2000),random.randint(0,5000),random.randint(1,50),
random.randint(0,100),"nodo 2",current_date_format(now),format)
cursor1.execute(sql, datos)
conexion1.commit()
conexion1.close()
