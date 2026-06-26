# OneAPI4OneKey 接口文档

**Base URL**: `http://localhost:3000`

---

## 1. 注册

```
POST /api/user/register
Content-Type: application/json
```

### 请求

```json
{
  "username": "myapp",
  "password": "***"
}
```

### 响应

```json
{"success": true}
```

```bash
curl -X POST http://localhost:3000/api/user/register \
  -H "Content-Type: application/json" \
  -d '{"username":"myapp","password": "***"}'
```

---

## 2. 登录

```
POST /api/user/login
Content-Type: application/json
```

### 请求

```json
{
  "username": "myapp",
  "password": "***"
}
```

### 响应

```json
{
  "success": true,
  "data": {
    "id": 7,
    "username": "myapp",
    "access_token": "1a2b3c..."
  }
}
```

`access_token` 用于后续请求鉴权：

```
Authorization: Bearer ***
```

```bash
curl -X POST http://localhost:3000/api/user/login \
  -H "Content-Type: application/json" \
  -d '{"username":"myapp","password": "***"}'
```

---

## 3. 获取 API Key

登录后获取 deepseek 令牌。

```
GET /api/token/?p=0
Authorization: Bearer ***
```

### 响应

```json
{
  "success": true,
  "data": [{
    "id": 5,
    "key": "yLp3m...3004",
    "name": "deepseek",
    "models": "deepseek-v4-flash",
    "unlimited_quota": true,
    "expired_time": -1
  }]
}
```

取 `data[0].key` 即为 API Key，限模型 `deepseek-v4-flash`，永不过期。

```bash
curl http://localhost:3000/api/token/ \
  -H "Authorization: Bearer ***
```

---

## 4. Chat Completions

```
POST /v1/chat/completions
Authorization: Bearer ***
```

```bash
curl http://localhost:3000/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer *** \
  -d '{"model":"deepseek-v4-flash","messages":[{"role":"user","content":"你好"}]}'
```
