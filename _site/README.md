# OstentatiousBrewingWebsite

This is my website, yo! :beer:

## Local Preview Using Docker

You can preview the site locally without installing Ruby/Jekyll by using the official Jekyll Docker image.

Docker:

```bash
# from the repository root
docker run --rm -it -p 4000:4000 \
	-v "$PWD":/srv/jekyll \
	-v "$PWD"/.bundle:/usr/local/bundle \
	jekyll/jekyll:4.2.0 jekyll serve --watch --host 0.0.0.0
```

Open http://localhost:4000 in your browser to review the site. Stop the server with Ctrl+C.

Notes:
- Use Docker if you don't want to install Ruby locally.
- To emulate dark mode, enable your system dark theme or use browser devtools (Emulate CSS media > prefers-color-scheme: dark).
