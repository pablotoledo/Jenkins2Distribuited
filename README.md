Para montar las imágenes:

    docker build -t jtoledog/jenkins2-slave jenkins2-slave/.

    docker build -t jtoledog/jenkins2-master jenkins2-master/.

Para ejecutar los dockers:

    docker run -itd  -p 6022:22 --name=jenkins2-esclavo jtoledog/jenkins2-slave

    docker run -itd --name=jenkins2-maestro --link jenkins2-esclavo -p 6080:8080 -p 6050:50000 jtoledog/jenkins2-master 
    
Caso habitual:

    docker-compose up -d jenkins sonar nexus
    
Para obtener la IP local de algun contenedor:

    docker inspect CONTENEDOR | grep '"IPAddress"' | head -n 1 | awk -v x=2 '{ gsub("\"","");  gsub(",",""); print $x}'
    
Referencias utilizadas para Sonar:

    [http://sonarqube-archive.15.x6.nabble.com/Integrating-sonar-scoverage-plugin-with-maven-td5034968.html]
    [https://github.com/RadoBuransky/sonar-scoverage-plugin]
    [https://docs.sonarqube.org/display/SCAN/Analyzing+with+SonarQube+Scanner+for+Maven]
    
    En la carpeta de /opt/sonarqube/extensions/plugins se ha añadido:
        https://github.com/hantuzun/sonar-scalastyle/releases/download/v0.0.1-SNAPSHOT/sonar-scalastyle-plugin-0.0.1-SNAPSHOT.jar
        de: https://github.com/hantuzun/sonar-scalastyle/releases
