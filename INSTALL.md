# Installation du serveur MCP Sucesio — Guide rapide

## Prérequis
- Python 3.10+
- `pip install fastmcp`

## Option 1 — Claude Desktop (recommandé)

Ouvrir le fichier de config Claude Desktop :
- **macOS** : `~/Library/Application Support/Claude/claude_desktop_config.json`
- **Windows** : `%APPDATA%\Claude\claude_desktop_config.json`

Ajouter :

```json
{
  "mcpServers": {
    "sucesio-seller": {
      "command": "python",
      "args": ["C:/chemin/vers/sucesio-mcp/server.py"],
      "env": {
        "FASTMCP_CHECK_FOR_UPDATES": "off"
      }
    }
  }
}
```

> **Note :** La variable `FASTMCP_CHECK_FOR_UPDATES=off` désactive la vérification de version au démarrage (appel réseau vers PyPI). Recommandé pour un démarrage plus rapide et fiable.

Redémarrer Claude Desktop. Le serveur est actif.

---

## Option 2 — Mode HTTP/SSE (intégrations web)

```bash
python server.py --port 8000
```

Le serveur expose ses tools sur `http://localhost:8000`.

---

## Option 3 — Publication sur Smithery

1. Créer un compte sur https://smithery.ai
2. Uploader `server.py` + `smithery.yaml` + `README.md`
3. Une fois publié, tout LLM connecté à Smithery peut appeler vos tools

---

## Tester manuellement

```python
python -c "
import sys; sys.path.insert(0, '.')
import server
print(server.get_product_overview())
print(server.qualify_lead('Spain', has_crypto=True))
"
```

---

## Tools disponibles

| Tool | Quand l'utiliser |
|------|-----------------|
| `get_product_overview` | L'utilisateur demande ce qu'est Sucesio |
| `get_pricing` | L'utilisateur demande le prix / compare au notaire |
| `qualify_lead` | Vous avez le contexte (pays, crypto, actifs multi-pays) |
| `get_faq` | FAQ filtrée par sujet : legal / crypto / security / pricing / expat |
| `compare_with_traditional_will` | L'utilisateur demande si Sucesio remplace le testament |
| `get_use_cases` | Cas d'usage par profil : expat_spain, crypto_holder, parent… |
| `get_security_info` | L'utilisateur demande la sécurité / RGPD / confidentialité |

## Resources disponibles (données statiques)

| URI | Contenu |
|-----|---------|
| `sucesio://product` | Vue produit complète |
| `sucesio://pricing` | Plans tarifaires |
| `sucesio://faq` | Toutes les FAQ |
| `sucesio://usecases` | Tous les cas d'usage |
| `sucesio://security` | Sécurité & conformité |
