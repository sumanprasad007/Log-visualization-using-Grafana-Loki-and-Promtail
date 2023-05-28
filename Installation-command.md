https://onedrive.live.com/view.aspx?resid=3881176461C0B223%21961&id=documents&wd=target%28Projects.one%7C3101AC34-FF83-4A16-8543-68DBB5E5D4BC%2F%F0%9F%93%A2%20Observability%20-%20Grafana%20%26%20Prometheus%7CCAAE82D8-90F2-4D0F-80FC-3E7680F6D9D1%2F%29
onenote:https://d.docs.live.net/3881176461c0b223/Documents/2022/Old%20stuffs/OneNote%20Notebooks/Morning%20Planning/Projects.one#📢%20Observability%20-%20Grafana%20%20Prometheus&section-id={3101AC34-FF83-4A16-8543-68DBB5E5D4BC}&page-id={CAAE82D8-90F2-4D0F-80FC-3E7680F6D9D1}&object-id={70BF5401-E446-4F61-A695-47D09C964AE0}&8B

Video:
https://youtu.be/QwGm5m4AxNA
Install Grafana on Debian or Ubuntu
sudo apt-get install -y apt-transport-https
sudo apt-get install -y software-properties-common wget
sudo wget -q -O /usr/share/keyrings/grafana.key https://apt.grafana.com/gpg.key

Stable release
echo "deb [signed-by=/usr/share/keyrings/grafana.key] https://apt.grafana.com stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
Beta release
echo "deb [signed-by=/usr/share/keyrings/grafana.key] https://apt.grafana.com beta main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
# Update the list of available packages
sudo apt-get update
# Install the latest OSS release:
sudo apt-get install grafana


Install Loki and Promtail using Docker

Download Loki Config
wget https://raw.githubusercontent.com/grafana/loki/v2.8.0/cmd/loki/loki-local-config.yaml -O loki-config.yaml

Run Loki Docker container
docker run -d --name loki -v $(pwd):/mnt/config -p 3100:3100 grafana/loki:2.8.0 --config.file=/mnt/config/loki-config.yaml

Download Promtail Config
wget https://raw.githubusercontent.com/grafana/loki/v2.8.0/clients/cmd/promtail/promtail-docker-config.yaml -O promtail-config.yaml

Run Promtail Docker container
docker run -d --name promtail -v $(pwd):/mnt/config -v /var/log:/var/log --link loki grafana/promtail:2.8.0 --config.file=/mnt/config/promtail-config.yaml


