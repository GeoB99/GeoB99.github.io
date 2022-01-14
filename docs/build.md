# Building website

## How to build and preview locally this website

1. Clone the website

`git clone URL_REPO`

2. Download and install [gohugo binary](https://github.com/gohugoio/hugo/releases). You have two main options: you could move the gohugo binary to PATH and then use as any installed program with the command `hugo` or you could download it, and move to the repo you want to build/serve. 

3. You can have a preview of the website using `hugo serve` or `./hugo serve`. Open your browser at `localhost:3000` and the website will be build locally (and temporarely, meaning that CTRL-C in the shell aborts the server and clear the caches created). Naturally, the server is only for development and can not be used for production. The 

## How to build HTML

Simply execute `hugo build` to generate the directory that contains all the static file. Use `--minify` option to keep HTML and CSS minified. Use `--builddrafts` to build drafts. More flags can be found [here](https://gohugo.io/getting-started/usage/).

###
WARNING BuildURL does not need trailing slash!!!!!!!