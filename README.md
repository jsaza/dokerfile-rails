# Ruby on Rails用 Dockerfile

* Rails構成ディレクトリ内でOK

```
Gemfile
Gemfile.lock
Rakefile
app
config
db
doc	
lib
log	
public
script	
test
tmp	
vendoer

--
Dockerfile * 
docker-compose.yml * 
entrypoint.sh * 
```

* 起動

```
$ docker-compose up -d
Building ruby_web
Step 1/14 : FROM ruby:2.5.3
 ---> 72aaaee1eea4
Step 2/14 : RUN apt-get update -qq && apt-get install -y nodejs --no-install-recommends && rm -rf /var/lib/apt/lists/*
 ---> Using cache
 ---> b8aea95ae9e4
Step 3/14 : RUN apt-get update && apt-get install -y mysql-client --no-install-recommends && rm -rf /var/lib/apt/lists/*
 ---> Using cache
 ---> be06d1ad7271
Step 4/14 : RUN apt-get update && apt-get install -y build-essential libpq-dev
 ---> Using cache
 ---> 00214c553fd6
Step 5/14 : COPY . /home
 ---> 81b55540f974
Step 6/14 : RUN ls -la
:
Removing intermediate container 3f3b5fb05e67
 ---> 448fca0aebee
Step 7/14 : RUN ls -la home
 ---> Running in cdbc4e4b17df
total 112
:
Removing intermediate container cdbc4e4b17df
 ---> f1d2be333056
Step 8/14 : WORKDIR /home
 ---> Running in 5c59cf5b434f
Removing intermediate container 5c59cf5b434f
 ---> eabbc54839dd
Step 9/14 : RUN gem install bundler
 ---> Running in 9b0eb2ad4bbf
Successfully installed bundler-2.0.1
1 gem installed
Removing intermediate container 9b0eb2ad4bbf
 ---> 7d235cd94bd3
Step 10/14 : RUN bundle install
 ---> Running in ee7de582976a
:
:
:
Removing intermediate container ee7de582976a
 ---> e97d429c69a9
Step 11/14 : COPY entrypoint.sh /usr/bin/
 ---> 264ecc97718a
Step 12/14 : RUN chmod +x /usr/bin/entrypoint.sh
 ---> Running in 2b30cbe9a7a5
Removing intermediate container 2b30cbe9a7a5
 ---> f9e879d4f0a0
Step 13/14 : ENTRYPOINT ["entrypoint.sh"]
 ---> Running in e36367a11f08
Removing intermediate container e36367a11f08
 ---> 25eb09e4dfa2
Step 14/14 : EXPOSE 3000
 ---> Running in ee5e3d1db7a8
Removing intermediate container ee5e3d1db7a8
 ---> 8c6473b480b6
Successfully built 8c6473b480b6
Successfully tagged ruby-test_ruby_web:latest
cker-compose build` or `docker-compose up --build`.
Creating Dir_ruby_db_1 ... done
Creating Dir_ruby_web_1 ... done
```

* 動作確認

```
$ docker-compose ps
        Name                   Command           State            Ports         
--------------------------------------------------------------------------------
Dir_ruby_db_1    docker-entrypoint.sh      Up      0.0.0.0:3306->3306/tcp,
                       mysqld                            33060/tcp              
Dir_ruby_web_1   entrypoint.sh bash -c     Up      0.0.0.0:3000->3000/tcp 
```
