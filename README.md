# Tutorial: Como remapear botões do mouse com keyd no Fedora

Este tutorial ensina a remapear os botões do mouse usando o daemon **keyd** no Fedora.

---

## 1. Identificar o ID do mouse

Para descobrir o ID do seu mouse USB, use:

```bash
lsusb
````

Exemplo de saída:

```
Bus 001 Device 006: ID 1bcf:0005 Sunplus Innovation Technology Inc. Optical Mouse
```

O ID do dispositivo neste exemplo é `1bcf:0005`. Guarde esse valor.

---

## 2. Descobrir os códigos dos botões do mouse

Use o comando abaixo para monitorar os eventos do mouse diretamente com o keyd:

```bash
sudo keyd monitor
```

Agora pressione os botões do mouse e observe as saídas. Exemplo:

```
mouse1 down
mouse1 up
mouse2 down
mouse2 up
middlemouse down
middlemouse up
```

Esses nomes são os códigos que você utilizará na configuração.

---

## 3. Criar ou editar `/etc/keyd/default.conf`

Edite o arquivo de configuração padrão do keyd:

```bash
sudo nano /etc/keyd/default.conf
```

Adicione o seguinte conteúdo (substitua o ID pelo do seu mouse):

```ini
[ids]
1bcf:0005

[main]
mouse1 = C-v
mouse2 = C-c
middlemouse = backspace
```

---

## 4. Aplicar as alterações

Após salvar o arquivo, reinicie o serviço do keyd:

```bash
sudo systemctl restart keyd
```

Verifique se está rodando corretamente:

```bash
systemctl status keyd
```

---

## Notas

* Você pode usar `keyd list-keys` para ver todos os nomes de teclas e atalhos válidos.
* Atalhos seguem a sintaxe:

  * `C-` para Ctrl
  * `A-` para Alt
  * `S-` para Shift
  * `M-` para Meta (Windows/Super)

---

## Exemplo prático

Remapear botões laterais do mouse para copiar e colar:

```ini
[main]
mouse1 = C-v
mouse2 = C-c
```

---

## Referências

* [Repositório oficial do keyd](https://github.com/rvaiya/keyd)
* `sudo keyd monitor` para testar eventos do mouse
