# README

*I have archived this repo due to ty inactivity, mostly on my part. I have become far less active in Svelte development and feel this repo has become stale.*

## About

This is a Wails template using Svelte with Vite for asset bundling. Immediately after installing do the following:
 1. First, double-check the values in wails.json and frontend/package.json
 2. Run `npm install` from within the `frontend/` dir to install the JS dependencies
 3. Run `wails build` from the project root dir to build the `dist/` directory for the first time. Completing this is also a good first test.


## Live Development

To run in live development mode, go into the `frontend/` directory and run `npm run dev`. 
Then, in another terminal, run `wails dev` in the project directory. 
You can navigate to http://localhost:34115 in your browser to connect to your application or (preferably) just work off of the Wails app that launches via `wails dev`.

Changes made to frontend source files in should trigger Vite to reload and changes to any .go files should trigger Wails to recompile and reload.

## Building

To build a redistributable, production mode package, use `wails build`.

## Issues

From time to time I have noticed that the live reload seems to stop working, especially for the JS side. 
Normally, closing both dev servers and relaunching, starting with `npm run dev` in `frontend/` 
followed by `wails dev` in the project root seems to take care of that.


## Caveats

By default, Vite does not bundle source files when previewing with the dev server. 
It essentially acts as a no-bundle dev server, using the source files. 
This is feature needs to basically be disabled to function alongside of the Wails dev server.
Therefore, you will notice that the frontend is being rebuilt when Vite sees a change.
This is accomplished by changing the `npm run dev` command from `vite` to `vite build --watch` in `/frontend/package.json`.

As of this writing, Jan 2022, I have only tested this on macOS. I have yet to get a Windows dev environment set up. 
If you try this on Windows, I would appreciate it if you'd let me know how it went.


## Wails version v2.0.0-beta.33 and later

Starting with Wails version v2.0.0-beta.33 you can just use `wails dev` to start and monitor both frontend and backend changes simultaneously.

There is a new config setting for `wails.json` called `frontend:dev:watcher`. 
Im my experience it's best to set its value to an `npm run` script command that is launching `vite build --watch` rather than entering `vite build --watch` for the value.
At this point you should be able to just do `wails dev` and it will first launch the Vite watcher, then compile the app and launch it with just that one command.

Example `frontend/package.json`:
```
 "scripts": {
    "vite": "vite",
    "dev": "vite build --watch",
    "build": "vite build",
    "preview": "vite preview",
  },
```

And `wails.json`:
```
"frontend:build": "npm run build",
"frontend:install": "npm install",
"frontend:dev": "",
"frontend:dev:watcher": "npm run dev",
"wailsjsdir": "./frontend",
```

I will update these templates accordingly once more time has passed and no major issues have arisen. As of this writing (March, 2022) this is a brand new feature but one I thought was worth mentioning now.

More information can be found here: https://wails.io/docs/reference/project-config


## Shout-Outs

Being new to both Vite and Wails, the above-mentioned caveat gave me quite a fit for a while, 
but after comparing the `package.json` and `vite.config.js` files in the Wails + Vite + View templates with those 
generated by the Vite-Svelte scaffolded template, I was able to finally get it working. 
You can get more information about the Wails + Vite + View templates here:

 - https://github.com/codydbentley/wails-vite-vue-the-works
 - https://github.com/codydbentley/wails-vite-vue-ts
