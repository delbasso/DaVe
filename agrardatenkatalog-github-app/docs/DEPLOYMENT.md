# Deployment

## Empfohlener Weg: Vercel

Diese App ist eine Next.js-App. Sie kann direkt ueber Vercel aus einem GitHub-Repository deployed werden.

### Schritte

1. Neues GitHub-Repository erstellen.
2. Den Inhalt dieses Ordners hochladen.
3. Bei Vercel ein neues Projekt aus dem GitHub-Repository erstellen.
4. Environment Variables setzen:

```env
WEAVIATE_URL="https://dein-cluster.weaviate.cloud"
WEAVIATE_API_KEY="dein-weaviate-api-key"
WEAVIATE_COLLECTION="AtomicRequirement"
```

5. Deploy ausfuehren.

## Wichtig

Der Weaviate-Key darf nie in den Browser-Code geschrieben werden. Deshalb liegen alle Weaviate-Abfragen in `src/app/api/...`.

## Wenn Weaviate spaeter nicht mehr verfuegbar ist

Dann kann die App weiterhin als Prototyp und Codebasis dienen. Die Live-Suche muesste dann auf eine andere Datenquelle umgestellt werden.
