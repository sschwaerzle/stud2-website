# Development

## Local Development

Prerequisites:
- git installed

1. Install hugo (e.g. via UniGetUI)
2. Clone the repository
3. cd into the repository and host the website with *hugo server*

# Theme

We use [the ananke theme](https://github.com/theNewDynamic/gohugo-theme-ananke). It was added as a git submodule.
Currently, it is not updated automatically. This has to be done via *git submodule update --remote*.
In the future, we might use *git pull --recurse-submodules* to handle this automatically.

# Add-Ons

# Deployment

After pushing to master, a workflow (under .github directory) builds the website and hosts it on github pages.
Currently, the workflow is a 1:1 copy of the one in [this official tutorial](https://gohugo.io/host-and-deploy/host-on-github-pages/).

# Images

We host images on a webserver, so as to keep this repository small. The plan is to connect the image folder to nextcloud, so that we can use python to scan the image folder. We then want to use this result to create a json with all of the image links. This json just has to go inside the hugo data folder. Then, we can access the pictures.
Snippet to get all pictures from the json location into the markdown concert page with the same name:
```
<!-- Fetch the concert images dynamically from links.json -->
  <h2>Images</h2>
  <ul>
    {{ $concertSlug := .File.BaseFileName }} <!-- Get the slug of the current concert -->
    {{ $images := index .Site.Data.links.concerts $concertSlug }} <!-- Get images from links.json for this concert -->
    
    {{ if $images }}
      {{ range $images }}
        <li><img src="{{ . }}" alt="Concert Image" width="300"></li>
      {{ end }}
    {{ else }}
      <p>No images available for this concert.</p>
    {{ end }}
  </ul>
```
