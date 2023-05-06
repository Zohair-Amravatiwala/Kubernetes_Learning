Set ENV variables
- Naked POD creation : kubectl run mydb --image=mysql --env="MYSQL_ROOT_PASSWORD=password"
- For Deployment we need to first create the deployment using kubectl create deploy and then use kubectl set env deploy <deployment_name> <Variable_KEY>=<variable_Value>

ConfigMaps can be used for 3 different types of configurations:
1) Variables
2) Configuration Files
3) command line Arguments
Based on these different types. ConfigMaps are created and used in different way.

If an application refers to a ConfigMap, it should exist in the cluster before running the application. Unlike the Volume.

# ConfigMap for Variables

- using --from-env-file : kubectl create cm --from-env-file=dbvars (--from-env-file flag can be used only single time)
- using --from-literal : kubectl create cm --from-literal=MYSQL_USER=zohair (--from-literal flag can be used multiple times to specify more than one variable)

After creating the configMao, use kubectl set env --from=configmao/<name> deploy/<deploy_name> to use config map in your deployment

- Create a new config map named my-config based on folder bar
  kubectl create configmap my-config --from-file=path/to/bar
  
  - Create a new config map named my-config with specified keys instead of file basenames on disk
  kubectl create configmap my-config --from-file=key1=/path/to/bar/file1.txt --from-file=key2=/path/to/bar/file2.txt
  
  - Create a new config map named my-config with key1=config1 and key2=config2
  kubectl create configmap my-config --from-literal=key1=config1 --from-literal=key2=config2
  
  - Create a new config map named my-config from the key=value pairs in the file
  kubectl create configmap my-config --from-file=path/to/bar
  
  - Create a new config map named my-config from an env file
  kubectl create configmap my-config --from-env-file=path/to/foo.env --from-env-file=path/to/bar.env

# ConfigMap for ConfigFiles

Config files needs to be mounted as volumes of type configMap.

# Secrets
- Secrets are not encrypted but base64 encoded.
- Three types of secrets are offered:
  1. docker-registry: used for connecting to docker registry.
  2. TLS: used to store TLS key material
   3. Generic: creates secret from local files, directory or literal value
- When creating the secret the type must be specified. kubectl create secret genric ....
- Secrets are used same as configmap. If it is a variable then use kubectl set env or if it is a file you need to mount it as a volume.
- While mounting the secret in the pod spec, consider using the defaultMode to set the permission defaultMode: 0400

Create a secret using specified subcommand.

Available Commands:
  docker-registry   Create a secret for use with a Docker registry
  generic           Create a secret from a local file, directory, or literal value
  tls               Create a TLS secret

Usage:
  kubectl create secret [flags] [options]



