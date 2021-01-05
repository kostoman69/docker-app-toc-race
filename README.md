Toc Race application 
- mysql
- adminer
- traccar/traccar/
    Traccar server image
    We just need to overwrite the configuration file traccar.xml. So, tere is no need to construct a new image!
    Just run a original one and mount as bind mout the file traccar.xml. We can also mount the logs of traccar server if needed.
    For details about using the traccar imge see:
    https://hub.docker.com/r/traccar/traccar 
- kostoman/toc-ranking

The toc race application uses the external volume toc_data which contains the folders that MySQL saves the databases. So, before we up the application we must create that external volume:

$ docker run --rm -v volume-name:/from alpine ash -c "cd /from ; tar -cf - . " | ssh hostname 'docker run --rm -i -v volume-name:/to alpine ash -c "cd /to ; tar -xpvf - " 

Ή βήμα-βήμα:

$ docker run --rm -v volume-name:/from alpine ash -c "cd /from ; tar -cf - . " > data.tar
$ scp data.tar remote-host:/root
$ cat data.tar | docker run --rm -i -v volume-name:/to alpine ash -c "cd /to ; tar -xpvf - "