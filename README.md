# AlvisAE

AlvisAE is an editor that facilitates the annotation of text documents with the goal of extracting knowledge.

This project is the server side of alvisae. It is a web service that implements all the operations to manage campaigns, documents, annotations, curations, tasks, workflows and users. It assures the storage of document annotations as well as linguistic processing via [AlvisNLP](https://github.com/Bibliome/alvisnlp).

## How to install
We assume that the user is familiar with the technologies and has glassfish and postgresql already installed in the server

### get the source code and package the web service

```sh
git clone https://github.com/mandiayba/alvisae
cd alvisae
mvn compile package
```

### create and initialize the database
[See here on how to initialize the database using the scala console](documentation/create-database.md)


### deploy the war
copy the generated package to a directory accessible from the GlassFish server

```
cp target/cdxws-lift-1.0-SNAPSHOT.war /tmp/
```

login as a user that is authorized to deploy packages on the Glassfish server

```
su glassfish \
cd \
glassfishv3/bin/asadmin  -p 5848 deploy --force  --contextroot <context root of the instance> --name <name of the instance> /tmp/cdxws-lift-1.0-SNAPSHOT.war \
```

### set-up database parameters
The content of property file look like this. Save the file with name of the following format <user>.<hostname>.props

```
db.type=postgresql
db.server=bddev
db.port=5432
db.dbname=annotation
db.username=annotation_admin
db.password=*****
db.schema=aae_newinstance
```

One simplest way to setup the parameters is by using these two glassfish commands :

```
GLASSFISH_HOME/bin/asadmin set-web-context-param --name configFilePath --value 'path/to/the/config/file' 'the_application_name'

GLASSFISH_HOME/bin/asadmin restart-domain
```
## How to use
The web service implement the [aero protocol](https://github.com/openminted/omtd-aero). Here are the calls for the moment avalaible to the users. 

### Projects
#### List Projects
```sh
curl -u aae_root:Tadmin -w "%{http_code}" http://localhost:8080/alvisae/api/projects
```
#### Create a project named **new project** with the creator name **ba**
```sh
curl -u aae_root:Tadmin -w "%{http_code}" -X POST -d 'name=new project&creator=ba' http://localhost:8080/alvisae/api/projects
```
#### Delete the project having **project_id == 1 ** 
```sh
curl -u aae_root:Tadmin -w "%{http_code}" -X DELETE http://localhost:8080/alvisae/api/projects/1
```

### Documents
#### List documents of a project (** project_id == 3 **)
```sh
curl -u aae_root:Tadmin -w "%{http_code}" http://localhost:8080/alvisae/api/projects/3/documents
```
#### Create a document named ** new document ** into the project **1**
```sh
curl -u aae_root:Tadmin -w "%{http_code}" -X POST -d 'name=new document&format=text&content=some content&creator' http://localhost:8080/alvisae/api/projects/1/documents
```
#### Delete Document
```
```

### Annotations
#### List Annotations
```
```
#### Create Annotation
```
```
#### Delete Annotation
```
```

