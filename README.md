# Hisense MQTT Bridge — быстрый старт

---

## 📦 Структура

После скачивания файлов у тебя должна быть структура:

```id="k9g3x2"
docker/
├── docker-compose.yml
└── data_mosquitto/
```

👉 Папка `docker/` — корень проекта для Docker.
Запускать нужно именно из неё.

---

## 1. Установка Docker (ARM64 и AMD64)

```bash id="y0m2c1"
apt update && apt upgrade -y
apt install -y ca-certificates curl gnupg
```

Добавляем ключ:

```bash id="m1z9a4"
install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/debian/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg
chmod a+r /etc/apt/keyrings/docker.gpg
```

Добавляем репозиторий (автоопределение архитектуры):

```bash id="p8w6e3"
ARCH=$(dpkg --print-architecture)
echo "deb [arch=$ARCH signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian $(. /etc/os-release && echo $VERSION_CODENAME) stable" > /etc/apt/sources.list.d/docker.list
```

Установка:

```bash id="c4t7r2"
apt update
apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

---

## 2. Проверка

```bash id="h2k8n5"
docker --version
docker compose version
```

---

## 3. Скачивание проекта

```bash id="u7d3l9"
git clone https://github.com/quetureve/hisense-mqtt-bridge.git
cd hisense-mqtt-bridge
```

👉 Перенеси папку `docker/` в удобное место, например:

```bash id="x5q1v6"
mv docker /opt/
cd /opt/docker
```

---

## 4. Запуск

```bash id="b6n4s8"
docker compose up -d
```

Проверка:

```bash id="j3f9w1"
docker ps
```

---

## 5. MQTT доступ

* Host: `localhost`
* Port: `1883`

---

## ⚠️ Важно

* Запускать нужно **из папки, где лежит `docker-compose.yml`**

* Рядом должна быть папка `data_mosquitto/`

* `docker-compose.yml` поднимает:

  * Mosquitto (MQTT брокер)
  * Home Assistant
  * Portainer

* При необходимости отредактируй:

  * `docker-compose.yml`
  * `data_mosquitto/config/mosquitto.conf`
  * сертификаты в `data_mosquitto/certs/`

* Убедись, что:

  * порт `1883` свободен
  * подсеть не конфликтует с твоей сетью
  * `/dev/ttyUSB0` существует (если используется)

---

## ✅ Готово

MQTT bridge запущен и готов к работе с Hisense TV.
