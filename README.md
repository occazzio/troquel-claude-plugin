# Troquel para Claude

Plugin de [Troquel](https://troquel.ai) para Claude Code, Cowork y la app de Claude.
Conecta Claude con tu cuenta de Troquel y le enseña a usarla: imágenes, video y voz
publicitarios, video UGC terminado y lectura de la biblioteca de anuncios de Meta.

Se paga por generación, con los créditos de tu cuenta (1 crédito = USD 0,01). Claude te
dice el precio antes de generar y lo que falla devuelve sus créditos.

## Instalar

En Claude Code:

```bash
claude plugin marketplace add occazzio/troquel-claude-plugin
```

```bash
claude plugin install troquel@troquel-ai
```

En la app de Claude o en Cowork: **Customize → Plugins**, agregá el marketplace desde
GitHub con `occazzio/troquel-claude-plugin` e instalá **Troquel**.

## Conectar tu cuenta

La primera vez, Claude te pide entrar a Troquel desde el navegador. En Claude Code es
`/mcp` → **troquel** → iniciar sesión. En la app, la pestaña **Connectors** del plugin.
Si no tenés cuenta, se crea en [troquel.ai](https://troquel.ai).

## Qué trae

| Pieza | Para qué |
|---|---|
| Conector `troquel` | Las herramientas de Troquel: generar imagen, video y voz, K-Chin Studio, Canvas, Meta Ad Library, puntuar un creativo, saldo y precios. |
| `/troquel:anuncios-producto` | Creativos de un producto real: sube el original, cotiza y genera. |
| `/troquel:investigar-competencia` | Lee los anuncios que una marca tiene activos en Meta, los etiqueta y puntúa los tuyos. |
| `/troquel:video-ugc` | Un video UGC terminado desde el link del producto, con guion y precio antes de cobrar. |

Las skills se cargan solas cuando el pedido coincide; no hace falta escribir el comando.

## Probalo

- "Hacé tres anuncios cuadrados de este producto" (y adjuntá la foto).
- "Mirá qué anuncios tiene activos esta marca en Meta" (y pegá el link de su biblioteca).
- "Armá un video UGC de 30 segundos de este producto" (y pegá el link de la tienda).

## English

Troquel plugin for Claude Code, Cowork and the Claude app. It connects Claude to your
Troquel account and teaches it the workflow: ad images, video and voice, finished UGC
videos, and reading a brand's Meta Ad Library. Pay per generation with your Troquel
credits (1 credit = USD 0.01); Claude quotes the price before generating.

Install with the two commands above, then sign in to Troquel when Claude asks.

## Soporte

[troquel.ai](https://troquel.ai) · contacto desde la app.

Licencia MIT para el contenido de este repositorio. El servicio de Troquel tiene sus
propios términos.
