To start Sonar stuff:
```
$ cd  sonarqube-server
$ docker-compose up -d
$ cd -
```

To clone and build modified plugin
```
$ git clone git@github.com:checkstyle/sonar-checkstyle.git
$ docker run -it --rm --name sonar-checkstyle -v "$PWD":/usr/src/mymaven -w /usr/src/mymaven maven:latest mvn clean install
```

To eval the source code:
```
$ cd demo-project
$ docker run --network=sonarpg_sonarnet --rm -v $PWD/:/data -w /data techdivision/docker-sonar-scanner:latest sonar-scanner -Dsonar.host.url=http://$(docker inspect --format '{{ .NetworkSettings.Networks.sonarpg_sonarnet.IPAddress }}' sonarpg_sonarqube_1):9000 -Dsonar.login=****************************** -Dsonar.projectKey=JSDEMO -Dsonar.sources=.  -Dsonar.projectVersion=1.0
$ cd -
```
