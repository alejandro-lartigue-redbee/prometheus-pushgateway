# Prometheus-Pushgateway
Basado en capítulos 9 y 10 de: https://testautomationu.applitools.com/observability-for-test-automation/

#### Requisitos 
Tener instalados `docker` y `docker-compose`
<blockquote>
Instalar de docker: https://docs.docker.com/engine/install/<br> 
Intalar docker-compose: https://docs.docker.com/compose/install/
</blockquote>

#### Proyecto:
- <b>Carpeta prometheus</b>: contiene la configuración de prometheus que es levantada automáticamente por el docker. Es un copy paste de la configuración default, más el agregado de las `scrape_configs`
- <b>docker-compose.yaml:</b>: Usado para ejecutar los docker y su comunicación  

#### ¿Cómo agregar métricas usando el PushGateway?
1. Run dockers de Prometheus y Pushgateway con el comando:
`docker-compose up`

<blockquote> 
En caso de no existir las imágenes localmente, se van descargar lo que puede demorar la primera ejecución</blockquote>

2. Enviar métricas al pushgateway usando mediante la api:  
```
echo "some_metric 3.14" | 
curl --data-binary @- http://pushgateway.example.org:9091/metrics/job/some_job
```
<blockquote> 
Docs de API de PushGateway: https://github.com/prometheus/pushgateway 
</blockquote>

3. Verificar la métricas en Pusgateway ingresando a `http:localhost:9091/`

4. Verificar la métricas en Prometheus ingresando a `http:localhost:9090/`

#### Modelo de Métrica  
Las métricas tienen el siguiente formato:
`<metric name>{<label name>=<label value> <metric value></metric>}`

<blockquote>
Docs de Métricas: https://prometheus.io/docs/concepts/data_model/ <br> 
Buenas prácticas de Métricas: https://prometheus.io/docs/practices/naming/
</blockquote>
 
#### Más información
Precauciones al usar pushgateway: https://prometheus.io/docs/practices/pushing/  
¿Qué es Prometheus y para que se usa?: https://www.metricfire.com/blog/what-is-prometheus-use-cases/#bWhat-Are-the-Use-Cases-of-Prometheusb    
¿Qué es Prometheus Pushgateway?:  https://www.metricfire.com/blog/what-is-prometheus-pushgateway/
¿Cómo trabajan juntos Prometheus y Prometheus Pushgateway?: https://testautomationu.applitools.com/observability-for-test-automation/    

