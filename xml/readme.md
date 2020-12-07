# XML processing

Consider the following file:

```xml
<!-- concat-md::include "./files/sample.txt" -->
```

## Extract the value of a node

Extract the value of the `project-name` node and display it

```bash
config="sample.xml"

projectName=$(grep -oP "(?<=<project-name>)[^<]+" $config)

echo -e "${projectName}\n${projectName//?/=}\n"
```

This sample will display:

```text
Test project
============
```

## Get the list of elements

Retrieve the list of elements in a XML file; limit the list based on the value of an attribute and return the value of a second attribute:

* Get the list of `<package>` nodes but only those with enabled=1 attribute
* Extract the name attribute of these nodes
* Then process them one by one

see https://unix.stackexchange.com/a/553142

```bash
packages=$(cat $config | tr -d '\n'| grep -Eo "<package[>\ ][^<]+enabled=\"1\"[^>]+." | grep -oP "(?<=name\=\")[^\"]*")

for package in $packages; do
    printf "Process '$package'\n"
done
```

This sample will display:

```text
Process 'git'
Process 'postgres'
```
