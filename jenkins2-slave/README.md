
 docker build --rm -t esclavo .

 docker run -d --name slave -p 2222:22 esclavo
