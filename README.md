# Environmental Toolkit

## Components

Actualmente el proyecto está compuesto por dos servicios desplegados a través de Helm.

- NGSI Timeseries API (QuantumLeap) is the first implementation of an API that supports the storage of FIWARE NGSIv2
  data
  into a time series database. It currently also experimentally supports the injection of NGSI-LD in a backward
  compatible way with NGSI-v2 API. I.e. you can retrieve NGSI-LD stored data via NGSI v2 API and retrieve data will be
  describe following NGSI v2 format.

- Grafana open source software enables you to query, visualize, alert on, and explore your metrics, logs, and traces
  wherever they are stored. Grafana OSS provides you with tools to turn your time-series database (TSDB) data into
  insightful graphs and visualizations.

## Install

### Quantumleap

Para la correcta instalación del Quantumleap es necesario aprovisionar correctamente la base de datos Timescale donde se
almacenarán los valores de series temporales. Con este motivo se aconseja ejecutar en dos ocasiones los Charts con Helm.
En la primera ocasión con los init-container habilitados y en la segunda deshabilitados.

To install the chart with the release name `quantumleap`:

```console
$ helm dependency up quantumleap/chart/
$ helm install quantumleap quantumleap/chart/
```

### Grafana

To install the chart with the release name `grafana`:

```console
$ helm dependency up grafana/chart/
$ helm install grafana grafana/chart/
```

## TODO
- Mejorar documentación
- Probar tests
- Encontrar mejor solución para Quantumleap → init-container with code 64
- Crear un usuario grafana para la base de datos de Quantumleap 
- Despliegue mediante Gitlab CI/CD

## License

for the ODALA project.

© 2022 HOPU

License EUPL 1.2

![](https://ec.europa.eu/inea/sites/default/files/ceflogos/en_horizontal_cef_logo_2.png)
