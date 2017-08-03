Para montar las imágenes:

    docker build -t jtoledog/jenkins2-slave jenkins2-slave/.

    docker build -t jtoledog/jenkins2-master jenkins2-master/.

Para ejecutar los dockers:

    docker run -itd  -p 6022:22 --name=jenkins2-esclavo jtoledog/jenkins2-slave

    docker run -itd --name=jenkins2-maestro --link jenkins2-esclavo -p 6080:8080 -p 6050:50000 jtoledog/jenkins2-master 
    
Caso habitual:

    docker run -itd  -p 6022:22 --name=jenkins2-esclavo jtoledog/jenkins2-slave

    docker run -itd --name=jenkins2-maestro --link jenkins2-esclavo -p 6080:8080 -p 6050:50000 jtoledog/jenkins2-master

    docker run -tid --name jenkins-sonar -p 6001:9000 -p 6092:9092 jtoledog/jenkins2-master:sonar

    docker run -tid -p 6081:8081 --name jenkins-nexus jtoledog/jenkins2-master:nexus
    
Para obtener la IP local de algun contenedor:

    docker inspect CONTENEDOR | grep '"IPAddress"' | head -n 1 | awk -v x=2 '{ gsub("\"","");  gsub(",",""); print $x}'
