

# SIT
## campaign rule adapter service sit
* restart: 
```provisioning-cli app restart --api provisioning-asia.platform.manulife.io --org ASIAREGIONAL-SEA-SIT --space HK_SHARED --foundation SEA --token xxx --appName hk-campaign-rules-adapter-service-sit DEBUG=true```


##  hk-cws-fcm
* delete:
``` provisioning-cli app delete --api provisioning-asia.platform.manulife.io --org ASIAREGIONAL-SEA-SIT --space HK_EXTERNALIZE --foundation SEA --token xxx --appName hk-cws-fcm-sit DEBUG=true ```


## sam-authorization
* promote:
``` provisioning-cli proxy upsert --api provisioning-asia.platform.manulife.io --token xxx --subBusinessEntity '' --basePath /v1/agent/authorization/edgemicro/hk/sit --proxyTeamName HK_AGENT --countryCode hk --appName '' --consumingBusinessUnit '' --backendName sam-authorization-service --businessEntity agent --env dev --version v1 --target https://sam-authorization-service-hk-agent-sit.apps.sea.preview.pcf.manulife.com --ignoreProdNamingConvention=true --proxyExt=false --moveProductsApps=true --microgateway=true --ignoreAppNamingConvention=true  ```

## hk-cws-login-web-app
* delete:
``` provisioning-cli app delete --api provisioning-asia.platform.manulife.io --org ASIAREGIONAL-SEA-SIT --space HK_EXTERNALIZE --foundation SEA --token xxx --appName hk-cws-login-web-app DEBUG=true ```

## eb-dst-service-hk
* get service key:
  ``` provisioning-cli service get-service-key --name eb-dst-service-hk-azuredb --serviceKeyName flyway_repair_eb-dst-service-hk-azuredb_5 --api provisioning-asia.platform.manulife.io --org ASIAREGIONAL-SEA-SIT --space HK_MPF_EB --foundation SEA --token xxx  DEBUG=true  ```

# UAT

## campaign rule adapter service uat
*  deploy:
```provisioning-cli app push-with-smoke-test --api provisioning-asia.platform.manulife.io --org ASIAREGIONAL-EAS-UAT --space HK_SHARED --foundation EAS --token xxx --smokeTestScript smokeTestScript.bat --appName hk-campaign-rules-adapter-service-uat --manifestFile manifest.yml   --buildPacks java_buildpack_offline --framework java --sourcePath temp/ --routes hk-campaign-rules-adapter-service-uat.apps.eas.pcf.manulife.com --deleteOldApp true  DEBUG=true```


## hk-productinfo-data-service-uat
* delete:
```provisioning-cli app delete --api provisioning-asia.platform.manulife.io --org ASIAREGIONAL-EAS-UAT --space HK_SHARED --foundation EAS --token xxx  --appName hk-productinfo-data-service-uat-new DEBUG=true``` 

## hk customer config server
* create:
``` provisioning-cli service create --api provisioning-asia.platform.manulife.io --org ASIAREGIONAL-EAS-UAT --space HK_CUSTOMER --foundation EAS --token xxx  --name hk_config_server_customer --serviceName p-config-server --plan standard --parametersFile config.json DEBUG=true```

 