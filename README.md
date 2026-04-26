# Qwen3.5-2B + llama.cpp (Docker)

Этот проект разворачивает локальный сервер LLM модели **Qwen3.5-2B** с помощью **llama.cpp** в Docker.

Модель доступна через OpenAI-compatible API и может принимать запросы через `curl` или любые HTTP-клиенты.

## Требования
- Linux (Debian/Ubuntu)
- Docker и Docker Compose
- 4-8 GB RAM

## Установка и запуск
### 0. Запустите виртуальную машину

### 1. Подключение к серверу (VM)
```bash
ssh -i C:\адрес\.ssh\сам ключ user@0.0.0.0
```
- 0.0.0.0 - IP адрес вашей виртуальной машины
- C:\адрес\.ssh\сам ключ - путь к SSH ключу
- user - имя пользователя на сервере

⚠️⚠️⚠️**Пропустите шаг 0 и 1, если запускаетесь локально у себя**

### 2.Клонирование репозитория
```bash
git clone https://github.com/milituzess/llm-qwen.git
cd llm-qwen
```

### 3. Создание папки для модели
```bash
mkdir models
cd models
```
### 4. Скачивание модели
```bash
wget https://huggingface.co/unsloth/Qwen3.5-2B-GGUF/resolve/main/Qwen3.5-2B-Q4_K_M.gguf
```
### 5. Возврат в корень проекта
```bash
cd ..
```
### 6. Настройка окружения
```bash
cp .env.example .env
```
⚠️⚠️⚠️ **Файл .env можно не изменять**

### 7. Запуск Docker
Обычный запуск:
```bash
sudo docker compose up -d
```
или 
```bash
sudo usermod -aG docker $USER
exit
```
Затем подключиться заново, зайти в папку llm-qwen и:
```bash
docker compose up -d
```
### 8. Проверка работы
```bash
docker ps
```
**Вы должны увидеть запущенный контейнер llama-server**

### 8. Тестирование 
Пример запроса:
```bash
curl -N -X POST http://localhost:8080/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "Qwen3.5-2B",
    "messages": [
      {"role": "user", "content": "Привет!"}
    ],
    "max_tokens": 200,
    "temperature": 0.7,
    "stream": false
  }'
```
**Вместо "Привет!" вы можете написать любое другое сообщение**

### 9. Остановка сервера
```bash
docker stop llama-server
```
Проверка:
```bash
docker ps
```
**Вы увидете пустой список(или без llama-server)**

Вот и всё, кто до конца дочитал - тот молодец
