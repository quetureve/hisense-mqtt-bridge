# Hisense MQTT Bridge — быстрый старт
---

## 1. Установка Docker

### Обновление системы

```bash
sudo apt update && sudo apt upgrade -y
```

### Зависимости

```bash
sudo apt install -y ca-certificates curl gnupg
```

### Ключ Docker

```bash
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

### Репозиторий

```bash
echo \
  "deb [arch=arm64 signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  $(. /etc/os-release && echo $VERSION_CODENAME) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### Установка

```bash
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

---

## 2. Проверка

```bash
docker --version
docker compose version
```

---

## 3. Скачивание проекта

```bash
git clone https://github.com/quetureve/hisense-mqtt-bridge.git
cd hisense-mqtt-bridge/docker
```

---

## 4. Запуск MQTT

```bash
docker compose up -d
```

---

## ⚠️ Важно

* `docker-compose.yml` поднимает следующие контейнеры:

  * MQTT брокер (Mosquitto)
  * Home Assistant
  * Portainer (UI для управления Docker)

* При необходимости отредактируй перед запуском:

  * `docker-compose.yml` (порты, IP, устройства)
  * `data_mosquitto/config/mosquitto.conf` (MQTT настройки)
  * сертификаты в `data_mosquitto/certs/`

---

## ✅ Готово

MQTT-брокер запущен и готов для использования с Home Assistant и Hisense TV.
