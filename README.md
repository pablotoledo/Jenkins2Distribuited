Para montar las imágenes:

    docker build -t jtoledog/jenkins2-slave jenkins2-slave/.

    docker build -t jtoledog/jenkins2-master jenkins2-master/.

Para ejecutar los dockers:

    docker run -itd  -p 6022:22 --name=jenkins2-esclavo jtoledog/jenkins2-slave

    docker run -itd --name=jenkins2-maestro --link jenkins2-esclavo -p 6080:8080 -p 6050:50000 jtoledog/jenkins2-master 