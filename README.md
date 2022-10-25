# Environmental Toolkit

## Components

The project currently consists of three services deployed through Helm:

- NGSI Timeseries API (QuantumLeap) is the first implementation of an API that supports the storage of FIWARE NGSIv2
  data into a time series database. It currently also experimentally supports the injection of NGSI-LD in a backward
  compatible way with NGSI-v2 API. I.e. you can retrieve NGSI-LD stored data via NGSI v2 API and retrieve data will be
  describe following NGSI v2 format.

- Grafana open source software enables you to query, visualize, alert on, and explore your metrics, logs, and traces
  wherever they are stored. Grafana OSS provides you with tools to turn your time-series database (TSDB) data into
  insightful graphs and visualizations.

- Air Quality App provides a set of Grafana dashboards that allows knowing the air quality status of a city.

## Install

### Quantumleap

To correctly install Quantumleap, it is necessary to correctly provision the Timescale database where the time series
values will be stored.
Time-series values will be stored. For this reason, it is advisable to run Charts with Helm twice.
The first time with the init-container enabled and the second time with the init-container disabled.

To install the chart with the release name `quantumleap`:

```console
$ helm dependency up quantumleap/chart/
$ helm install quantumleap quantumleap/chart/
```

#### First installation - Two steps installation

First, running the `helm dependency up quantumleap/chart/` command is necessary to ensure that the base chart is
downloaded.

- **Enable init-container**

  If this is the first time quantumleap is installed, it must be deployed with init-container enabled. This
  init-container will ensure the necessary database provisioning so that the communication between quantumleap and the
  time series database, Timescale, in this case, works correctly.
  quantumleap and the time series database, Timescale, in this case, to work correctly.
  Init-container will generate a quantumleap database in Timescale and assign the appropriate permissions and roles.

  To enable the init-container, the following parameter in the values.yaml file must be set to `true`:

  ```yaml
  quantumleap:
    ...
    init:
      enabled: true
    ...
  ```

  To install quantumleap, run the following command:

  ```console
  $ helm install quantumleap quantumleap/chart/
  ```

  > **Notice**: If the execution of the init-container finishes successfully, it returns a response code 64. Kubernetes
  interprets this code as a failure forcing a loop of restarts. For this reason, it is necessary to launch the service
  with the init-container disabled once it has been possible to confirm that the init-container has completed its task
  successfully.

- **Disable init-container**

  Disabling the init-container is as simple as changing the flag mentioned above:
  
  ```yaml
  quantumleap:
    ...
    init:
      enabled: false
    ...
  ```
  
  and run the command:
  
  ```console
  $ helm install quantumleap quantumleap/chart/
  ```

### Air Quality App

To install the chart with the release name `air-quality-app`:

```console
$ helm install air-quality-app air-quality-app/chart/
```

### Grafana

To install the chart with the release name `grafana`:

```console
$ helm dependency up grafana/chart/
$ helm install grafana grafana/chart/
```

## TODO

- Despliegue mediante Gitlab CI/CD

## License

for the ODALA project.

© 2022 HOPU

License EUPL 1.2

![](https://ec.europa.eu/inea/sites/default/files/ceflogos/en_horizontal_cef_logo_2.png)
