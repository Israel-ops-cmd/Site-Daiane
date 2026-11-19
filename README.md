# Site Daiane Freire | Massoterapeuta

Site estático (HTML, CSS e JS num único `index.html`), sem etapa de build.

## Rodar localmente

```bash
cd site-daiane
python -m http.server 8080
```

Abra http://localhost:8080. Abrir o `index.html` direto no navegador também funciona, mas as fontes e imagens usam caminhos absolutos (`/img/...`), então prefira o servidor local.

## Estrutura

```
index.html            página inteira (CSS e JS embutidos)
img/                  fotos em .webp (800 e 1600px; recortes em 700 e 1200px)
fonts/                Instrument Serif e Figtree (woff2, latin)
vendor/               GSAP 3.12.5 + ScrollTrigger e Lenis 1.1.13 (versões fixas)
favicon.svg, apple-touch-icon.png, og-image.jpg
vercel.json           cleanUrls e cache longo para img, fonts e vendor
```

Obs.: as fotos originais têm no máximo ~1100px de largura, então a versão "1600" tem a largura original (não foi ampliada).

## Publicar

Cada push na branch `main` publica sozinho na Vercel (projeto ligado ao repositório).
Configuração do projeto na Vercel: Framework Preset **Other**, Build Command vazio, Output Directory `./`.

Ao trocar de domínio, atualizar no `index.html`: `<link rel="canonical">`, `og:url`, `og:image`, `twitter:image` e o `url`/`image` do JSON-LD.

## Trocar fotos

Mantenha os mesmos nomes de arquivo em `img/`. Para gerar as versões:

```bash
# com fundo (ex.: 05)
cwebp -q 80 -resize 800 0 original.jpg -o img/05-ventosa-costas-COM-FUNDO-800.webp
# recorte com transparência (ex.: 01)
cwebp -q 82 -resize 700 0 recorte.png -o img/01-hero-SEM-FUNDO-700.webp
```
