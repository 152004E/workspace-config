# ⚙️ Instalación y Configuración de Obsidian

Esta guía detalla cómo replicar el entorno de Obsidian con sincronización automatizada de Git en Fedora/Linux.

## 1. Instalación (Flatpak)
Para mantener el sistema limpio en Fedora o distribuciones Inmutables, se recomienda Flatpak:
```bash
flatpak install flathub md.obsidian.Obsidian
```

## 2. Preparación del Repositorio (Clave SSH)
Para que la automatización funcione en segundo plano sin pedir usuario o contraseña, es **obligatorio** usar SSH.
```bash
# 1. Asegúrate de tener una llave (ej. ~/.ssh/id_ed25519) agregada a GitHub
# 2. Clona la bóveda o cambia la URL si ya la tienes por HTTPS:
git remote set-url origin git@github.com:TU_USUARIO/TU_REPOSITORIO.git
```

## 3. Configuración del Plugin: Obsidian Git
Instala el plugin de la comunidad **Obsidian Git**. Para replicar el comportamiento de "Background Sync cada 15 minutos", la configuración en `data.json` (`.obsidian/plugins/obsidian-git/data.json`) debe quedar exactamente así:

```json
{
  "commitMessage": "vault backup: {{date}}",
  "autoCommitMessage": "vault backup: {{date}}",
  "autoSaveInterval": 15,
  "autoPushInterval": 0,
  "autoPullInterval": 0,
  "autoPullOnBoot": true,
  "pullBeforePush": true,
  "syncMethod": "merge",
  "differentIntervalCommitAndPush": false
}
```

### Explicación de los parámetros clave:
- `autoSaveInterval: 15`: Hace commit y push automático cada 15 minutos exactos.
- `autoPullOnBoot: true`: Cuando abras la app, descargará inmediatamente lo que haya subido el Bot de Telegram/n8n mientras la PC estaba apagada.
- `pullBeforePush: true`: Evita conflictos de Git descargando primero antes de empaquetar tus cambios locales.
- `differentIntervalCommitAndPush: false`: Obliga a que el timer de 15 minutos ejecute ambas acciones juntas.
