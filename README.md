# C# Sample Accelerator

A sample accelerator for C#.

This sample is the Weather Forecast RESTful API application made available from Microsoft.

The starting source for this sample was created using:
```
$ dotnet new webapi --framework net6.0 --language C#
```

## Running the app locally

To run the sample application:

```
$ dotnet run
```

## Deploying to Azure Spring Apps with Azure CLI

Here, we will deploy the application on Azure Spring Apps, ensure that all prerequisites are met

Prerequisites:

* Completion of [Create Azure Spring Apps service instance](https://github.com/Azure-Samples/acme-fitness-store/blob/Azure/README.md#create-azure-spring-apps-service-instance)

### Create the application in Azure Spring Apps

Create an application:

```shell
az spring app create --name ${SERVICE_APP} \
  --assign-endpoint true \
  --instance-count 1 \
  --memory 1Gi
```
> Note: The app will take around 2-3 minutes to create.

### Build and Deploy the Application

Deploy and build the application, specifying its required parameters

```shell
az spring app deploy --name ${SERVICE_APP} \
    --source-path weatherforecast-csharp 
```
> Note: Deploying the application will take 5-10 minutes

### Test the Application

Run the following commands

```shell
export APP_URL=$(az spring app show --name ${SERVICE_APP} --query properties.url | tr -d '"')

curl "${APP_URL}/WeatherForecast"
```
