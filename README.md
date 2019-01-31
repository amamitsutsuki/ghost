ghost を docker-compose で動かす。
1/30/2019

以下の例では /opt/ghost にファイルを置いてます。
$ git clone https://github.com/amamitsutsuki/ghost.git

docker のインストール
$ sudo apt install apt-transport-https ca-certificates curl software-properties-common
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
$ sudo apt purge docker docker-engine docker.io

certbot で無料の ssl 取得。
先ずはマッピング先のディレクトリー先に作っておく。
$ sudo mkdir -p /opt/ghost/html

注意：先に http://blog.uemura.us に外からアクセス出来るようにしておかないとエラーでます。一旦何かつくるなりで終わったら消してください。
$ docker run -d -p 80:80 --name webserver -v /opt/ghost/html:/usr/share/nginx/html nginx
とかで用意しておく。
$ sudo add-apt-repository ppa:certbot/certbot$ sudo certbot certonly --agree-tos --webroot -w /opt/ghost/html/ -d blog.uemura.us
もう要らないので消す。もっといい方法ある？
$ docker stop webserver; docker rm webserver

$ docker-compose up -d
