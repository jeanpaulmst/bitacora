# Scripting: que el servidor se revise solo

### 1. El esqueleto que devuelve un número

Creo el archivo healthcheck.sh y lo corro

`sudo /usr/local/bin/healthcheck.sh ; echo "salió con: $?"`

lo que me devuelve `salió con: 0` indicando que no hubo error en la ejecucion y que el sistema esta trabajando por debajo del umbral que definimos

Luego al correr `cat /var/log/healthcheck.log` la consola imprime `2026-09-23 16:41:01 srv1 OK disco=11%`

AL ejecutar `sudo env UMBRAL_DISCO=1 /usr/local/bin/healthcheck.sh ; echo "salió con: $?"`, la salida indica: `salió con: 1`

### 2. Que revise algo más que el disco

agregamos las siguientes funciones para que verifique tambien el uso de memoria ram y si ssh esta escuchando en el puerto 22:

```
uso_mem() {
    free | awk '/^Mem:/ {printf "%d", $3*100/$2}'
}
ssh_escucha() {
    ss -tln | grep -qE '[:.]22[[:space:]]'
}
```

Una vez le agregamos verificaciones para la memoria y ssh, el nuevo log se ve así:

```
2026-09-23 16:41:01 srv1 OK disco=11%
2026-09-23 16:43:08 srv1 OK disco=11%
2026-09-23 16:43:57 srv1 OK disco=11%
2026-09-23 16:45:07 srv1 ALERTA disco=11%
2026-09-23 16:56:43 srv1 OK disco=11% mem=11% ssh22=si
```

### 3. shellcheck: que lo revise alguien más

El comando es shellcheck (con doble "l"). Es un analizador estático para scripts de shell: lee el script sin ejecutarlo y te avisa de errores y malas prácticas antes de que te causen problemas.

Corriendolo en mi propio archio `healthcheck.sh`la salida es limpia, indicando que no hay errores en el archivo

### 4. Que corra solo, con cron

Configuro el cron job con un tiempo de 5 minutos y con la ejecucion del usuario root:
`*/5 * * * * root /usr/local/bin/healthcheck.sh`

Luego miro la salida del log, donde se imprime:

```
2026-09-23 16:41:01 srv1 OK disco=11%
2026-09-23 16:43:08 srv1 OK disco=11%
2026-09-23 16:43:57 srv1 OK disco=11%
2026-09-23 16:45:07 srv1 ALERTA disco=11%
2026-09-23 16:56:43 srv1 OK disco=11% mem=11% ssh22=si
2026-09-23 17:10:01 srv1 OK disco=11% mem=11% ssh22=si
2026-09-23 17:15:01 srv1 OK disco=11% mem=11% ssh22=si
```

Esto indica que funciona bien ya que se ejecuta cada el tiempo definido

### 5. Lo mismo con systemd

Otra herramienta que se puede utilizar para tareas programadas es el mismo systemd. A traves de una tabla de timers

```
sysadmin@srv1:/var/log$ systemctl list-timers healthcheck.timer
NEXT                    LEFT     LAST                    PASSED      UNIT              ACTIVATES
Wed 2026-09-23 17:26:3… 58s left Wed 2026-09-23 17:21:3… 4min 1s ago healthcheck.timer healthcheck.service

1 timers listed.
```
