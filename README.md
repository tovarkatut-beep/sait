# sait

## WaveSpeed MCP setup

Цей репозиторій містить конфігурацію MCP-сервера [WaveSpeed](https://pypi.org/project/wavespeed-mcp/) для Claude Code (`.mcp.json`).

### Встановлення

```bash
pip install wavespeed-mcp
```

### Налаштування ключа

Ключ **не зберігається в репозиторії**. Задайте його через змінну середовища перед запуском Claude Code:

```bash
export WAVESPEED_API_KEY=ваш_ключ
```

Або додайте сервер вручну у свій локальний конфіг:

```bash
claude mcp add wavespeed \
  -e WAVESPEED_API_KEY=ваш_ключ \
  -- wavespeed-mcp
```

У середовищах Claude Code on the web додайте `WAVESPEED_API_KEY` у налаштування середовища (environment variables), і `.mcp.json` підхопить його автоматично.
